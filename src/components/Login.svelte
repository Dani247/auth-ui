<script>
    let error = "";

    const onSubmit = async (e) => {
        e.preventDefault();
        const [{ value: username }, { value: password }] = e.target;
        const body = {
            username,
            password,
        };
        console.log(body);

        try {
            error = ``;
            const res = await fetch("https://auth.primerocomer.com.mx/login", {
                method: "POST",
                body: JSON.stringify(body),
                headers: {
                    "content-type": "application/json",
                },
            });
            console.log("status", res.status);
            if (res.status === 401) {
                error = `Username not found`;
            }
            if (res.status !== 200) return;
            const data = await res.json();

            // redirect
            const url = new URL(window.location.href);
            const redirect = url.searchParams.get('redirect')
            if (!redirect) return;

            const newUrl = new URL(`${redirect}?access_token=${data.accessToken}`);
            window.location.href = newUrl.href;
        } catch (error) {
            console.log(error);
        }
    };
</script>

<div class="login-container">
    <form on:submit={onSubmit} class="login-form">
        <h2>Login</h2>
        <div class="input-group">
            <label for="username">Username</label>
            <input type="text" id="username" name="username" required />
        </div>
        <div class="input-group">
            <label for="password">Password</label>
            <input type="password" id="password" name="password" required />
        </div>
        <button type="submit">Log In</button>
    </form>
    {#if error}
        <div class="error-container">
            {error}
        </div>
    {/if}
</div>

<style>
    .login-container {
        /* background: white; */
        padding: 20px;
        border-radius: 10px;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    }

    .login-form h2 {
        text-align: center;
        /* color: #333; */
    }

    .input-group {
        margin-bottom: 15px;
        text-align: left;
    }

    .input-group label {
        display: block;
        margin-bottom: 5px;
    }

    .input-group input {
        width: 100%;
        padding: 10px;
        border: 1px solid #ddd;
        border-radius: 5px;
        box-sizing: border-box;
    }

    button {
        width: 100%;
        padding: 10px;
        border: none;
        /* background-color: #5c67a3; */
        color: white;
        border-radius: 5px;
        cursor: pointer;
        font-size: 16px;
    }

    button:hover {
        background-color: #4b5481;
    }

    .error-container {
        color: rgb(255, 153, 0);
        padding: 1rem;
        text-align: center;
    }
</style>
