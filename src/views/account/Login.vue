<script setup>
import { Form, Field } from 'vee-validate';
import * as Yup from 'yup';
import { useAuthStore } from '@/stores';
import { NImage } from 'naive-ui';

const schema = Yup.object().shape({
    username: Yup.string().required('帳號不能為空！'),
    password: Yup.string().required('密碼不能為空！')
});

async function onSubmit(values) {
    const authStore = useAuthStore();
    const { username, password } = values;
    await authStore.login(username, password);
}
</script>

<template>
    <div class="card m-3">
        <n-image height="120" width="500" src="https://i.imgur.com/VVLoUqg.png"/>
        <div class="card-body">
            <h4 class="card-header">登入Herstory27</h4>
            <Form @submit="onSubmit" :validation-schema="schema" v-slot="{ errors, isSubmitting }">
                <div class="form-group">
                    <label>Account</label>
                    <Field name="username" type="text" class="form-control" :class="{ 'is-invalid': errors.username }" />
                    <div class="invalid-feedback">{{ errors.username }}</div>
                </div>
                <div class="form-group">
                    <label>Password</label>
                    <Field name="password" type="password" class="form-control" :class="{ 'is-invalid': errors.password }" />
                    <div class="invalid-feedback">{{ errors.password }}</div>
                </div>
                <div class="form-group">
                    <button class="btn subbtn" :disabled="isSubmitting">
                        <div>
                            <span v-show="isSubmitting" class="spinner-border"></span>
                        </div>
                        Login
                    </button>  
                    <router-link to="register" class="btn btn-link">Register</router-link>
                </div>
            </Form>
        </div>
    </div>
</template>

<style>
    .card {
        width: 500px;
        margin: 0 auto;
    }
    .card-header {
        text-align: center;
        background: #ffffff;
    } 
    .form-group {
        margin: 0 auto;
        width: 100%;
        padding: 2vw;
    }
    .n-image {
        width: 100%;
        height: 50%; /* To maintain the aspect ratio of the image */
    }
    .label {
        font-size: 20px;
    }
    .btn.subbtn {
        width: 100%;
        height: 100%;
        background: #800000;
        color: #ffffff;
        border-radius: 20px;
        display: flex;
        justify-content: center; /* 水平置中 */
        align-items: center; /* 垂直置中 */
    }

    .btn-link {
        color: #800000;
        display: block;
        text-align: center;
    }
    

</style>
