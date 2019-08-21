<template>
  <div class="home">
    <h3>左滑删除演示</h3>
    <slide-delete>list1</slide-delete>
    <slide-delete>list2</slide-delete>
    <slide-delete>list3</slide-delete>
  </div>
</template>

<script>
import SlideDelete from "@/components/slide-delete";
export default {
  name: "home",
  components: { SlideDelete },
  data() {
    return {};
  }
};
</script>
