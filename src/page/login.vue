<template>
    <div class="login">
        <div class="container">
            <div class="left-banner">
                <h2 class="title">{{photo.copyright}}</h2>
                <img :src="photo.url" alt="">
            </div>
            <div class="right-login">
                <div class="in-or-up">
                    <a :class="type === 'up'? 'active':''" @click="type='up'">Sign Up</a>
                    <a :class="type === 'in'? 'active':''" @click="type='in'">Sign In</a>
                </div>
                <div class="form">
                    <p class="form-type"><span :class="type === 'up'? 'active':''">Sign Up</span> or <span :class="type === 'in'? 'active':''">Sign In</span></p>
                    <div class="username">
                        <h5>Username</h5>
                        <input type="text" name="username" id="username" placeholder="Enter your username">
                    </div>
                    <div class="password">
                        <h5>Password</h5>
                        <input type="password" name="password" id="password" placeholder="******">
                    </div>
                    <div class="email">
                        <h5>E-Mail</h5>
                        <input type="email" name="email" id="email" placeholder="Your e-mail goes here">
                    </div>
                    <div class="agreement">
                        <div :class="agree?'checkbox active':'checkbox'" @click="agree=!agree"></div>
                        <span>I agree all statements in <a href="javascript:;">terms of service</a></span>
                    </div>
                    <div class="button">
                        <button type="button">
                            <span v-if="type==='up'">Sign Up</span>
                            <span v-if="type==='in'">Sign In</span>
                        </button>
                    </div>
                </div>
            </div>
        </div> 
    </div>
</template>

<script>
export default {
    data() {
        return {
            type: "in",
            agree: false,
            photo: {}
        }
    },
    async created() {
        const result = await this.axios.get("https://api.aidioute.cn/photo/getOnePhoto.php")
        if(result.status === 200) {
            this.photo = result.data
        }
    }
}
</script>

<style lang="scss" scoped>
.login {
    width: 100%;
    height: 100%;
    padding: 50px 0 0;
    background-color: #e2dbcc;
    .container {
        width: 1200px;
        height: 800px;
        margin: 0 auto;
        border-radius: 10px;
        display: flex;
        box-shadow: 0 10px 30px rgba(0,0,0,0.2);
        .left-banner {
            flex: 1;
            border-radius: 10px 0 0 10px;
            background-color: #2a9d8f;
            position: relative;
            overflow: hidden;
            .title {
                position: relative;
                z-index: 1;
                padding: 100px;
                text-align: left;
                font-size: 24px;
                color: #ffffff;
            }
            img {
                position: absolute;
                bottom: 0;
                left: 0;
                height: 800px;
                transition: left 4s linear ;
                &:hover {
                    left: -822px;
                }
            }
        }
        .right-login {
            flex: 1;
            border-radius: 0 10px 10px 0;
            position: relative;
            background-color: #264653;
            box-shadow: -10px 0 30px rgba(0,0,0,0.2);
            .in-or-up {
                position: absolute;
                top: 20px;
                right: 36px;
                width: 140px;
                height: 30px;
                line-height: 30px;
                border-radius: 15px;
                text-align: center;
                display: flex;
                overflow: hidden;
                a {
                    flex: 1;
                    color: #7b8897;
                    font-size: 13px;
                    box-sizing: border-box;
                    background-color: #4c5d72;
                    cursor: pointer;
                    transition: all .4s;
                    &.active {
                        color: #ffffff;
                        background: #56c9bb;
                    }
                }
            }
            .form {
                position: absolute;
                top: 100px;
                left: 100px;
                width: 400px;
                .form-type {
                    color: #7b8897;
                    font-size: 24px;
                    span {
                        display: inline-block;
                        height: 60px;
                        line-height: 60px;
                        font-size: 34px;
                        margin: 0 10px;
                        border-bottom: 1px solid transparent;
                        transition: all .4s;
                        &:first-child {
                            margin: 0 10px 0 0;
                        }
                        &.active {
                            color: #ecedf0;
                            border-bottom: 1px solid #56c9bb;
                        }
                    }
                }
                .username, .password, .email {
                    margin-top: 30px;
                    h5 {
                        color: #d7d7d7;
                        font-weight: normal;
                        font-size: 20px;
                        height: 30px;
                        line-height: 30px;
                    }
                    input {
                        width: 100%;
                        height: 50px;
                        line-height: 50px;
                        color: #ffffff;
                        outline: none;
                        border: 0;
                        border-bottom: 2px solid #3e4e62;
                        background: transparent;
                        font-size: 20px;
                        letter-spacing: 1px;
                    }
                }
                .agreement {
                    margin-top: 40px;
                    color: #7b8897;
                    font-size: 14px;
                    .checkbox {
                        display: inline-block;
                        width: 16px;
                        height: 16px;
                        border: 1px solid #7b8897;
                        margin-right: 10px;
                        vertical-align: middle;
                        position: relative;
                        cursor: pointer;
                        transition: all .2s;
                        &.active {
                            background: #14d9b2 url("../assets/image/hook.png") no-repeat center;
                            background-size: 100%;
                        }
                    }
                    span {
                        user-select: none;
                        a {
                            display: inline-block;
                            height: 20px;
                            line-height: 20px;
                            color: #ffffff;
                            border-bottom: 1px solid #2a9d8f;
                        }
                    }
                }
                .button {
                    margin-top: 40px;
                    button {
                        width: 160px;
                        height: 46px;
                        line-height: 46px;
                        outline: none;
                        font-size: 16px;
                        color: #ffffff;
                        background-color: #14d9b2;
                        border: 0;
                        border-radius: 23px;
                        box-shadow: 0 10px 40px 10px rgba(0,0,0,0.2);
                        cursor: pointer;
                    }
                }
            }
        }
    }
}
</style>