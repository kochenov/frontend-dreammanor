<template>
  <transition-group name="fade">
    <div v-if="message" class="flesh info" key="message">
      {{ message }}
    </div>
    <div
      class="flesh error"
      v-if="errorMessage && getType(errorMessage) === 'string'"
      key="error"
    >
      {{ errorMessage }}
    </div>
    <div v-if="getType(errorMessage) === 'object'" key="error-list">
      <div class="flesh error" v-for="key in errorKeys" :key="key">
        <b>{{ titleCase(key) }}</b>
        <ul class="list">
          <li v-for="(item, index) in getErrors(key)" :key="`${index}-error`">
            {{ item }}
          </li>
        </ul>
      </div>
    </div>
  </transition-group>
</template>
<script setup>
import { computed } from "vue";
const props = defineProps({
  message: {
    type: String,
    default: null,
  },
  errorMessage: {
    type: [Object, String],
    default: null,
  },
});
const errorKeys = computed(() => {
  if (!props.errorMessage || getType(props.errorMessage) === "string") {
    return null;
  }
  return Object.keys(props.errorMessage);
});
function getErrors(key) {
  return props.errorMessage[key];
}
function getType(obj) {
  return Object.prototype.toString.call(obj).slice(8, -1).toLowerCase();
}
function titleCase(value) {
  return value.replace("_", " ");
}
</script>
<style lang="scss" scoped>
.flesh {
  padding: 15px 30px;
  border-radius: 3px;
  background-color: #fff;
  margin-bottom: 15px;
}

.error {
  color: red;
  border: 1px solid red;
}

.info {
  color: rgb(0, 132, 255);
  border: 1px solid rgb(0, 132, 255);
}

.alert {
  color: rgb(220, 170, 30);
  border: 1px solid rgb(220, 170, 30);
}

.lite {
  border: none;
  padding: 0px 0px;
  margin-bottom: 5px;
}

.fade-enter-active,
.fade-leave-active {
  transition: all 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translateX(30px);
}

.list {
  padding-left: 20px;
  padding-top: 5px;
}
</style>
