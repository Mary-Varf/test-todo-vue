<template>
    <li @drop="onDrop($event, currentPosition)">
        <div
            class="main__item item grid"
            v-bind:class="{checked: task.status, dragged: isDragged}"
            draggable
            @dragstart="onDragStart($event, currentPosition)"
            @dragend="onDragEnd"
            @dragover.prevent
            @dragenter.prevent
        >
            <div class="item__checkbox">
                <input type="checkbox" class="checkbox" v-model="task.status"/>
                <label for="happy"></label>
            </div>
            <p class="item__title">{{title}}</p>
            <input
                v-model="title"
                class="input item__input"
                v-on:keyup.enter="handleSave"
            />
            <button class="btn btn-reset btn-isEdited btn-save" v-on:click="handleSave">Save</button>
            <button class="btn btn-reset btn-isEdited btn-edit" v-on:click="handleEdit($event)">Edit</button>
            <button class="btn btn-reset btn-delete" v-on:click="$emit('delete-task', task.id)"></button>
        </div>
    </li>
</template>

<script>
export default {
    data() {
        return {
            title: this.task.title,
            isEdited: false,
            isDragged: false,
        }
    },
    methods: {
        handleEdit(ev) {
            const targetParent = ev.target.parentNode;

            document.querySelectorAll('.main__item').forEach(el => el.classList.remove('edited'));
            targetParent.classList.add('edited');
            this.$emit('isEdited-task', this.task.id);
            this.isEdited = true;
        },
        handleSave() {
            if (this.title.trim()) {
                const newTask = { ...this.task, title: this.title };
                this.$emit('edit-task', newTask);
                document.querySelectorAll('.main__item').forEach(el => el.classList.remove('edited'));
                this.isEdited = false;
            } else {
                this.isEdited = true;
            }
        },
        onDragStart(ev, id) {
            ev.dataTransfer.dropEffect = 'move';
            ev.dataTransfer.effectAllowed = 'move';
            ev.dataTransfer.setData('itemId', id);

            this.isDragged = !this.isDragged; 
        },
        onDragEnd() {
            this.isDragged = !this.isDragged;
        },
        onDrop(ev, index) {
            const itemId = parseInt(ev.dataTransfer.getData('itemId'));
            
            this.$emit('change-index', itemId, index);
        }
    },
    props: {
        task: {
            type: Object,
            required: true,
        },
        currentPosition: {
            type: Number,
            required: true,
        }
    }
}
</script>

<style scoped>
    .edited {
        background-color: lightyellow;
    }
    .btn-save {
        display: none;
    }
    .item__input {
        display: none;
    }
    .edited > .btn-edit {
        display: none;
    }
    .edited > .btn-save {
        display: block;
    }
    .edited > .item__input {
        display: block;
    }
    .item__title {
        display: block;
    }
    .edited > .item__title {
        display: none;
    }
    .checked > .item__title{
        text-decoration: line-through;
    }
    .main__item {
        cursor: pointer;
    }
    .main__item > p {
        margin:0;
    }
    .dragged {
        background-color: yellow;
    }
</style>