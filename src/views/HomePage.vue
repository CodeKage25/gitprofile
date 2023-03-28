<template>
  <div>
    <Layout />
    <div class="mt-[3rem] max-md:mt-[10rem] hero-con">
      <div class="flex flex-row items-center justify-between">
        <div>
          <h1 class="front-page-heading tracking-tighter">Frontend</h1>
          <h1 class="front-page-heading tracking-tighter">Developer</h1>
        </div>

        <div class="img-and-bg-container">
          <img :src="this.displayImage" alt="User Image" class="user-img" />
          <div class="img-bg"></div>
        </div>
      </div>
    </div>
    <div class="grid grid-cols-[1fr,0.3fr] mt-[4rem] max-md:block">
      <!-- <SmallText
        className="w-[70%] max-md:w-full max-md:text-[1.4rem] mb-[2rem] leading-[2.4rem]"
        text="Details About You"
      /> -->
      <p>{{this.bio}}</p>

      <div class="socials">
        <SmallText
          text="Let's get connected"
          className="border-slate-400 text-[1.4rem] border-b-[1px] py-[.4rem] my-[.6rem] text-slate-400"
        />
        <Link className="" title="Resume" link="" /><br />
        <Link title="Portfolio" link="" /><br />
        <Link title="LinkedIn" link="www.linkedin.com/in/" /><br />
        <Link title="Github" link="github.com/" /><br />
      </div>
    </div>
    <div class="max:md-block mb-[4rem]">
      <Btn
        className="bg-black mr-[.6rem] hover:bg-slate-700"
        text="Hit me up"
      />
      <router-link to="/repositories"
        ><Btn
          className="bg-slate-700 hover:bg-black"
          link="/repositories"
          text="Repositories"
      /></router-link>
    </div>
  </div>
</template>

<script>
import Layout from "../components/Layout.vue";
import Paragraph from "@/components/typography/Paragraph.vue";
import SmallText from "@/components/typography/SmallText.vue";
import Btn from "@/components/Button.vue";
// import SmallTextVue
import Link from "../components/Links.vue";

export default {
  name: "HomePage",
  components: {
    Layout,
    Paragraph,
    Link,
    SmallText,
    Btn,
  },

  data() {
      return {
        displayImage: "",
        bio: "",
      };
    },

    methods: {
      async github() {
      const response = await fetch("https://api.github.com/users/codekage25");
      const data = await response.json();
      this.displayImage = data.avatar_url;
      this.bio = data.bio;
      console.log(this.bio);
    }
    },

    mounted() {
      this.github();
    },
};
</script>


<style>
.hero-con {
  display: grid;
  grid-template-columns: 1fr 0.3fr;
  gap: 3rem;
  align-items: center;
}

.front-page-heading {
  font-size: 9vw;
  font-weight: 500;
  line-height: 170px;
}

.img-and-bg-container {
  position: relative;
}

.user-img {
  height: 35vw;
  width: 100%;
  margin-left: 10rem;
  border-radius: 60px;
}

.img-bg {
  background: green;
  height: 28vw;
  width: 28vw;
  position: absolute;
  top: 250px;
  z-index: -1;
  left: 300px;
  border-radius: 60px;
}

@media (max-width: 801px) {
  .front-page-heading {
    font-size: 16vw;
    line-height: 13vw;
  }
  .socials {
    display: none;
  }
}
</style>
