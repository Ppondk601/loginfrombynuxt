<template>
  <div></div>
</template>

<script>
export default {
  data() {
    return {
      formElements: {
        username: {
          type: "text",
          value: "",
          validator: {
            required: true,
            minLength: 5,
            maxLength: 15,
          },
          touched: false,
          error: { status: true, message: "" },
        },
        password: {
          type: "password",
          value: "",
          validator: {
            required: true,
            minLength: 8,
          },
          touched: false,
          error: { status: true, message: "" },
        },
        email: {
          type: "email",
          value: "",
          validator: {
            required: true,
            pattern: "email",
          },
          touch: false,
          error: { status: true, message: "" },
        },
      },
      formValid: false,
    };
  },
  methods: {
    onFormChange(event) {
      const name = event.target.name;
      const value = event.target.value;
      let updatedForm = { ...this.formElements };
      //console.log(updatedForm,name)
      updatedForm[name].value = value;
      updatedForm[name].touched = true;
      const validatorObject = this.checkValidator(
        value,
        updatedForm[name].validator
      );
      updatedForm[name].error = {
        status: validatorObject.status,
        message: validatorObject.message,
      };
      let formStatus = true;
      for (let name in updatedForm) {
        if (updatedForm[name].validator.required === true) {
          formStatus = !updatedForm[name].error.status && formStatus;
        }
      }
      this.formElements = updatedForm;
      this.formValid = formStatus;
    },
    checkValidator(value, rule) {
      let valid = true;
      let message = "";
      if (value.trim().length === 0 && rule.required) {
        valid = false;
        message = "จำเป็นต้องกรอก";
      }
      if (value.length < rule.minLength && valid) {
        valid = false;
        message = `น้อยกว่า ${rule.minLength} ตัวอักษร`;
      }
      if (value.length > rule.maxLength && valid) {
        valid = false;
        message = `มากกว่า ${rule.maxLength} ตัวอักษร`;
      }
      if (rule.pattern === "email" && valid) {
        if (/^w+([.-]?w+)*@w+([.-]?w+)*(.w{2,3})+$/.test(value) === false) {
          valid = false;
          message = "กรอกอีเมลไม่ถูกต้อง";
        }
      }
      return { status: !valid, message: message };
    },
  },
};
</script>

<style lang="scss" scoped></style>
