<template>
  <div class="mydialog"  v-if="isDialogVisible">
    <div class="dialog_mask"></div>
    <div class="dialog_content">
      <div class="dialog_head">
        <slot name="d_head"></slot>
        <span @click="cancel()" class="close"></span>
      </div>
      <div class="dialog_body">
        <slot name="d_body"></slot>
      </div>
      <div class="dialog_footer">
        <button class="btn" @click="submit()">确定</button>
		<button class="btn cancel" @click="cancel()">取消</button>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props:[
            'isDialogVisible'
        ],
  data () {
    return {
		
	}
  },
  methods: {
    cancel () {
	  this.$emit('d_close',false);
    },
	submit (){
	  let data={sub:true}
	  this.$emit('d_submit',data);
	}
  },
  mounted(){
	console.log(this.dialogShow);
  }
}
</script>
<style scoped>
	.btn{
		margin-right: 35px;
		padding: 0;
		width: 80px;
		height: 32px;
		background: #ff9f00;
		border: none;
		color: #fff;
		font-size: 14px;
		border-radius: 4px;
		cursor: pointer;
		float: right;
        margin-right: 15px;
	}
	.btn.cancel{
		background: #fff;
		color: #ff9f00;
		margin-right: 10px;
	}
	
  .dialog_mask{
    display: block;
    position: fixed;
    left: 0;
    top: 0;
	right:0;
	bottom:0;
    background: #000;
    filter: alpha(opacity=20);
    opacity: 0.2;
    z-index: 9;
  }

  .dialog_content{
    display: block;
    width: 600px;
    position: absolute;
    top: 50%;
    left: 50%;
    z-index: 10;
    transform: translate(-50%,-50%);
    box-shadow: 0 0 14px 1px #c6c5c5;
    color: #666;
    border: 1px #d7d7d8 solid;
    background-color: white;
    border-radius: 5px;
    z-index: 10;
  }

  .close{
    width: 15px;
    height: 15px;
    position: absolute;
    top: 10px;
    right: 20px;
    cursor: pointer;
  }
  .close:before, .close:after {
    position: absolute;
    top: 50%;
    width: 15px;
    height: 2px;
    content: '';
    background-color: #e0c09f;
    -webkit-transform: rotate(45deg);
    transform: rotate(45deg);
  }
  .close:after{
    transform: rotate(-45deg);
  }

  .dialog_head{
    position: relative;
    border-bottom: 1px solid #eaeef7;
	height: 35px;
    color: #999;
    background: #f7fafc;
  }
</style>
