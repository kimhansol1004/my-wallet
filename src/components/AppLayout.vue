<template>
  <div >
    <el-row>
      <el-col :span="24">
        <img src="../assets/jeju_banner2.png" :style="{maxHeight: '80px', minWidth: '100%'}" alt=""/>
      </el-col>
    </el-row>
    <el-row class="tab-layout">
      <el-col :span="12">
        <el-button :type="primary" :style="{minWidth: '100%'}" @click="handleClickOverview(true)">요약</el-button>
      </el-col>
      <el-col :span="12">
        <el-button :type="primary" :style="{minWidth: '100%'}"  @click="handleClickOverview(false)">자세히</el-button>
      </el-col>
    </el-row>
    
    <div v-if="isOverview">
      <overview />
    </div>
    <div v-else>
      <detail />
    </div>
  </div>
</template>

<script>
import Detail from './Detail.vue';
import Overview from './Overview.vue';

export default {
  name: "AppLayout",
  components: {
    Overview,
    Detail
  },
  data() {
    return {
      isOverview: true,
    }
  },
  methods: {
    handleClickOverview: function(isOverview) {
      this.isOverview = isOverview;
    }
  }

}
</script>

<style lang="css" scoped>
  .tab-layout {
    margin-bottom: 10px;
  }
</style>