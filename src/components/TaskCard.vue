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
          <input type="checkbox" v-bind:id="currentPosition" v-model="task.status"/>
          <label v-bind:for="currentPosition"></label>
      </div>
      <p class="item__title">{{title}}</p>
      <input
          v-model="title"
          class="input item__input"
          @keyup.enter="handleSave"
      />
      <button class="btn btn-reset btn-icon btn-isEdited btn-save" @click="handleSave">
        <svg version="1.1" id="Capa_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px"
            viewBox="0 0 330 330" style="enable-background:new 0 0 330 330;" xml:space="preserve">
            <path d="M325.606,84.668L245.334,4.394c-2.813-2.813-6.628-4.393-10.607-4.393H195.02C195.013,0.001,195.007,0,195,0H75
            c-0.007,0-0.013,0.001-0.02,0.001H15c-8.284,0-15,6.716-15,15V315c0,8.284,6.716,15,15,15h60h180h60c8.284,0,15-6.716,15-15V95.274
            C330,91.296,328.42,87.48,325.606,84.668z M90,30.001h30V70c0,8.284,6.716,15,15,15s15-6.716,15-15V30.001h30V110H90V30.001z
            M240,240H90v-30h150V240z M90,300v-30h150v30H90z M300,300h-30V195c0-8.284-6.716-15-15-15H75c-8.284,0-15,6.716-15,15v105H30
            V30.001h30V125c0,8.284,6.716,15,15,15h120c8.284,0,15-6.716,15-15V30.001h18.515L300,101.487V300z"/>
        </svg>
      </button>
      <button class="btn btn-reset btn-icon btn-isEdited btn-edit" @click="handleEdit($event)">
        <svg version="1.1" id="Layer_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px"
            viewBox="0 0 330 330" style="enable-background:new 0 0 330 330;" xml:space="preserve">
            <g id="XMLID_23_">
              <path id="XMLID_24_" d="M75,180v60c0,8.284,6.716,15,15,15h60c3.978,0,7.793-1.581,10.606-4.394l164.999-165
                c5.858-5.858,5.858-15.355,0-21.213l-60-60C262.794,1.581,258.978,0,255,0s-7.794,1.581-10.606,4.394l-165,165
                C76.58,172.206,75,176.022,75,180z M105,186.213L255,36.213L293.787,75l-150,150H105V186.213z"/>
              <path id="XMLID_27_" d="M315,150.001c-8.284,0-15,6.716-15,15V300H30V30H165c8.284,0,15-6.716,15-15s-6.716-15-15-15H15
                C6.716,0,0,6.716,0,15v300c0,8.284,6.716,15,15,15h300c8.284,0,15-6.716,15-15V165.001C330,156.716,323.284,150.001,315,150.001z"
                />
            </g>
        </svg>
      </button>
      <button class="btn btn-reset btn-icon btn-delete" @click="$emit('delete-task', task.id)">
        <svg version="1.1" id="Capa_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px"
          viewBox="0 0 330 330" style="enable-background:new 0 0 330 330;" xml:space="preserve">
          <g>
            <path d="M240,121.076V90h15c8.284,0,15-6.716,15-15s-6.716-15-15-15h-30h-15V15c0-8.284-6.716-15-15-15H75c-8.284,0-15,6.716-15,15
              v45H45H15C6.716,60,0,66.716,0,75s6.716,15,15,15h15v185c0,8.284,6.716,15,15,15h60h37.596c19.246,24.347,49.031,40,82.404,40
              c57.897,0,105-47.103,105-105C330,172.195,290.817,128.377,240,121.076z M90,30h90v30h-15h-60H90V30z M105,260H60V90h15h30h60h30
              h15v31.076c-50.817,7.301-90,51.119-90,103.924c0,12.268,2.122,24.047,6.006,35H105z M225,300c-41.355,0-75-33.645-75-75
              s33.645-75,75-75s75,33.645,75,75S266.355,300,225,300z"/>
            <path d="M256.819,193.181c-5.857-5.857-15.355-5.857-21.213,0L225,203.787l-10.606-10.606c-5.857-5.857-15.355-5.857-21.213,0
              c-5.858,5.857-5.858,15.355,0,21.213L203.787,225l-10.606,10.606c-5.858,5.857-5.858,15.355,0,21.213
              c2.929,2.929,6.768,4.394,10.606,4.394s7.678-1.465,10.606-4.394L225,246.213l10.606,10.606c2.929,2.929,6.768,4.394,10.606,4.394
              s7.678-1.465,10.606-4.394c5.858-5.857,5.858-15.355,0-21.213L246.213,225l10.606-10.606
              C262.678,208.536,262.678,199.038,256.819,193.181z"/>
          </g>
        </svg>
      </button>
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
      const targetParent = ev.target.closest('.main__item');

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
    background-color: rgba(#c408b1, 0.5);
  }
  .btn-save {
    display: none;
  }
  .item__input {
    display: none;
  }
  .item__title {
    display: block;
  }
  .edited > .item__title {
    display: none;
  }
  .checked > .item__title{
    text-decoration: line-through;
    color: gray;
  }
  .main__item {
    cursor: pointer;
  }
  .main__item > p {
    margin:0;
  }
  .dragged {
    background-color: rgba(46,7,245, 0.2);
  }
  
  .btn-icon {
    background-color: linear-gradient(to left bottom, #2e07f5 20%, #c408b1 100%);
    padding: 10px;
  }
  .btn-icon svg {
    width: 20px;
    height: 20px;
  }

  .btn-edit, .btn-save, .btn-delete {
    fill: white;
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
  input[type="checkbox"] {
    display: none;
  }

  label {
    position: relative;
    width: 25px;
    height: 25px;
  }
  label:before {
    content: " ";
    display: inline-block;
    margin-left: 20px;
    width: 25px;
    height: 25px;
    transition: background 0.3s ease;
    border-radius: 5px;
    border: 3px solid #2e07f5;
  }
  input[type="checkbox"]:checked + label:after {
    content: " ";
    position: absolute;
    top: -12px;
    left: 22px;
    width: 25px;
    height: 25px;
    transition: background 0.3s ease;
    background-image: url("../assets/check.svg");
    background-repeat: no-repeat;
    background-position: center center;
    background-size: 25px 25px;
  }
</style>