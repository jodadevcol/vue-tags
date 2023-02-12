<script>
import InputTag from './InputTag.vue'

export default { components: { InputTag } }
</script>

<template>
  <aside class="tags-box">
    <h2 class="tags-box--title">Tags</h2>

    <div class="tags-box--wrapper">
      <InputTag />
    </div>
  </aside>
</template>

<style scoped>
.tags-box {
  width: 100%;
  max-width: 400px;
  background-color: var(--color-white);
  padding-block: 4rem;
  padding-inline: 3.2rem;
  border-radius: 8px;
  box-shadow: 0px 0px 20px 1px rgba(40, 75, 99, 0.06);
}

.tags-box--title {
  margin-block-end: 2rem;
  font-size: 2.4rem;
  font-weight: 600;
  color: var(--color-caribbean-current);
}
</style>
