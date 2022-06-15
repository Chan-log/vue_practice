<template>
  <div>
    <div v-if="step == 0">
      <Post v-for="(post, i) in post" :key="i" :post="post" />
    </div>

    <div v-if="step == 1">
      <div
        class="upload-image"
        :style="{ backgroundImage: `url(${imageUrl})` }"
      ></div>
      <div class="filters">
          <FilterBox :imageUrl="imageUrl" v-for="(filterList, i) in filterList" :key="i" :post="post" :filterList="filterList"></FilterBox>
      </div>
    </div>

    <div v-if="step == 2">
      <div
        class="upload-image"
        :style="{ backgroundImage: `url(${imageUrl})` }"
      ></div>
      <div class="write">
        <textarea @input="mainText" class="write-box">write!</textarea>
      </div>
    </div>
  </div>
</template>


<script>
import Post from "./Post.vue";
import FilterBox from "./FilterBox.vue";
export default {
  name: "Container",
  props: {
    post: Object,
    step: Number,
    imageUrl: String,
  },
  data(){
    return{
      filterList : [ "aden", "_1977", "brannan", "brooklyn", "clarendon", "earlybird", "gingham", "hudson", 
"inkwell", "kelvin", "lark", "lofi", "maven", "mayfair", "moon", "nashville", "perpetua", 
"reyes", "rise", "slumber", "stinson", "toaster", "valencia", "walden", "willow", "xpro2"],
    }
  },
  components: {
    Post: Post,
    FilterBox: FilterBox,
  },
  methods: {
      mainText(e){
          this.$emit('mainText', e.target.value)
      },
  },
};
</script>

<style>
.upload-image {
  width: 100%;
  height: 450px;
  background: rgb(255, 255, 255);
  background-size: contain;
  background-repeat: no-repeat;
}
.filters {
  overflow-x: scroll;
  white-space: nowrap;
}
.filter-1 {
  width: 100px;
  height: 100px;
  background-color: rgba(59, 35, 35, 0);
  margin: 10px 10px 10px auto;
  padding: 8px;
  display: inline-block;
  color: white;
  background-size: cover;
}
.filters::-webkit-scrollbar {
  height: 5px;
}
.filters::-webkit-scrollbar-track {
  background: #f1f1f1;
}
.filters::-webkit-scrollbar-thumb {
  background: #888;
  border-radius: 5px;
}
.filters::-webkit-scrollbar-thumb:hover {
  background: #555;
}
.write-box {
  border: none;
  width: 90%;
  height: 100px;
  padding: 15px;
  margin: auto;
  display: block;
  outline: none;
}
</style>