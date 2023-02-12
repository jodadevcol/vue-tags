<script>
import TagIcon from './icons/IconTag.vue'
import RemoveTagIcon from './icons/IconRemoveTag.vue'

export default {
  data() {
    return {
      currentValue: '',
      tags: ['React', 'Vue', 'DevOps']
    }
  },
  methods: {
    handleKeyDown(event) {
      if (event.key === 'Backspace' && this.currentValue === '') {
        this.tags.pop()
      }
    },
    handleSubmit() {
      if (this.currentValue !== '') {
        const existTag = this.tags.some((item) => item === this.currentValue)

        if (!existTag) {
          this.tags.push(this.currentValue)
          this.currentValue = ''
        }
      }
    },
    deleteTag(tag) {
      this.tags = this.tags.filter((item) => item !== tag)
    }
  },
  components: { TagIcon, RemoveTagIcon }
}
</script>

<template>
  <div class="input-tag">
    <form class="input-tag--form form-tags" @submit.prevent="handleSubmit">
      <label class="form-tags--field field-text" for="tags">
        <span class="field-text--icon">
          <TagIcon />
        </span>
        <input class="field-text--input" type="text" v-model="currentValue" name="tags" id="tags" placeholder="Add a tag..." @keydown="handleKeyDown" />
      </label>
    </form>

    <div class="input-tag--tags">
      <div class="input-tag--tag tag-box" v-for="(tag, index) in tags" :key="index">
        <span class="tag-box--label">{{ tag }}</span>
        <button class="tag-box--remove" @click="deleteTag(tag)">
          <span><RemoveTagIcon /></span>
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.form-tags--field {
  position: relative;
  display: block;
  width: 100%;
  max-width: 100%;
  color: var(--color-jet);
}

.field-text--icon {
  position: absolute;
  top: 50%;
  left: 8px;
  display: block;
  width: 16px;
  height: 20px;
  transform: translateY(-50%);
  z-index: 10;
}

.field-text--icon svg {
  width: 100%;
  height: 100%;
  opacity: 0.7;
}

.field-text--input {
  width: 100%;
  min-height: 44px;
  padding-block: 0.8rem;
  padding-inline: 2.8rem 1.2rem;
  z-index: 0;
  outline: none;
  border: 1px solid rgb(217, 217, 217, 0.8);
  border-radius: 4px;
}

.field-text--input:focus {
  outline: 1px solid rgb(217, 217, 217, 1);
}

.input-tag--tags {
  display: flex;
  flex-wrap: wrap;
  column-gap: 0.8rem;
  row-gap: 1.2rem;
  margin-block-start: 1.6rem;
}

.input-tag--tag {
  padding-block: 0.4rem;
  padding-inline: 1.2rem;
  font-size: 1.4rem;
  color: var(--color-indigo-dye);
}

.tag-box {
  display: flex;
  align-items: center;
  justify-content: center;
  column-gap: 0.8rem;
  outline: none;
  border: 2px solid rgba(40, 75, 99, 0.4);
  border-radius: 8px;
  cursor: grab;
  will-change: auto;
  transition: border-color 240ms linear;
}

.tag-box:hover {
  border-color: rgba(40, 75, 99, 0.8);
}

.tag-box .tag-box--label {
  font-size: inherit;
  pointer-events: none;
}

.tag-box .tag-box--remove {
  color: var(--color-indigo-dye);
  outline: none;
  border: none;
  background-color: transparent;
  cursor: pointer;
}

.tag-box .tag-box--remove span {
  display: block;
  width: 16px;
  height: 20px;
}

.tag-box .tag-box--remove svg {
  width: 100%;
  height: 100%;
  opacity: 0.5;
  will-change: auto;
  transition: opacity 200ms linear;
}

.tag-box .tag-box--remove:hover svg {
  opacity: 1;
}
</style>
