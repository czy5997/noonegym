<template>
  <div class="flex items-center">
    <div
      v-for="(item, key) in filterList"
      :key="key"
      :span="item.span || 5"
      class="mr-[15px]"
    >
      <el-select
        v-if="item.type === 'select'"
        v-model="formData[item.props]"
        :placeholder="item.placeholder || '请选择下拉选择'"
        clearable
        :style="{ width: item.width || '100%' }"
      >
        <el-option
          v-for="(item, index) in item.options"
          :key="index"
          :label="item.label"
          :value="item.value"
          :disabled="item.disabled"
        ></el-option>
      </el-select>

      <el-button
        @click="item.click && item.click(formData)"
        v-if="item.type === 'button'"
        :type="item.btnType"
        :size="item.size || 'default'"
      >
        {{ item.label }}
      </el-button>

      <el-date-picker
        v-if="item.type === 'date'"
        v-model="formData[item.props]"
        format="YYYY-MM-DD"
        :style="{ width: item.width || '100%' }"
        :placeholder="item.placeholder || '请选择日期'"
        clearable
      ></el-date-picker>
      <el-input
        v-if="item.type === 'input'"
        v-model="formData[item.props]"
        :placeholder="item.placeholder || '请输入内容'"
        clearable
        :style="{ width: item.width || '100%' }"
      >
      </el-input>
    </div>
  </div>
</template>
<script>
export default {
  components: {},
  props: {
    filterList: {
      type: Array,
      default: () => [],
    },
    formData: {
      type: Object,
      default: () => {},
    },
  },
  data() {
    return {}
  },

  mounted() {},
  methods: {},
}
</script>
<style></style>
