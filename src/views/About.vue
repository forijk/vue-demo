<template>
  <a-form :form="form" :label-col="{ span: 5 }" :wrapper-col="{ span: 12 }">
    <a-form-item label="Note">
      <!-- <a-input
        v-decorator="['note', { rules: [{ required: true, message: 'Please input your note!' }] }]"
      /> -->

      <input-tags v-decorator="['note', { rules: [{ required: true, message: 'Please input your note!' }] }]" @input="handleInput"></input-tags>
      
    </a-form-item>
    <a-form-item label="Gender">
      <a-select
        v-decorator="[
          'gender',
          { rules: [{ required: true, message: 'Please select your gender!' }] },
        ]"
        placeholder="Select a option and change input text above"
        @change="handleSelectChange"
      >
        <a-select-option value="male">
          male
        </a-select-option>
        <a-select-option value="female">
          female
        </a-select-option>
      </a-select>
    </a-form-item>
    <a-form-item :wrapper-col="{ span: 12, offset: 5 }">
      <a-button type="primary" html-type="submit" @click.native="handleSubmit">
        Submit
      </a-button>
    </a-form-item>
  </a-form>
</template>

<script>
import InputTags from './components/InputTags'

export default {
  data() {
    return {
      formLayout: 'horizontal',
      form: this.$form.createForm(this, { name: 'coordinated' }),
      arr: []
    };
  },
  components: {
    InputTags
  },
  methods: {
    handleInput(v, isAdd) {
      this.arr = isAdd ? this.arr.concat(v) : this.arr.filter(item => item !==v)
      this.form.setFieldsValue({
        note: this.arr
      });
      console.log(this.arr)
    },
    handleSubmit(e) {
      console.log(1111)
      e.preventDefault();
      this.form.validateFields((err, values) => {
        if (!err) {
          console.log('Received values of form: ', values);
        }
      });
    },
    handleSelectChange(value) {
      console.log(value);
      this.form.setFieldsValue({
        note: ['haha']
      });
    },
  },
};
</script>