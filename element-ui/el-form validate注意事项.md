# el-form validate 注意事项

## 基本用法

```js
<template>
  <el-form
    ref="ruleFormRef"
    :model="ruleForm"
    :rules="rules"
  >
    <el-form-item label="Activity name" prop="name">
      <el-input v-model="ruleForm.name" />
    </el-form-item>
    <el-form-item label="Activity zone" prop="region">
      <el-select v-model="ruleForm.region" placeholder="Activity zone">
        <el-option label="Zone one" value="shanghai" />
        <el-option label="Zone two" value="beijing" />
      </el-select>
    </el-form-item>
    <el-button @click="save">提交</el-button>
  </el-form>
</template>

<script>
export default {
    data() {
        return {
            ruleForm: {
                name: '',
                region: '',
            },
            rules: {
                name: {
                    required: true,
                    message: '必填字段',
                    trigger: [
                        'blur',
                        'change',
                    ]
                }
            }
        },
    },
    methods: {
    async save() {
        await formEl.validate((valid, fields) => {
            if (valid) {
              console.log('submit!')
            } else {
              console.log('error submit!', fields)
            }
          })
        }
    }
}
</script>
```

## 表单嵌套时，如何检验

### 1、外层表单的 v-model 和 里层表单的 v-model 没有嵌套关系

里层表单重新绑定自己的 ref、model="xxx"、rules。

里层表单的表单项 prop="aa"，表单项里面输入框 v-model="xxx.aa"。

即表单项里面输入框 v-model 的必须是表单 model 的子项。

```js
<el-form
    ref="ruleFormRef"
    :model="ruleForm"
    :rules="rules"
>
    <el-form-item label="Activity name" prop="name">
        <el-input v-model="ruleForm.name" />
    </el-form-item>
    <el-form-item label="嵌套表单">
        <el-form
             ref="newRef",
            :modle="newForm",
            :rules="rules02"
        >
            <el-form-item label="年龄" prop="age">
                <el-input v-model="newForm.age"/>
            </el-form-item>
         <el-form>
     </el-form-item>
</el-form>

<script>
export default {
    data() {
        return {
            ruleForm: {
                name: '',
                region: '',
            },
            newForm: {
                age: '',
            },
            rules: {
                name: {
                    required: true,
                    message: '必填字段',
                    trigger: [
                        'blur',
                        'change',
                    ]
                }
            },
            rules02: {
                age: {
                    required: true,
                    message: '必填字段',
                    trigger: [
                        'blur',
                        'change',
                    ]
                }
            }
        },
    },
    methods: {
    async save() {
        await this.$refs.ruleFormRef.validate((valid, fields) => {
            if (valid) {
              console.log('submit!')
            } else {
              console.log('error submit!', fields)
            }
          })
        }
        await this.$refs.newRef.validate((valid, fields) => {
            if (valid) {
              console.log('submit!')
            } else {
              console.log('error submit!', fields)
            }
          })
        }
    }
}
</script>
```

在验证时，最好在异步函数中进行验证，能够等每个都验证成功后再进行下一步操作（如，保存等）。否则，可能在验证失败的情况下仍然进行了下一步操作（如，验证未通过，却可以保存等）。

### 2、外层表单的 v-model 和 里层表单的 v-model 有嵌套关系

有嵌套关系时，可以不嵌套表单，仅仅是嵌套表单项即可。

在规则设定时，也要嵌套设定规则。

```js
<el-form
    ref="ruleFormRef"
    :model="ruleForm"
    :rules="rules"
>
    <el-form-item label="Activity name" prop="name">
        <el-input v-model="ruleForm.name" />
    </el-form-item>
    <el-form-item
        label="嵌套表单" 
        prop="info"
    >
        <el-form-item label="年龄" prop="age">
            <el-input v-model="ruleForm.info.age"/>
        </el-form-item>
    </el-form-item>
</el-form>

<script>
export default {
    data() {
        return {
            ruleForm: {
                name: '',
                region: '',
            },
            newForm: {
                age: '',
            },
            rules: {
                name: {
                    required: true,
                    message: '必填字段',
                    trigger: [
                        'blur',
                        'change',
                    ]
                },
                info: {
                    age: {
                        required: true,
                        message: '必填字段',
                        trigger: [
                            'blur',
                            'change',
                        ]
                    }
                }
            },
        },
    },
    methods: {
    async save() {
        await formEl.validate((valid, fields) => {
            if (valid) {
              console.log('submit!')
            } else {
              console.log('error submit!', fields)
            }
          })
        }
    }
}
</script>
```
