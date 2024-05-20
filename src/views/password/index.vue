<template>
  <div class="app-container">
    <el-form
      ref="form"
      :model="form"
      :rules="passwordRules"
      label-width="100px"
    >
      <el-form-item label="oldPassword" prop="oldPassword">
        <el-input
          v-model="form.oldPassword"
          type="password"
          placeholder="please input old password"
          style="width: 300px"
        />
      </el-form-item>
      <el-form-item label="newPassword" prop="newPassword">
        <el-input
          v-model="form.newPassword"
          type="password"
          placeholder="please input new password"
          style="width: 300px"
        />
      </el-form-item>
      <el-form-item label="confirmPassword" prop="repeat">
        <el-input
          v-model="form.repeat"
          type="password"
          placeholder="please input new password again"
          style="width: 300px"
        />
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="onSubmit">updatePassword</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import { alterPassword } from '@/api/user'
export default {
  data() {
    const validateRepeat = (rule, value, callback) => {
      if (value !== this.form.newPassword) {
        callback(new Error('confirm password is not same as the new password!'))
      } else {
        callback()
      }
    }
    return {
      form: {
        oldPassword: '',
        newPassword: '',
        repeat: ''
      },
      passwordRules: {
        oldPassword: [
          { required: true, message: 'please input old password', trigger: 'blur' }
        ],
        newPassword: [
          { required: true, message: 'please input new password', trigger: 'blur' }
        ],
        repeat: [
          { required: true, message: 'please input new password again', trigger: 'blur' },
          { trigger: 'blur', validator: validateRepeat }
        ]
      }
    }
  },
  methods: {
    onSubmit() {
      this.$refs.form.validate(valid => {
        if (valid) {
          const isadmin = this.roles[0] === 'admin' ? 1 : 0
          console.log(isadmin)
          alterPassword({ userid: this.id, username: this.name, isadmin: isadmin, oldPassword: this.form.oldPassword, newPassword: this.form.newPassword }).then(res => {
            if(res === 0) this.$message.error('the old password is not correct')
            else this.$message.success('update success')
          })
        } else {
          console.log('submit not allowed!')
          return
        }
      })
      
    }
  },
  computed: {
    // 获得user信息
    ...mapGetters(['id','name','roles']),
  }
}
</script>

<style>
</style>
