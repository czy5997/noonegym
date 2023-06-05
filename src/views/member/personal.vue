<template>
  <div>
    <el-form
      ref="elForm"
      :model="formData"
      :rules="rules"
      size="medium"
      label-width="100px"
    >
      <el-row type="flex" justify="start" align="top">
        <el-col :span="11">
          <el-form-item label="下拉选择" prop="field108">
            <el-select
              v-model="formData.field108"
              placeholder="请选择下拉选择"
              clearable
              :style="{ width: '100%' }"
            >
              <el-option
                v-for="(item, index) in field108Options"
                :key="index"
                :label="item.label"
                :value="item.value"
                :disabled="item.disabled"
              ></el-option>
            </el-select>
          </el-form-item>
        </el-col>
        <el-form-item label="日期选择" prop="field112">
          <el-date-picker
            v-model="formData.field112"
            format="yyyy-MM-dd"
            value-format="yyyy-MM-dd"
            :style="{ width: '100%' }"
            placeholder="请选择日期选择"
            clearable
          ></el-date-picker>
        </el-form-item>
        <el-form-item label="单行文本" prop="field110">
          <el-input
            v-model="formData.field110"
            placeholder="请输入单行文本"
            clearable
            :style="{ width: '100%' }"
          >
          </el-input>
        </el-form-item>
      </el-row>
      <el-form-item size="large">
        <el-button type="primary" @click="submitForm">提交</el-button>
        <el-button @click="resetForm">重置</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>
<script>
export default {
  components: {},
  props: [],
  data() {
    return {
      formData: {
        field108: undefined,
        field112: null,
        field110: undefined,
      },
      rules: {
        field108: [
          {
            required: true,
            message: '请选择下拉选择',
            trigger: 'change',
          },
        ],
        field112: [
          {
            required: true,
            message: '请选择日期选择',
            trigger: 'change',
          },
        ],
        field110: [
          {
            required: true,
            message: '请输入单行文本',
            trigger: 'blur',
          },
        ],
      },
      field108Options: [
        {
          label: '选项一',
          value: 1,
        },
        {
          label: '选项二',
          value: 2,
        },
      ],
    }
  },
  computed: {},
  watch: {},
  created() {},
  mounted() {},
  methods: {
    submitForm() {
      this.$refs['elForm'].validate((valid) => {
        if (!valid) return
        // TODO 提交表单
      })
    },
    resetForm() {
      this.$refs['elForm'].resetFields()
    },
  },
}
</script>
<style></style>
