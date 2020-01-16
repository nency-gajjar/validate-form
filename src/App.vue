<template>
  <div id="app">
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css">
    <div class="container">
      <center><h2>Registration Form</h2></center>
      <br>
      <form @submit.prevent="submitted">
        <div class="form-group row">
          <label for="fname" class="col-sm-2 col-form-label">First Name</label>
          <div class="col-sm-10"> 
            <input type="text" class="form-control" id="fname" name="fname" placeholder="Enter First Name"
            v-model="firstName"
            :class="{ 'has-error': submitting && invalidFirstName }">
            <!-- {{firstName}} -->
          </div>
        </div>
        <div class="form-group row">
          <label for="lname" class="col-sm-2 col-form-label">Last Name</label>
          <div class="col-sm-10">
            <input type="text" class="form-control" id="lname" name="lname" placeholder="Enter Last Name"
            v-model="lastName"
            :class="{'has-error' : submitting && invalidLastName}">
            <!-- {{lastName}} -->
          </div>
        </div>
        <div class="form-group row">
          <label for="uname" class="col-sm-2 col-form-label">User Name</label>
          <div class="col-sm-10">
            <input type="email" class="form-control" id="uname" name="uname" placeholder="Enter User Name"
            v-model="userName"
            :class="{'has-error' : submitting && invalidUserName}">
            <!-- {{userName}} -->
          </div>
        </div>
        <div class="form-group row">
          <label for="email" class="col-sm-2 col-form-label">Email</label>
          <div class="col-sm-10">
            <input type="email" class="form-control" id="email" name="email" placeholder="Enter Email"
            v-model="email"
            :class="{'has-error' : submitting && invalidEmail}">
            <!-- {{email}} -->
          </div>
        </div>
        <div class="form-group row">
          <label for="pwd" class="col-sm-2 col-form-label">Password</label>
          <div class="col-sm-10">
            <input type="password" class="form-control" id="pwd" name="pwd" placeholder="Enter Password"
            v-model="password"
            :class="{'has-error' : submitting && invalidPassword}">
            <!-- {{password}} -->
          </div>
        </div>
        <div class="form-group row">
          <label for="mnum" class="col-sm-2 col-form-label">Mobile Number</label>
          <div class="col-sm-10">
            <input type="number" class="form-control" id="mnum" name="mnum" max="10"  placeholder="Enter Mobile Number"
            v-model="mobileNumber"
            :class="{'has-error' : submitting && invalidNumber}">
            <!-- {{mobileNumber}} -->
          </div>
        </div>
        <p v-if="error && submitting" class="error-message">
          ❗Please fill out all required fields
        </p>
        <p v-if="success" class="success-message">
          ✅ Employee successfully added
        </p>
        <div class="form-group row">
          <div class="col-sm-10">
          <button class="btn-floating  btn-primary">Submit</button>
          </div>
        </div>
        <div class="card" v-if="isSubmitted">   
          <pre><h4><strong>Submitted Data</strong></h4>
  =============================================
              <p>First Name : <b>{{ data.firstName }}</b></p>
              <p>Last Name : <b>{{ data.lastName }}</b></p>
              <p>User Name : <b>{{ data.userName }}</b></p>
              <p>Email : <b>{{ data.email }}</b></p>
              <p>Mobile Number : <b>{{ data.mobileNumber }}</b></p>
          </pre>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name : "#app",
  data(){
    return {
      firstName: null,
      lastName: null,
      userName : null,
      email : null,
      password : null,
      mobileNumber : null,
      data:{
        'firstName': null,
        'lastName': null,
        'userName' : null,
        'email' : null,
        'password' : null,
        'mobileNumber' :null,
      },
      isSubmitted : false ,
      submitting : false,
      success : false,
      error : false
    }
  },
  
  methods: {
        submitted() {
            this.submitting = true
            if (this.invalidFirstName || this.invalidLastName
            || this.invalidUserName
            || this.invalidEmail
            || this.invalidPassword
            || this.invalidNumber){
                this.error = true
                return
            }
          
            this.error = false
            this.success = true
            //this.submitting = false
            this.isSubmitted = true
            this.data = {
              'firstName' : this.firstName,
              'lastName' : this.lastName,
              'password' : this.password,
              'userName' : this.userName,
              'email' : this.email,
              'mobileNumber' : this.mobileNumber
            }
        },
    },

    computed: {
    invalidFirstName() {
        return this.firstName === null
    },
    invalidLastName() {
        return this.lastName === null
    },  
    invalidUserName() {
        return this.userName === null
    }, 
    invalidEmail() {
        return this.email === null
    }, 
    invalidPassword() {
        return this.password === null
    }, 
    invalidNumber() {
        return this.mobileNumber === null
    }, 

    },
    
    isValid(){
      if(!this.firstName || !this.lastName || !this.password
        || !this.userName || !this.mobileNumber || !this.email) {
          return true
        }
        return false  
    },
    
    submitted(){
      //this.isSubmitted = false

      if (this.isValid()){
              this.error = true
              this.submitting =false
              this.isSubmitted = false
              return
        }else{
          this.isSubmitted = true
          this.data = {
            'firstName' : this.firstName,
            'lastName' : this.lastName,
            'password' : this.password,
            'userName' : this.userName,
            'email' : this.email,
            'mobileNumber' : this.mobileNumber
          }
        }
        this.error = false
        this.success = true
        this.submitting = true 
        
    },
  
}
</script>

<style scoped>
body{
  margin : 0;  
}

.error-message {
    color: #d33c40;
}

.has-error {
  border-color: #d33c40 ;
}
.success-message {
    color: #32a95d;
}  
  
</style>