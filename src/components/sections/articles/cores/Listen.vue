<template>
  <article class="listen flex-center">
    <span class="iconfont icon-unie66a" @click="listenSent"></span>

    <select class="block-style" v-model="select">
      <option disabled selected value="select">请选择语音引擎</option>
      <option v-for="option in options" :key="option.value" :value="option.value">{{ option.text }}</option>
    </select>
    <audio ref="audio"></audio>
  </article>
</template>

<script>
import get from "../../../../url";

export default {
  name: "Listen",
  props: {
    examed: null
  },

  data() {
    return {
      select: "select",
      options: [
        { text: "谷歌", value: "google" },
        { text: "腾讯", value: "tencent" },
        { text: "百度", value: "baidu" },
        { text: "搜狗", value: "sougou" }
      ],
    };
  },
  watch: {
    select: function() {
      if (this.select == "google") {
        this.$refs.audio.src = get.googleTTS(
          this.examed.replace("<b>", "").replace("</b>", "")
        );
        this.$refs.audio.play();
      } else if (this.select == "tencent") {
        this.$refs.audio.src = get.tencentTTS(
          this.examed.replace("<b>", "").replace("</b>", "")
        );
        this.$refs.audio.play();
      } else if (this.select == "baidu") {
        this.$refs.audio.src = get.baiduTTS(
          this.examed.replace("<b>", "").replace("</b>", "")
        );
        this.$refs.audio.play();
      } else if (this.select == "sougou") {
        this.$refs.audio.src = get.sougouTTS(
          this.examed.replace("<b>", "").replace("</b>", "")
        );
        this.$refs.audio.play();
      }
    },
  },
  methods: {
    listenSent: function() {
      this.$refs.audio.play();
    }
  }
};
</script>

<style scoped>
.listen {
  box-shadow: none;
  font-size: 2rem;
}

select {
  margin: 1rem 3rem 3rem;
  text-align: center;
  border-color: #fff;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
}
option {
  width: auto;
  text-align: center;
  text-align-last: center;
}

.iconfont{
  font-size: 3rem;
}
.iconfont:hover{
  cursor: pointer;
}

</style>