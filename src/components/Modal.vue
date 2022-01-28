<template>
  <div class="modal">
    <h1>{{ title }}</h1>
    <p>{{ message }}</p>
    <div class="actions">
      <button name="cancel" @click="handleCancel">
        {{ cancelButtonTitle }}
      </button>
      <button name="confirm" @click="handleConfirm">
        {{ confirmButtonTitle }}
      </button>
    </div>
  </div>
  <div class="backdrop" />
</template>

<script>
export default {
  name: "Modal",
  props: {
    title: String,
    message: String,
    cancelButtonTitle: String,
    confirmButtonTitle: String,
  },
  data() {
    return {};
  },
  methods: {
    handleCancel() {
      this.$emit("cancel");
    },
    handleConfirm() {
      this.$emit("confirm");
    },
  },
};
</script>

<style scoped>
.modal {
  position: fixed;

  top: calc(-50vh - 50%);
  bottom: calc(-50vh - 50%);
  left: calc(-50vw + 50%);
  right: calc(-50vw + 50%);
  margin: auto;
  z-index: 1;

  width: 300px;
  height: min-content;

  display: grid;
  grid-gap: var(--desktop-margin);
  grid-template-rows: min-content 1fr min-content;

  background: var(--neutral-white);
  border-radius: var(--desktop-borderRadius);
  padding: var(--desktop-padding);

  text-align: start;
  color: var(--neutral-grayBlue);
}

.backdrop {
  position: fixed;
  height: 100%;
  width: 100%;
  background-color: rgba(0, 0, 0, 0.4);
}

h1 {
  font-size: 22px;
  color: #333;
}

.actions {
  display: flex;
  justify-content: center;
  gap: var(--desktop-margin);
}

button {
  background: var(--primary-blue);
  color: var(--neutral-white);

  border: 0px;
  border-radius: var(--desktop-borderRadius);
  padding: calc(0.6 * var(--desktop-padding));

  text-transform: uppercase;
  font-weight: bold;

  height: min-content;
}

button[name="cancel"] {
  background: var(--neutral-grayBlue);
}

button[name="confirm"] {
  background: var(--primary-red);
}

button:disabled {
  opacity: 0.5;
  cursor: default;
}

button:disabled:hover {
  filter: none;
}

@media (max-width: 375px) {
}
</style>
