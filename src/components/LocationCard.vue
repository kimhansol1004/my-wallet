<template>
  <div class="block">
    <el-row style="padding-top:10px; height: 350px; margin:2px; border:solid 2px #0067A3;border-radius:10px" >
      <el-row>
        <el-col :span="20">
            새로운 장소 등록
        </el-col>
        <el-col :span="2">
            <el-button type="danger" icon="el-icon-delete" circle style="top: 100px"></el-button>
        </el-col>
      </el-row>

      <el-row>
        <el-col :span="12">
          <el-row>
            <el-input placeholder="" v-model="writtenLocation" style="margin:2px;">
              <template slot="prepend" >장소 : </template>
            </el-input>
          </el-row>
          <el-row>
            <el-time-select 
              v-model="value" 
              :picker-options="{start: '08:30',step: '00:15',end: '18:30'}" 
              placeholder="시간을 입력하세요" 
              style=" width:100%; margin:2px;"
            >
            </el-time-select>
          </el-row>
          <el-row>
            <el-col :span="8">
              <el-button disabled style="width:100%; margin:2px;">순서</el-button>
            </el-col>
            <el-col :span="16">
              <el-input-number 
                v-model="order" 
                controls-position="right" 
                @change="handleChange" 
                :min="1" 
                :max="10"
                style="width:100%; margin:2px;"
              >
              </el-input-number>
            </el-col>
          </el-row>
        </el-col>
        <el-col :span="12">
          <el-row>
            <div id="map" style="z-index: 0;left:15px;width:180px;height:128px;"></div>
          </el-row>
        </el-col>
      </el-row>
      <el-row>
        <el-input
          type="textarea"
          placeholder="메모를 입력해주세요."
          v-model="memo"
          maxlength="100"
          rows="5"
          show-word-limit
        >
        </el-input>
      </el-row>
      <el-row style="margin-top:3px">
      
        <el-button v-if="!isSaved" type="success" @click="handClickSave">SAVE</el-button>
        <p v-else>저장되었습니다.</p>
      </el-row>
    </el-row>
  </div>
</template>

<script>
export default {
    name:'LocationCard',
    data() {
      return {
        value: '',
        writtenLocation: '',
        order:'',
        memo:'',
        isSaved: false
      };
    },
    methods: {
      handClickSave() {
        this.$emit('clickSave');
        this.isSaved = true;
      },
      handleChange(value) {
        console.log(value);
      },
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
    },
     mounted() {
    if (window.kakao && window.kakao.maps) {
      this.initMap()
    } else {
      const script = document.createElement('script')
      script.onload = () => kakao.maps.load(this.initMap);
      script.src = 'http://dapi.kakao.com/v2/maps/sdk.js?appkey=a7c5bceb92db6ede8a37c7bf62832c61'
      document.head.appendChild(script)
    }
  }
}
</script>

<style>

</style>