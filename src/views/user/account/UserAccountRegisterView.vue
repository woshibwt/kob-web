<template>
    <ContentField>
        注册
    </ContentField>
</template>

<script>
import ContentField from '../../../components/ContentField.vue'
import { useStore } from 'vuex'
import { ref } from 'vue'
import router from '../../../router/index'

export default {
    components: {
        ContentField
    },
    setup() {
        const store = useStore();
        let username = ref('');
        let password = ref('');
        let error_message = ref('');
        //触发函数
        const login = () => {
            error_message.value = "";
            store.dispatch("login", {
                username: username.value,
                password: password.value,
                success() {
                    //成功后跳转到主页面
                    router.push({name: 'home'});
                },
                error() {
                    error_message.value = "用户名或密码错误";
                }

                /*
                success() {
                    //登陆成功后获取用户信息
                    store.dispatch("getinfo", {
                        success() {
                            router.push({ name: 'home' });
                            console.log(store.state.user);
                        }
                    })
                },
                error() {
                    error_message.value = "用户名或密码错误";
                }
                */
            })
        }

        return {
            username,
            password,
            error_message,
            login,
        }
    }
}
</script>

<style scoped>
</style>
