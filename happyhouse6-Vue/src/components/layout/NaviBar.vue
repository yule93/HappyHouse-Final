<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="info">
      <!-- type="dark" variant="dark" -->
      <b-navbar-brand href="#">
        <router-link :to="{ name: 'Home' }">
          <img
            src="@/assets/noun_House_1.png"
            class="d-inline-block align-middle"
            width="50px"
            alt="Kitten"
            style=""
          />
        </router-link>
      </b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-text-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-item href="#"
            ><router-link tag="li" :to="{ name: 'Home' }" class="link"
              ><b-icon icon="house" font-scale="1"></b-icon> HOME</router-link
            ></b-nav-item
          >
          <b-nav-item href="#"
            ><router-link tag="li" :to="{ name: 'BoardList' }" class="link"
              ><b-icon icon="journal" font-scale="1"></b-icon>
              게시판</router-link
            ></b-nav-item
          >
          <b-nav-item href="#"
            ><router-link tag="li" :to="{ name: 'House' }" class="link"
              ><b-icon icon="house-fill" font-scale="1"></b-icon>
              아파트정보</router-link
            ></b-nav-item
          >
          <b-nav-item href="#"
            ><router-link tag="li" :to="{ name: 'Covid' }" class="link"
              ><b-icon icon="file-earmark-medical-fill" font-scale="1"></b-icon>
              코로나 진료소</router-link
            ></b-nav-item
          >
        </b-navbar-nav>

        <b-navbar-nav
          target="navbar-toggle-collapse"
          class="ml-auto"
          v-if="userInfo"
          style=""
        >
          <b-nav-item class="align-self-center"
            ><b-avatar
              variant="primary"
              v-text="userInfo ? userInfo.userid.charAt(0).toUpperCase() : ''"
              style="width: 30px; height: 30px; margin-right: 10px"
            ></b-avatar
            >{{ userInfo.username }}({{ userInfo.userid }})님
            환영합니다.</b-nav-item
          >
          <b-nav-item class="align-self-center"
            ><router-link
              :to="{ name: 'MyPage' }"
              class="link align-self-center"
              >내정보보기</router-link
            ></b-nav-item
          >
          <b-nav-item
            class="link align-self-center"
            @click.prevent="onClickLogout"
            >로그아웃</b-nav-item
          >
        </b-navbar-nav>
        <b-navbar-nav class="ml-auto" v-else>
          <b-nav-item-dropdown right>
            <template #button-content>
              <b-icon icon="people" font-scale="2"></b-icon>
            </template>
            <b-dropdown-item href="#"
              ><router-link :to="{ name: 'SignUp' }" class="link"
                ><b-icon icon="person-circle"></b-icon> 회원가입</router-link
              ></b-dropdown-item
            >
            <b-dropdown-item href="#"
              ><router-link :to="{ name: 'SignIn' }" class="link"
                ><b-icon icon="key"></b-icon> 로그인</router-link
              ></b-dropdown-item
            >
          </b-nav-item-dropdown>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
import { mapState, mapMutations } from "vuex";

const memberStore = "memberStore";

export default {
  name: "NaviBar",
  computed: {
    ...mapState(memberStore, ["isLogin", "userInfo", "isLogout"]),
  },
  methods: {
    ...mapMutations(memberStore, [
      "SET_IS_LOGIN",
      "SET_USER_INFO",
      "SET_IS_LOGOUT",
    ]),
    onClickLogout() {
      this.SET_IS_LOGIN(false);
      this.SET_USER_INFO(null);
      sessionStorage.removeItem("access-token");
      if (this.$route.path != "/") this.$router.push({ name: "Home" });
    },
  },
};
</script>

<style></style>
