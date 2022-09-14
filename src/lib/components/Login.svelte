<script>
    import { supabase } from "$lib/supabaseClient";

    let email, password;

    async function login() {
        try {
            const { data, error } = await supabase.auth.signIn({
                email,
                password,
            });
            if (error) throw error;
            console.log("login success\nuser info", data);
        } catch (error) {
            console.log(error);
            alert(error.message);
        }
    }
</script>

<main>
    <div class="container">
        <div class="logo">4JN Inventory System</div>
        <div class="login-item">
            <form on:submit|preventDefault={login} class="form form-login">
                <div class="form-field">
                    <label class="user" for="login-username"><span class="hidden">Username</span></label>
                    <input bind:value={email} type="email" class="form-input" placeholder="Email Address" required>
                </div>
                <div class="form-field">
                    <label class="lock" for="login-password"><span class="hidden">Password</span></label>
                    <input bind:value={password} type="password" class="form-input" placeholder="Password" required>
                </div>
                <div class="form-field">
                    <input type="submit" value="Log in">
                </div>
            </form>
        </div>
    </div>
</main>

<style>
   @import url('https://netdna.bootstrapcdn.com/font-awesome/4.4.0/css/font-awesome.css');
   @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700&display=swap');

   main {
    display: flex;
    margin-top: 175px;
}

.container {
    background: #fff;
    border-radius: 5px;
    box-shadow: 0 1.5px 0 0 rgba(0,0,0,0.1);
    width: 500px;
    height: 380px;
    display: flex;  
    flex-direction: column;
}

.logo{ 
  font-size: 1.5rem;
  font-weight: 600;
  text-align: center;
  padding: 20px 20px 0;
  margin-top: 10px;
}

.login-item {
	padding:25px 25px 0;
	margin: 20px 20px 0;	
	border-radius: 3px;
}

input {
  border: 0;
  color: inherit;
  font: inherit;
  margin: 0;
  outline: 0;
  padding: 0;
  -webkit-transition: background-color .3s;
  transition: background-color .3s;
}

.user:before {
  content: '\f007';
  font: 14px fontawesome;
	color: #5b5b5b;
}

.lock:before {
  content: '\f023';
  font: 14px fontawesome;
	color: #5b5b5b;
}

.form input[type="password"], .form input[type="email"], .form input[type="submit"] {
  width: 100%;
}

.form-login label,
.form-login input[type="email"],
.form-login input[type="password"],
.form-login input[type="submit"] {
  border-radius: 0.25rem;
  padding: 1rem;
  color: #3A3F44;  
}

.form-login label {
  background-color: #222222;
  border-bottom-right-radius: 0;
  border-top-right-radius: 0;
  padding-left: 1.25rem;
  padding-right: 1.25rem;
}

.form-login input[type="email"], .form-login input[type="password"] {
  background-color: #eeeeee;
  border-bottom-left-radius: 0;
  border-top-left-radius: 0;
}
.form-login input[type="email"]:focus, .form-login input[type="email"]:hover, .form-login input[type="password"]:focus, .form-login input[type="password"]:hover {
  background-color: #d6d6d6;
}
.form-login input[type="submit"] {
  background-color: #2196F3;
  color: #eee;
  font-weight: bold;
  text-transform: uppercase;
}
.form-login input[type="submit"]:focus, .form-login input[type="submit"]:hover {
  background-color: #1976D2;
}
.form-field {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  margin-bottom: 2rem;
}
.hidden {
  border: 0;
  clip: rect(0 0 0 0);
  height: 1px;
  margin: -1px;
  overflow: hidden;
  padding: 0;
  position: absolute;
  width: 1px;
}
@media only screen and (max-width: 600px) {
    .container {
        width: 85vw;
    }
}
</style>