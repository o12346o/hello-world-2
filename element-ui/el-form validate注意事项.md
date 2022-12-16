# el-form validate 注意事项

对表单进行验证，未通过验证时，会给出提示。

## 1. 基本用法

### 1.1 使用

1. el-form 设置 `:model="form"`、`:rules="rules"` （rules 是一个对象），

2. el-form-item 设置 `prop="name"`、`required` （required 显示星号，非必要），

3. el-form-item 里的数据项 设置 `v-model="form.name"` 。

```html
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
```

### 1.2 验证

在 data 中添加验证规则对象（也可以直接写在结构中， `rules="{rules:{....}}"` ）。

在 method 中添加验证函数。

```html
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
    async save() { // 保存时进行验证。
        await 表单元素01.validate((valid, fields) => {
            /**
             * 会对表单中所有设置的表单项进行检验，
             * 当所有都检验成功时，才会检验成功。
             */
            if (valid) { // 验证通过，valid 为 true
              console.log('submit!')
            } else { // 验证失败
              console.log('error submit!', fields)
            }
          })
        }
        await 表单元素02.validate(()=>{/* 代码省略 */})
        // 其他表单检验代码
    }
}
</script>
```

## 2. 表单嵌套时，如何检验?

### 2.1 当外层表单的 v-model 和 里层表单的 v-model 没有嵌套关系时

里层表单重新绑定自己的 `ref` 、`:model="xxx"` 、`rules` 。

里层表单的表单项 `prop="aa"` ，表单项里面输入框 `v-model="xxx.aa"` 。

**即:** 表单项里 `v-model` 的必须是表单 `:model` 的子项。

```html
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

在验证时，最好在**异步函数**中进行验证，能够等每个都验证成功后再进行下一步操作（如，保存等）。否则，可能在验证失败的情况下仍然进行了下一步操作（如，验证未通过，却可以保存等）。

### 2.2 当外层表单的 v-model 和 里层表单的 v-model 有嵌套关系时

有嵌套关系时，可以不嵌套表单，仅仅是嵌套表单项即可。

在规则设定时，也要嵌套设定规则。

```html
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
