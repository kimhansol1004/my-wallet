<template>
  <div>
    <h3>날짜</h3>
    <div class="block" style="margin-bottom:10px">
      <el-date-picker
        type="date"
        v-model="date"
        placeholder="날짜를 먼저 선택해주세요">
      </el-date-picker>
    </div>

    <location-card v-for="(schedule, index) in schedules" :key="index" v-on:clickSave="save">
      {{ schedule }}
    </location-card>

    <el-button v-if="date.length !== 0" type="primary" icon="el-icon-circle-plus" :disabled="!isSaved" @click="addCard">장소 추가</el-button>
  </div>
</template>

<script>
import LocationCard from './LocationCard.vue'
export default {
  components: { LocationCard },
    name: 'Detail',
    data() {
      return  {
        date: '',
        schedules:[],
        isSaved: true
      }
    },
    methods: {
      addCard: function() {
        this.schedules.push('c');
        this.isSaved = false;
      },
      save: function() {
        this.isSaved = true;
      }
    }
}

  
</script>

<style>
  
</style>