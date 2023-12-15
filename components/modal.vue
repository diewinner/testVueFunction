<template>
  <transition name="transition_modal">
    <div class="modal_backup" @click="modal">
      <div class="modal_wrapper" @click.stop.prevent="clickInsideModal">
        <div class="title_container">
          <h2 class="title">{{ title }}</h2>
          <div class="btn">
          <vButton  @click="modal" :text="closeTitle"/>
          </div>
        </div>
        <div class="input_container">
          <div class="input_item">
            <div>Login</div>
            <customInput/>
          </div>
          <div class="input_item">
            <div>Password</div>
            <customInput/>
          </div>
        </div>
        <div class="btn">
        <vButton :text="signUp" @click="signUpModal"/>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
import VButton from "@/components/vButton.vue";
import CustomInput from "@/components/customInput.vue";

export default {
  components: {CustomInput, VButton},
  data() {
    return {
      signUp:'Sign Up',
      closeTitle:'close',
    }
  },
  props: {
    close: {
      type: Boolean,
      default: true,
    },
    title: {
      type: String,
      default: ''
    }
  },
  methods: {
    modal() {
      this.$emit('activeModal')
    },
    clickInsideModal(event) {
      event.stopPropagation()
    },
    signUpModal() {
      this.$emit("checkSignUp")
    }
  }
}
</script>

<style lang="scss" scoped>
.modal_backup {
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  top: 0;
  left: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 100vh;
}

.modal_wrapper {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  gap: 25px;
  border: 2px solid #000;
  border-radius: 10px;
  background: #fff;
  padding: 25px 15px;
  min-width: 350px;
  min-height: 250px;
}

.title_container {
  display: flex;
  justify-content: space-between;
  align-items: center;

}

.title {
  align-self: flex-start;
}

.btn {
  max-width: 125px;
  max-height: 25px;
}

.input_container {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.input_item {
  display: flex;
  flex-direction: column;
}




.transition_modal-enter,
.transition_modal-active {
  opacity: 0;
}

.transition_modal-enter-active,
.transition_modal-leave-active {
  transition: opacity .5s linear;
}
</style>
