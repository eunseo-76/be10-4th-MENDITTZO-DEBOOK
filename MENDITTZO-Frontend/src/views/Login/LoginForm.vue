<script setup>
import ButtonLong from "@/components/common/ButtonLong.vue";
import axios from "axios";
import {useAuthStore} from "@/store/auth.js";
import router from "@/router/router.js";
import {useRouter} from "vue-router";
import {onMounted} from "vue";

const authStore = useAuthStore();

// 로그인 버튼 누르면 서버에서 로그인 url을 가져온다.
const handleKakaoLogin = async () => {

  console.log("handleKakaoLogin 함수 호출");

  try {
    console.log("백엔드 서버에서 카카오 로그인 url 가져오기 시작");
    // 백엔드 서버에서 카카오 로그인 URL 가져오기
    const response = await axios.get("http://localhost:8080/api/v1/public/auth/kakao-url");
    console.log("api 응답 - response.data : ", response.data);

    const loginUrl = response.data.kakaoLoginUrl;

    console.log("카카오 로그인 url: ", loginUrl);

    window.location.href = loginUrl;

  } catch (error) {
    console.error(('카카오 로그인 url 가져오기 실패'), error);
  }
};


</script>

<template>
  <div class="login-container">
    <div class="login-form">
      <!-- 설명 -->
      <div class="text">
        <h1>SNS 간편 로그인</h1>
        <div class="text-sub">
          <img src="@/assets/image/info-icon.png" alt="경고 이미지">
          <a>SNS 간편 로그인을 통해 회원가입 할 수 있습니다!</a>
        </div>
      </div>

      <!-- 로그인 버튼 -->
      <div class="login-buttons">
        <ButtonLong class="kakao" @click="handleKakaoLogin" >
          <img src="@/assets/image/kakao-logo.png" alt="카카오 로그인">
          카카오 로그인
        </ButtonLong>

      </div>
      <!-- 설명 -->
      <div class="text">
        <a>공용 PC 및 기기에서는 소셜로그인 이용 후 개인정보 유출방지를 위해 소셜 사이트(네이버, 구글, 카카오)에서 로그아웃을 반드시 해 주세요.</a>
      </div>
    </div>
  </div>

</template>

<style scoped>
.login-container{
  display: flex;
  align-items: center; /* 수직 중앙 정렬 */
  justify-content: center; /* 수평 중앙 정렬 */
  width: 950px;
  height: 400px;
  margin: 50px auto;
  padding: 20px 40px;
  border-radius: 10px;
  box-shadow: 0 8px 24px 0 rgba(149, 157, 165, 0.2);
  background-color: #fff;
}
/* login-container 안에서 login-form을 중앙 정렬 */
.login-form {
  padding: 0 10px 10px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100%;                /* login-container 내의 여백 설정 */
  height: auto;
  padding: 10px;
  text-align: center;
}

/* 버튼 이미지, 텍스트 중간 정렬 */
.kakao{
  display: flex;
  align-items: center;
  gap: 5px;
  cursor: pointer;
  margin-bottom: 50px;
}

/* 로그인 버튼 간 세로 간격 */
.login-buttons{
  display: flex;
  flex-direction: column;
  gap: 10px;
}

/* 각 버튼 속성 */
.kakao{
  background-color: #FEE500;
}

/* 텍스트, 아이콘 중간 정렬 */
.text-sub{
  display: flex;
  align-items: center;
  gap: 2px;
}

/* 버튼, 텍스트 간격 설정 */
.text-sub{
  margin-bottom: 50px;
}
.text{
  margin-top: 0px;
}

/* 텍스트 속성 */
.text a{
  font-size: 15px;
  color: #888888;
}

h1{
  font-size: 40px;
  font-weight: bold;
  margin-top: 0;
}


</style>