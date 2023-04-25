<template>
  <div>
    <div ref="source">This is the source element.</div>
    <div ref="target"></div>
    <button @click="copyAndPaste">Copy and paste</button>
  </div>
</template>

<script>
export default {
  methods: {
    copyAndPaste() {
      const sourceElement = this.$refs.source;
      const targetElement = this.$refs.target;
      const newDiv = document.createElement("div");
      newDiv.innerHTML = sourceElement.innerHTML;
      targetElement.appendChild(newDiv);
    },
  },
};
</script>
