<script>
    let email = "";
    let password = "";
    let confirmPassword = "";
    let username = "";
    let isAgreed = false;

    let errors = {
        email: "",
        password: "",
        confirmPassword: "",
        username: "",
    };

    function validateForm() {
        let isValid = true;
        errors = {
            email: "",
            password: "",
            confirmPassword: "",
            username: "",
        };

        if (!email) {
            errors.email = "이메일을 입력해주세요";
            isValid = false;
        } else if (!/\S+@\S+\.\S+/.test(email)) {
            errors.email = "올바른 이메일 형식이 아닙니다";
            isValid = false;
        }

        if (!password) {
            errors.password = "비밀번호를 입력해주세요";
            isValid = false;
        } else if (password.length < 8) {
            errors.password = "비밀번호는 8자 이상이어야 합니다";
            isValid = false;
        }

        if (!confirmPassword) {
            errors.confirmPassword = "비밀번호를 다시 입력해주세요";
            isValid = false;
        } else if (password !== confirmPassword) {
            errors.confirmPassword = "비밀번호가 일치하지 않습니다";
            isValid = false;
        }

        if (!username) {
            errors.username = "사용자 이름을 입력해주세요";
            isValid = false;
        }

        return isValid;
    }

    function handleSubmit() {
        if (validateForm() && isAgreed) {
            // 회원가입 로직 구현
            console.log("회원가입 성공!", { email, password, username });
        }
    }
</script>

<div class="container">
    <div class="signup-box">
        <div class="header">
            <h1>회원가입</h1>
            <p>새로운 계정을 만들어보세요</p>
        </div>

        <form on:submit|preventDefault={handleSubmit}>
            <div class="input-group">
                <label for="username">사용자 이름</label>
                <input
                    type="text"
                    id="username"
                    bind:value={username}
                    class:error={errors.username}
                    placeholder="홍길동"
                />
                {#if errors.username}
                    <span class="error-message">{errors.username}</span>
                {/if}
            </div>

            <div class="input-group">
                <label for="email">이메일</label>
                <input
                    type="email"
                    id="email"
                    bind:value={email}
                    class:error={errors.email}
                    placeholder="example@email.com"
                />
                {#if errors.email}
                    <span class="error-message">{errors.email}</span>
                {/if}
            </div>

            <div class="input-group">
                <label for="password">비밀번호</label>
                <input
                    type="password"
                    id="password"
                    bind:value={password}
                    class:error={errors.password}
                    placeholder="********"
                />
                {#if errors.password}
                    <span class="error-message">{errors.password}</span>
                {/if}
            </div>

            <div class="input-group">
                <label for="confirm-password">비밀번호 확인</label>
                <input
                    type="password"
                    id="confirm-password"
                    bind:value={confirmPassword}
                    class:error={errors.confirmPassword}
                    placeholder="********"
                />
                {#if errors.confirmPassword}
                    <span class="error-message">{errors.confirmPassword}</span>
                {/if}
            </div>

            <div class="agreement">
                <label class="checkbox-container">
                    <input type="checkbox" bind:checked={isAgreed} />
                    <span class="checkmark"></span>
                    <span class="agreement-text">이용약관에 동의합니다</span>
                </label>
            </div>

            <button type="submit" disabled={!isAgreed}>가입하기</button>

            <div class="login-link">
                이미 계정이 있으신가요? <a href="/login">로그인하기</a>
            </div>
        </form>
    </div>
</div>

<style>
    .container {
        min-height: 100vh;
        display: flex;
        justify-content: center;
        align-items: center;
        background-color: #f8f9fa;
        padding: 20px;
    }

    .signup-box {
        background: white;
        padding: 40px;
        border-radius: 20px;
        box-shadow: 0 10px 25px rgba(0, 0, 0, 0.05);
        width: 100%;
        max-width: 480px;
    }

    .header {
        text-align: center;
        margin-bottom: 40px;
    }

    .header h1 {
        color: #ff5757;
        margin: 0;
        font-size: 2.5em;
        font-weight: 700;
    }

    .header p {
        color: #666;
        margin-top: 8px;
    }

    .input-group {
        margin-bottom: 24px;
    }

    label {
        display: block;
        margin-bottom: 8px;
        color: #333;
        font-weight: 500;
    }

    input {
        width: 100%;
        padding: 12px 16px;
        border: 2px solid #e1e1e1;
        border-radius: 10px;
        font-size: 16px;
        transition: all 0.3s ease;
    }

    input:focus {
        outline: none;
        border-color: #ff5757;
        box-shadow: 0 0 0 3px rgba(255, 87, 87, 0.1);
    }

    input.error {
        border-color: #ff5757;
    }

    .error-message {
        color: #ff5757;
        font-size: 14px;
        margin-top: 4px;
        display: block;
    }

    button {
        width: 100%;
        padding: 14px;
        background-color: #ff5757;
        color: white;
        border: none;
        border-radius: 10px;
        font-size: 16px;
        font-weight: 600;
        cursor: pointer;
        transition: all 0.3s ease;
    }

    button:hover {
        background-color: #ff4040;
        transform: translateY(-1px);
    }

    button:disabled {
        background-color: #ccc;
        cursor: not-allowed;
        transform: none;
    }

    .agreement {
        margin: 24px 0;
    }

    .checkbox-container {
        display: flex;
        align-items: center;
        cursor: pointer;
        user-select: none;
    }

    .checkbox-container input {
        width: auto;
        margin-right: 8px;
    }

    .agreement-text {
        color: #666;
    }

    .login-link {
        text-align: center;
        margin-top: 24px;
        color: #666;
    }

    .login-link a {
        color: #ff5757;
        text-decoration: none;
        font-weight: 500;
    }

    .login-link a:hover {
        text-decoration: underline;
    }

    @media (max-width: 480px) {
        .signup-box {
            padding: 20px;
        }

        .header h1 {
            font-size: 2em;
        }
    }
</style>
