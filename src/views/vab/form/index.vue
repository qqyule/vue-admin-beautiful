<template>
  <div class="form-container">
    <vab-page-header description="Element UI 表单组件的使用示例，包含验证、重置等功能" :icon="['fas', 'edit']" title="表单组件" />

    <el-row :gutter="20">
      <el-col :lg="8" :md="12" :sm="24" :xl="8" :xs="24">
        <el-form ref="ruleForm" class="demo-ruleForm" label-width="100px" :model="ruleForm" :rules="rules">
          <el-form-item label="活动名称" prop="name">
            <el-input v-model="ruleForm.name" />
          </el-form-item>
          <el-form-item label="活动区域" prop="region">
            <el-select v-model="ruleForm.region" placeholder="请选择活动区域">
              <el-option label="区域一" value="shanghai" />
              <el-option label="区域二" value="beijing" />
            </el-select>
          </el-form-item>
          <el-form-item label="即时配送" prop="delivery">
            <el-switch v-model="ruleForm.delivery" />
          </el-form-item>
          <el-form-item label="活动性质" prop="type">
            <el-checkbox-group v-model="ruleForm.type">
              <el-checkbox label="美食/餐厅线上活动" name="type" />
              <el-checkbox label="地推活动" name="type" />
              <el-checkbox label="线下主题活动" name="type" />
              <el-checkbox label="单纯品牌曝光" name="type" />
            </el-checkbox-group>
          </el-form-item>
          <el-form-item label="特殊资源" prop="resource">
            <el-radio-group v-model="ruleForm.resource">
              <el-radio label="线上品牌商赞助" />
              <el-radio label="线下场地免费" />
            </el-radio-group>
          </el-form-item>
          <el-form-item label="活动形式" prop="desc">
            <el-input v-model="ruleForm.desc" type="textarea" />
          </el-form-item>
          <el-form-item>
            <el-button type="primary" @click="submitForm('ruleForm')">立即创建</el-button>
            <el-button @click="resetForm('ruleForm')">重置</el-button>
          </el-form-item>
        </el-form>
      </el-col>
    </el-row>
  </div>
</template>

<script>
  import VabPageHeader from '@/components/VabPageHeader'

  export default {
    name: 'Form',
    components: {
      VabPageHeader,
    },
    data() {
      return {
        ruleForm: {
          name: '',
          region: '',
          delivery: false,
          type: [],
          resource: '',
          desc: '',
        },
        rules: {
          name: [
            { required: true, message: '请输入活动名称', trigger: 'blur' },
            {
              min: 3,
              max: 5,
              message: '长度在 3 到 5 个字符',
              trigger: 'blur',
            },
          ],
          region: [{ required: true, message: '请选择活动区域', trigger: 'change' }],
          type: [
            {
              type: 'array',
              required: true,
              message: '请至少选择一个活动性质',
              trigger: 'change',
            },
          ],
          resource: [{ required: true, message: '请选择活动资源', trigger: 'change' }],
          desc: [{ required: true, message: '请填写活动形式', trigger: 'blur' }],
        },
      }
    },
    methods: {
      submitForm(formName) {
        this.$refs[formName].validate((valid) => {
          if (valid) {
            alert('submit!')
          } else {
            return false
          }
        })
      },
      resetForm(formName) {
        this.$refs[formName].resetFields()
      },
    },
  }
</script>
