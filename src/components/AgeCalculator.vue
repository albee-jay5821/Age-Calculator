<template>
  <body>
      <div class="container">
      <div class="input-flex">
          <div class="input-container">
              <span>Day</span>
              <input type="number" id="day" placeholder="DD" @input="validateDay" v-model="dayInput">
              <small class="error-day" >{{ errorDay }}</small>
          </div>
          <div class="input-container">
              <span>Month</span>
              <input type="number" id="month" placeholder="MM" @input="validateMonth" v-model="monthInput">
              <small class="error-month">{{ errorMonth }}</small>
          </div>
          <div class="input-container">
              <span>Year</span>
              <input type="number" id="year" placeholder="YYYY" @input="validateYear" v-model="yearInput">
              <small class="error-year">{{ errorYear }}</small>
          </div>
      </div>
      <button class="submit" @click="calculateDate">
          <img src="./icon-arrow.svg" alt="">
      </button>
      <div class="output">
          <h1><span class="output-year" >{{ outputYear ?outputYear:'- -'}}</span> years</h1>
          <h1><span class="output-month">{{ outputMonth ?outputMonth:'- -'}}</span> months</h1>
          <h1><span class="output-day">{{ outputDay ?outputDay:'- -'}}</span> days</h1>
      </div>
      </div>
  </body>
</template>
<script>
import { ref,watch  } from 'vue';
export default {
setup() {
  const errorDay = ref("");
  const errorMonth = ref("");
  const errorYear = ref("");
  const inputDay = ref("");
  const inputMonth = ref("");
  const inputYear = ref("");
  const outputDay = ref("");
  const outputMonth = ref("");
  const outputYear = ref("");
  let isValid = ref(false);
  const dayInput = ref('');
  let day
  let month
  let year
  const monthInput = ref('');
  const yearInput = ref('');
  const handleDay = (dayValue) => {
      console.log("tags: ",dayValue)
    if (dayValue > 31) {
      errorDay.value = "Must be a valid date";
      isValid.value = false;
      return;
    } else {
      isValid.value = true;
      errorDay.value = "";
    }
    if (dayValue === 0) {
      errorDay.value = "This field is required";
      isValid.value = false;
      return;
    } else {
      errorDay.value = "";
      day= dayValue
    }
  };
  const handleMonth = (monthValue) => {
    console.log("tags: ",monthValue)
    if (monthValue > 12) {
      errorMonth.value = "Must be a valid month";
      isValid.value = false;
      return;
    } else {
      isValid.value = true;
      errorMonth.value = "";
    }
    if (monthValue === 0) {
      errorMonth.value = "Month can bot be 0";
      isValid.value = false;
      return;
    } else {
      errorMonth.value = "";
      month= monthValue
    }
 
  };
  const handleYear = (yearValue) => {
    console.log("tags: ",yearValue)
    if (yearValue > 2023) {
      errorYear.value = "Year out of range";
      isValid.value = false;
      return;
    } else {
      isValid.value = true;
      errorYear.value = "";
    }
    if (yearValue === 0) {
      errorYear.value = "Year can not be 0";
      isValid.value = false;
      return;
    } else {
      errorYear.value = "";
      year=yearValue
    }

  };
  watch(dayInput, handleDay);
  watch(monthInput, handleMonth);
  watch(yearInput, handleYear);
  function validateDay() {

  }
  function validateMonth() {

  }
  function validateYear() {

  }
  function calculateDate() {
    if (isValid.value) {
      let birthday = `${month}/${day}/${year}`;
      console.log(birthday, " :hgjgj")
      let birthdayObj = new Date(birthday);
      let ageDiffMill = Date.now() - birthdayObj;
      let ageDate = new Date(ageDiffMill);
      let ageYears = ageDate.getUTCFullYear() - 1970;
      let ageMonth = ageDate.getUTCMonth();
      let ageDay = ageDate.getUTCDay();
      outputDay.value = ageDay;
      outputMonth.value = ageMonth;
      outputYear.value = ageYears;
    } else {
      alert("Error");
    }
  }
  return {
    errorDay,
    errorMonth,
    errorYear,
    inputDay,
    inputMonth,
    inputYear,
    outputDay,
    outputMonth,
    outputYear,
    validateDay,
    validateMonth,
    validateYear,
    calculateDate,
    dayInput,
    monthInput,
    yearInput
  };
},
};
</script>
<style scoped>

* {
  font-family: 'Poppins', sans-serif;
}
body {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background-color: hsl(0, 0%, 94%);
}
.container {
  background-color: hsl(0, 0%, 100%);
  width: 550px;
  max-width: 80%;
  padding: 30px;
  position: relative;
  border-bottom-right-radius: 120px;
}
input {
  width: 120px;
  padding: 15px;
  font-size: 20px;
  border-radius: 5px;
  border: 3px solid hsl(0, 0%, 94%);
  outline: none;
}
input:focus {
  border: 3px solid hsl(259, 100%, 65%);
}
small {
  color: red;
  font-size: 0.6rem;
  font-weight: bold;
  text-transform: capitalize;
}
.submit {
  width: 70px;
  height: 70px;
  padding: 20px;
  display: flex;
  background-color: hsl(259, 100%, 65%);
  justify-content: center;
  align-items: center;
  border: none;
  border-radius: 50%;
  position: absolute;
  right: 30px;
  top: 130px;
}
.submit:hover {
  background-color: black;
}
.input-container {
  display: flex;
  flex-direction: column;
  margin-left: 20px;
  margin-bottom: 10px;
}
.input-flex {
  display: flex;
  border-bottom: 2px solid hsl(0, 0%, 94%);
  margin-bottom: 20px;
}
.output span {
  font-size: 60px;
  color: hsl(259, 100%, 65%);
  font-style: italic;

}
.output {
  font-size: 32px;
  margin: auto auto;
}
@media (max-width: 900px)  {
  input {
      width: 80%;
  }
  .output h1{
    font-size: xx-large;
  }
  .submit {
      width: 40px;
      height: 40px;
      right: 40%;
      top: 120px;
  }
  .submit img {
      transform: scale(0.5);
  }
}
</style>