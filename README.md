# Oggy-project
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Login with Effects</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: Arial, sans-serif;
        }

        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            overflow: hidden;
            background: linear-gradient(45deg, rgba(255, 0, 255, 0.8), rgba(0, 255, 255, 0.553));
            position: relative;
            transition: background 1s ease-in-out;
        }

        /* Expanding Black Blur Effect */
        .black-blur-effect {
            position: absolute;
            top: 50%;
            left: 50%;
            width: 0;
            height: 0;
            background: rgba(0, 0, 0, 0.9);
            backdrop-filter: blur(0px);
            opacity: 0;
            transform: translate(-50%, -50%);
            transition: width 3s ease-out, height 3s ease-out, opacity 3s ease-out, backdrop-filter 3s ease-out;
            border-radius: 50%;
            z-index: 2;
        }

        .blur-transparent-div {
            position: relative;
            width: 400px;
            padding: 30px;
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(20px);
            border: 2px solid rgba(255, 255, 255, 0.2);
            border-radius: 12px;
            text-align: center;
            color: white;
            box-shadow: 0 0 15px rgba(255, 255, 255, 0.1);
            z-index: 3;
            transition: opacity 1.5s ease-out;
        }

        .blur-transparent-div h2 {
            margin-bottom: 20px;
            font-size: 24px;
        }

        .input-group {
            margin-bottom: 20px;
            position: relative;
        }

        .input-group input {
            width: 100%;
            padding: 12px;
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            border: 2px solid transparent;
            border-radius: 8px;
            font-size: 16px;
            color: white;
            transition: 0.4s ease-in-out;
            text-align: center;
            outline: none;
        }

        .input-group input::placeholder {
            color: rgba(255, 255, 255, 0.7);
        }

        /* Glow Effect on Hover & Focus */
        .input-group input:hover,
        .input-group input:focus {
            border-color: rgba(0, 255, 255, 0.8);
            box-shadow: 0 0 10px rgba(0, 255, 255, 0.8), 
                        0 0 20px rgba(255, 0, 255, 0.8);
        }

        .error-text {
            color: rgb(255, 0, 0);
            font-size: 14px;
            margin-top: 5px;
            opacity: 0;
            transition: opacity 0.5s ease-in-out;
        }

        .error-border {
            border-color: rgb(255, 0, 0) !important;
            box-shadow: 0 0 10px rgb(255, 0, 0);
        }

        .login-btn {
            width: 100%;
            padding: 12px;
            background: linear-gradient(90deg, rgba(255, 0, 255, 0.8), rgba(0, 255, 255, 0.8));
            border: none;
            border-radius: 8px;
            font-size: 18px;
            color: white;
            cursor: pointer;
            transition: 0.3s ease-in-out;
        }

        .login-btn:hover {
            box-shadow: 0 0 15px rgba(255, 0, 255, 0.8), 
                        0 0 30px rgba(0, 255, 255, 0.8);
            transform: scale(1.05);
        }

        /* Blood Effect */
        .blood-background {
            background: linear-gradient(45deg, black, darkred, black) !important;
        }
    </style>
</head>
<body>

    <!-- Expanding Black Blur Effect -->
    <div class="black-blur-effect" id="black-blur"></div>

    <div class="blur-transparent-div" id="login-box">
        <h2>Login</h2>
        <div class="input-group">
            <input type="email" id="email" placeholder="Email">
            <p class="error-text" id="email-error">Empty Email</p>
        </div>
        <div class="input-group">
            <input type="password" id="password" placeholder="Password">
            <p class="error-text" id="password-error">Empty Password</p>
        </div>
        <button class="login-btn" onclick="validateAndLogin()">Login</button>
    </div>

    <script>
        function validateAndLogin() {
            const email = document.getElementById('email');
            const password = document.getElementById('password');
            const emailError = document.getElementById('email-error');
            const passwordError = document.getElementById('password-error');
            const blackBlur = document.getElementById('black-blur');
            const loginBox = document.getElementById('login-box');
            const body = document.body;

            let hasError = false;

            // Reset styles
            email.classList.remove('error-border');
            password.classList.remove('error-border');
            emailError.style.opacity = "0";
            passwordError.style.opacity = "0";
            body.classList.remove('blood-background');

            // Check if inputs are empty
            if (email.value.trim() === "") {
                email.classList.add('error-border');
                emailError.style.opacity = "1";
                hasError = true;
            }
            if (password.value.trim() === "") {
                password.classList.add('error-border');
                passwordError.style.opacity = "1";
                hasError = true;
            }

            // If there's an error, apply the blood background
            if (hasError) {
                body.classList.add('blood-background');
                return;
            }

            // If inputs are filled, start the black blur effect
            blackBlur.style.width = "5000px";
            blackBlur.style.height = "5000px";
            blackBlur.style.opacity = "1";
            blackBlur.style.backdropFilter = "blur(30px)";

            // Fade out and remove login box after 1.5s
            setTimeout(() => {
                loginBox.style.opacity = "0";
                setTimeout(() => {
                    loginBox.remove();
                }, 1500);
            }, 1500);
        }
    </script>

</body>
</html>
