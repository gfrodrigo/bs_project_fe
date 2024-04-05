<template>
  <form @submit.prevent="handleSubmit">
    <label>Tax ID:</label>
    <input type="text" required v-model="taxId">
    <label>Business name:</label>
    <input type="text" required v-model="businessName">
    <label>Annual revenue:</label>
    <input type="number" required v-model="annualRevenue">
    <label v-if="validateCredit">Credit validation is:</label>
    <input type="text" v-if="validateCredit" v-model="validateCredit" disabled>

    <div class="submit">
      <button v-on:click="handleSubmit()">Validate Credit</button>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      taxId: "",
      businessName: "",
      annualRevenue: "",
      validateCredit: "",
    }
  },
  methods: {
    handleSubmit() {
      this.validateCredit = ""
      const requestOptions = {
        method: "POST",
        headers: {"Content-Type": "application/json"},
        body: JSON.stringify({tax_id: this.taxId, name: this.businessName, annual_revenue: this.annualRevenue})
      };
      fetch("http://localhost:8000/api/validate_credit/", requestOptions)
          .then(response => response.json())
          .then(data => (this.validateCredit = data.data));
    },
  },
}
</script>

<style>
form {
  max-width: 420px;
  margin: 30px auto;
  background: white;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
}

label {
  color: #aaa;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}

input {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555
}

button {
  background: #0b6dff;
  border: 0;
  padding: 10px 20px;
  margin-top: 20px;
  color: white;
  border-radius: 20px;
}

.submit {
  text-align: center;
}

.error {
  color: red;
  margin-top: 10px;
  font-size: 0.8em;
  font-weight: bold;
}
</style>