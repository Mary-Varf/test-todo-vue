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
            <p class="item__title" v-bind:class="{hidden: isEdited}">{{task.title}}</p>
            <input
                v-model="title"
                class="input item__input"
                v-bind:class="{hidden: !isEdited}"
            />
            <button v-if="isEdited" class="btn btn-reset btn-isEdited" v-on:click="handleSave">Save</button>
            <button v-else class="btn btn-reset btn-isEdited" v-on:click="handleEdit">Edit</button>
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
        handleEdit() {
            document.querySelectorAll('.item__input').forEach(el => el.classList.add('hidden'));
            document.querySelectorAll('.item__title').forEach(el => el.classList.remove('hidden'));
            this.$emit('isEdited-task', this.task.id);
            this.isEdited = true;
        },
        handleSave() {
            if (this.title.trim()) {
                const newTask = { ...this.task, title: this.title };
                this.$emit('edit-task', newTask);
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