<template>
  <div class="header">
    <div class="header__logo">
      <img src="logo.png" alt="logo">
    </div>
    <nav class="header__nav">
      <span class="header__nav__item">HOME</span>
      <span class="header__nav__item">SHOP</span>
    </nav>
    <div v-if="!checkSign" class="header__registration">
      <vButton :text="sign_up_btn" @click="modalSignUp"/>
      <vButton :text="log_in_btn"/>
    </div>
    <h4 v-if="checkSign">Вы зарегистрированы</h4>
    <modal v-show="isShowModal" :title="titleRegistration" @checkSignUp="checkSignUpModal" @activeModal="modalSignUp"/>
  </div>
</template>

<script>
import VButton from "@/components/vButton.vue";
import Modal from "@/components/modal.vue";

export default {
  name: 'Header',
  components: {Modal, VButton},
  data() {
    return {
      sign_up_btn: 'Sign Up',
      log_in_btn: 'Log In',
      isShowModal: false,
      checkSign: false,
      titleRegistration: 'Registration',
    }
  },
  props: {
    content: {
      type: Array,
      default: () => []
    },
  },
  methods: {
    modalSignUp() {
      this.isShowModal = !this.isShowModal;
      console.log(this.isShowModal)
    },
    checkSignUpModal() {
      this.isShowModal = !this.isShowModal;
      this.checkSign = true;
    }
  },
}
</script>

<style lang="scss" scoped>
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 75px;
  box-shadow: 0 0 15px 0 rgba(0, 0, 0, 0.2);

  &__logo {
    width: 100px;
    height: 100px;

    img {
      width: 100%;
      height: 100%;
    }
  }

  &__nav {
    display: flex;
    gap: 15px;
    font-size: 24px;

    &__item {
      align-self: center;
      transition: all .3s ease-in-out;
      cursor: pointer;

      &:hover {
        color: #2A3C93FF;
        transform: scale(.95);
      }
    }
  }

  &__registration {
    display: flex;
    gap: 15px;
    height: 30px;
    width: 150px;
  }
}


</style>
