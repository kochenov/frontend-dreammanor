<template>
  <div class="form-input">
    <slot />
  </div>
</template>

<script setup></script>

<style lang="scss" scoped>
.form-input {
  display: flex;
  justify-content: space-between;
  gap: 30px;

  @include screen-size(lg) {
    flex-wrap: wrap;
  }
}
</style>
