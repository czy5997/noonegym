<template>
  <el-dialog v-model="visible" @open="onOpen" @close="onClose" :title="title">
    <el-form ref="elForm" :model="formData" :rules="rules" label-width="100px">
      <el-form-item label="会员手机号" prop="phone">
        <el-input
          v-model="formData.phone"
          placeholder="请输入会员手机号"
          clearable
          :style="{ width: '100%' }"
        >
        </el-input>
      </el-form-item>
      <el-form-item label="渠道来源" prop="registChannel">
        <el-select
          v-model="formData.registChannel"
          placeholder="请选择渠道来源"
          clearable
          :style="{ width: '100%' }"
        >
          <el-option
            v-for="(item, index) in registChannelOptions"
            :key="index"
            :label="item.label"
            :value="item.value"
            :disabled="item.disabled"
          ></el-option>
        </el-select>
      </el-form-item>
      <el-form-item label="责任教练" prop="responsibilityName">
        <el-select
          v-model="formData.responsibilityName"
          placeholder="请选择责任教练"
          :style="{ width: '100%' }"
        >
        </el-select>
      </el-form-item>
      <el-form-item label="会籍顾问" prop="consultantName">
        <el-select
          v-model="formData.consultantName"
          placeholder="请选择会籍顾问"
          :style="{ width: '100%' }"
        >
        </el-select>
      </el-form-item>
      <el-form-item label="所属分销商" prop="other">
        <el-select
          v-model="formData.other"
          placeholder="请选择所属分销商"
          :style="{ width: '100%' }"
        ></el-select>
      </el-form-item>
      <el-form-item label="备注" prop="notes">
        <el-input
          v-model="formData.notes"
          placeholder="请输入备注"
          :style="{ width: '100%' }"
        ></el-input>
      </el-form-item>
      <el-form-item label="状态" prop="enable">
        <el-switch
          v-model="formData.enable"
          :active-value="1"
          :inactive-value="0"
        ></el-switch>
      </el-form-item>
    </el-form>
    <div slot="footer" class="text-right">
      <el-button @click="close">取消</el-button>
      <el-button type="primary" @click="handelConfirm">确定</el-button>
    </div>
  </el-dialog>
</template>
<script>
export default {
  inheritAttrs: false,
  components: {},
  props: {
    title: {
      type: String,
      default: '新增个人会员',
    },
    modelValue: {
      type: Boolean,
      default: false,
    },
  },
  emits: ['update:modelValue', 'confirmUserData'],
  data() {
    return {
      formData: {
        phone: undefined,
        registChannel: undefined,
        responsibilityName: undefined,
        consultantName: undefined,
        other: undefined,
        notes: undefined,
        enable: 1,
      },
      rules: {
        phone: [
          {
            required: true,
            message: '请输入会员手机号',
            trigger: 'blur',
          },
          {
            pattern: /^(?:(?:\+|00)86)?1\d{10}$/,
            message: '请输入正确的手机号',
            trigger: 'blur',
          },
        ],
        registChannel: [
          {
            required: true,
            message: '请选择渠道来源',
            trigger: 'change',
          },
        ],
        responsibilityName: [],
        consultantName: [],
        other: [],
        notes: [],
      },
      registChannelOptions: [
        {
          label: '小程序',
          value: '小程序',
        },
        {
          label: '美团',
          value: '美团',
        },
        {
          label: '地推',
          value: '地推',
        },
        {
          label: '其他',
          value: '其他',
        },
      ],
    }
  },
  computed: {
    visible: {
      get() {
        return this.modelValue
      },
      set(value) {
        this.$emit('update:modelValue', value)
      },
    },
  },
  watch: {},
  created() {},
  mounted() {},
  methods: {
    onOpen() {},
    onClose() {
      this.$refs['elForm'].resetFields()
      //   this.$emit('update:modelValue', false)
    },
    close() {
      this.$emit('update:modelValue', false)
    },
    handelConfirm() {
      this.$refs['elForm'].validate((valid) => {
        if (!valid) return
        // console.log(this.formData)
        this.$emit('confirmUserData', this.formData)
        // this.close()
      })
    },
  },
}
</script>
<style></style>
