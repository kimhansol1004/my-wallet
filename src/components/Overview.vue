<template>
  <div>
      <el-row>
      <el-col :span="24">
        <div id="map" style="width:100%;height:300px;"></div>
      </el-col>
    </el-row>
    <el-row>
      <el-col :span="12">
        <el-date-picker
          v-model="value1"
          type="date"
          placeholder="Pick a day">
        </el-date-picker>
      </el-col>
      <el-col :span="12">
        <el-date-picker
          v-model="value1"
          type="date"
          placeholder="Pick a day">
        </el-date-picker>
      </el-col>
    </el-row>
    <el-row>
      <el-col :span="24">
        <el-dropdown>
          <span class="el-dropdown-link">
            날짜를 선택해주세요. 2021년 7월 21일<i class="el-icon-arrow-down el-icon--right"></i>
          </span>
          <el-dropdown-menu slot="dropdown">
            <el-dropdown-item>19일</el-dropdown-item>
            <el-dropdown-item>20일</el-dropdown-item>
            <el-dropdown-item>21일</el-dropdown-item>
            <el-dropdown-item>22일</el-dropdown-item>
            <el-dropdown-item>23일</el-dropdown-item>
          </el-dropdown-menu>
        </el-dropdown>
      </el-col>
    </el-row>
    <el-row>
      <el-col :span="24">
        <el-timeline>
            <el-timeline-item
              v-for="(activity, index) in activities"
              :key="index"
              :icon="activity.icon"
              :type="activity.type"
              :color="activity.color"
              :size="activity.size"
              :timestamp="activity.timestamp">
              {{activity.content}}
            </el-timeline-item>
          </el-timeline>
      </el-col>
    </el-row>
  </div>
</template>

<script>
export default {
    name: 'Overview',
    mounted() {
    if (window.kakao && window.kakao.maps) {
      this.initMap()
    } else {
      const script = document.createElement('script')
      script.onload = () => kakao.maps.load(this.initMap);
      script.src = 'http://dapi.kakao.com/v2/maps/sdk.js?appkey=a7c5bceb92db6ede8a37c7bf62832c61'
      document.head.appendChild(script)
    }
  },
  data() {
  return {
    activities: [{
      content: 'Custom icon',
      timestamp: '2021-04-12 20:46',
      size: 'large',
      type: 'primary',
      icon: 'el-icon-more'
    }, {
      content: 'Custom color',
      timestamp: '2021-04-03 20:46',
      color: '#0bbd87'
    }, {
      content: 'Custom size',
      timestamp: '2021-04-03 20:46',
      size: 'large'
    }, {
      content: 'Default node',
      timestamp: '2021-04-03 20:46'
    }]
  };
},
  methods: {
    initMap () {
      const container = document.querySelector('#map')
      const options = {
        center: new kakao.maps.LatLng(33.37670140634873, 126.53186278844765),
        level: 11
      }
      const map = new kakao.maps.Map(container, options)
      const markerPosition = new kakao.maps.LatLng(33.37670140634873, 126.53186278844765);

      const marker = new kakao.maps.Marker({
        position: markerPosition
      });
      marker.setMap(map)
    }
  }
}
</script>

<style lang="css" scoped>
  .el-tabs__nav is-top {
    min-width: 100%;
  }
  .tap-pane {
    min-width: 45%;
  }
</style>