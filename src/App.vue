<template>
<div class="container">
  <div v-if="editor">
    <div class="btns">
    <button @click="editor.chain().undo().run()" class="undo__btn">
    </button>
    <button @click="editor.chain().redo().run()" class="redo__btn">
    </button>
    <button @click="editor.chain().setParagraph().run()" :class="{ 'is-active': editor.isActive('paragraph') }" class="lowercase__btn">
    </button>
    <button @click="editor.chain().toggleHeading({ level: 1 }).run()" :class="{ 'is-active': editor.isActive('heading', { level: 1 }) }" class="uppercase__btn">
    </button>
    <button @click="addImage" class="img__btn">
    </button>
    <button @click="copyHTML" class="write-btn">Скопировать HTML</button>
  </div>
  </div>
  <editor-content :editor="editor" />
  </div>
</template>

<script>
import { Editor, EditorContent } from '@tiptap/vue-3'
import StarterKit from '@tiptap/starter-kit'
import Image from '@tiptap/extension-image'
export default {
  components: {
    EditorContent,
  },
  el: '#app',
  data() {
    return {
      editor: null,
      imgUrl: require('./assets/img/image.png')
    }
  },
  methods: {
  addImage() {
      this.imgUrl = prompt('Вставьте URL картинки')
      if (this.imgUrl) {
        this.editor.chain().setImage({ src: this.imgUrl }).run()
      }
    },
      copyHTML () {
      const copyBtn = this.$el.querySelector('.write-btn')
      const copyHTML = document.querySelector('html')

      copyBtn.addEventListener('click', () => {
        const copyText = copyHTML.outerHTML
        navigator.clipboard.writeText(copyText)
      })
      },
  },
  mounted() {
    this.editor = new Editor({
      extensions: [
        StarterKit,
        Image,
      ],
      content: `
        <p>
          Таким образом консультация с широким активом представляет собой интересный эксперимент проверки позиций, занимаемых участниками в отношении поставленных задач. С другой стороны постоянное информационно-пропагандистское обеспечение нашей деятельности представляет собой интересный эксперимент проверки форм развития. Идейные соображения высшего порядка, а также укрепление и развитие структуры влечет за собой процесс внедрения и модернизации соответствующий условий активизации. Задача организации, в особенности же реализация намеченных плановых заданий играет важную роль в формировании дальнейших направлений развития. Повседневная практика показывает, что постоянное информационно-пропагандистское обеспечение нашей деятельности играет важную роль в формировании существенных финансовых и административных условий.
        </p>
        <h1>Смотрите какие обезьянки</h1>

        <img src=${this.imgUrl} />

        <p>
          Таким образом консультация с широким активом представляет собой интересный эксперимент проверки позиций, занимаемых участниками в отношении поставленных задач. С другой стороны постоянное информационно-пропагандистское обеспечение нашей деятельности представляет собой интересный эксперимент проверки форм развития. Идейные соображения высшего порядка, а также укрепление и развитие структуры влечет за собой процесс внедрения и модернизации соответствующий условий активизации. Задача организации, в особенности же реализация намеченных плановых заданий играет важную роль в формировании дальнейших направлений развития. Повседневная практика показывает, что постоянное информационно-пропагандистское обеспечение нашей деятельности играет важную роль в формировании существенных финансовых и административных условий.
        </p>
        <p>
          Товарищи! новая модель организационной деятельности требуют от нас анализа направлений прогрессивного развития. Задача организации, в особенности же постоянный количественный рост и сфера нашей активности требуют от нас анализа позиций, занимаемых участниками в отношении поставленных задач. Задача организации, в особенности же реализация намеченных плановых заданий требуют от нас анализа системы обучения кадров, соответствует насущным потребностям.
        </p>
      `,
    })
  },

  beforeUnmount() {
    this.editor.destroy()
  },
}
</script>

<style lang="scss">
/* Basic editor styles */
.ProseMirror {
  &:focus {
    outline: none;
  }

  & img {
    max-width: 700px;
    width: 100%;
    max-height: 400px;
    object-fit: cover;
  }
}

.container {
    max-width: 780px;
    padding: 15px;

    margin: 0 auto;
}

p {
  font-size: 15px;
  margin: 31px 0px 46px;
}

h1 {
  font-size: 31px;
  margin-bottom: 31px;
}

.undo__btn::before {
  content: url("./assets/icons/undo-icon.svg");
}

.redo__btn::before {
  content: url("./assets/icons/redo-icon.svg");
}


.lowercase__btn::before {
  content: url("./assets/icons/lowercase-icon.svg");
}

.uppercase__btn::before {
  content: url("./assets/icons/uppercase-icon.svg");
}
.img__btn::before {
  content: url("./assets/icons/img-icon.svg");
}

.btns {
  display: flex;
}

.write-btn {
  padding: 0;
  background-color: transparent;
  color:#639EFF;
}
</style>