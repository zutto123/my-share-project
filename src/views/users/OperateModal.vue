<template>
  <div>
    <a-modal
      title="请确认您的操作"
      :visible="visible"
      @ok="handleOk"
      :confirmLoading="confirmLoading"
      @cancel="handleCancel"
    >
      <p>{{ModalText}}</p>
    </a-modal>
  </div>
</template>
<script>
export default {
name: 'OperateModal',
  data() {
    return {
      ModalText: '',
      visible: false,
      confirmLoading: false,
      handleText:''
    }
  },
  methods: {
    open(ModalText, handleText){
        this.visible = true;
        this.ModalText = ModalText;
        this.handleText = handleText;
    },
    close(){
        this.visible = false;
        this.confirmLoading = false;
    },
    handleOk(e) {
      this.ModalText = this.handleText;
      this.confirmLoading = true;
      this.$emit('isok');
    },
    handleCancel(e) {
      this.visible = false
    },
  }
}
</script>