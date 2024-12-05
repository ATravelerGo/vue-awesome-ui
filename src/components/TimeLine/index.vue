<script setup lang="ts">
import { ref } from 'vue';

const messageList = ref([
  {
    time: '11:46',
    isWarning: true,
    message: '异常: 发现车辆疑似占压消防通道。中新生态城X停车车车车',
  },
  {
    time: '11:42',
    isWarning: false,
    message: '正常: 中新生态城X停车场',
  },
  {
    time: '11:43',
    isWarning: true,
    message: '异常: 发现车辆疑似占压消防通道。中新生态城X停车',
  },
  {
    time: '11:42',
    isWarning: true,
    message: '异常: 发现车辆疑似占压消防通道。中新生态城X停车',
  },
  {
    time: '11:41',
    isWarning: false,
    message: '正常: 中新生态城X停车场',
  },
  {
    time: '11:40',
    isWarning: true,
    message: '异常: 发现车辆疑似占压消防通道。中新生态城X停车',
  },
]);

</script>


<template>

  <div class="timeline-data-content">
    <div v-for="(item,index) in messageList" :key="item.time" class="timeline-data-content-item">
      <div class="timeline-data-content-item-time" :class="[index===0? 'light-time':'']">
        {{ item.time }}
      </div>
      <div class="timeline-data-content-item-circle" :class="[index===0? 'light-circle':'']">
        <div v-if="index!==messageList.length-1" class="timeline-data-content-item-circle-line"
             :class="[item.message.length<=13? 'short-line':'',index===0? 'light-line':'']" />
      </div>
      <div class="timeline-data-content-item-message" :class="[item.isWarning? 'warning-message':'normal-message']">
              <span :title="item.message">
                {{ item.message }}
              </span>

        <img v-if="item.isWarning" src="./assets/rightArrow.png" alt="rightArrow">

      </div>
    </div>


  </div>
</template>

<style scoped lang="scss">

.timeline-data-content {
  width: 100%;
  height: 100%;
  margin-top: 15px;
  overflow-y: auto;

  &-item {
    padding: 0 16px;
    font-size: 14px;
    display: flex;
    justify-content: space-between;
    margin-bottom: 4px;

    &-time {
      margin-top: 12px;
      color: black;
    }

    &-circle {
      margin-top: 12px;
      background: rgba(29, 109, 167, 0.4);
      border: 1px solid rgba(132, 209, 234, 0.6);
      width: 14px;
      height: 14px;
      border-radius: 50%;
      position: relative;
      margin: 12px 5px 0 5px;

      &-line {
        height: 45px;
        position: absolute;
        bottom: -47px;
        left: 50%;
        transform: translateX(-50%);
        opacity: 0.4;
        border: 1px solid #84D1EA;
      }

      &-line.short-line {
        height: 25px;
        bottom: -28px;
        left: 50%;
        transform: translateX(-50%);
        opacity: 0.4;
        border: 1px solid #84D1EA;
      }
    }

    &-message {
      border-radius: 4px;
      //max-height: 60px;
      padding: 10px 26px 10px 12px;
      text-align: left;
      width: 190px;
      position: relative;

      span {
        display: -webkit-box;
        -webkit-box-orient: vertical;
        -webkit-line-clamp: 2; /* 限制为两行 */
        overflow: hidden;
        text-overflow: ellipsis;
      }

      img {
        position: absolute;
        right: 10px;
        top: 50%;
        transform: translateY(-50%);
        cursor: pointer;
        visibility: hidden;
      }

      &:hover img {
        visibility: visible;
      }

    }

  }

}


.warning-message {
  background: linear-gradient(270deg, rgba(43, 89, 128, 0.3) 10%, rgba(255, 171, 132, 0.4) 78%, rgba(255, 72, 72, 0.5) 100%);
}

.normal-message {
  background: linear-gradient(270deg, rgba(43, 89, 128, 0.2) 10%, rgba(6, 198, 255, 0.2) 75%, rgba(6, 184, 255, 0.3) 100%);
}


.light-circle {
  background: rgba(29, 109, 167, 0.6);
  border: 1px solid #84D1EA;
}

.light-line {
  border: 1px solid transparent;
  border-image: linear-gradient(to bottom, rgb(130, 206, 230) 0%, rgb(102, 158, 179) 50%, rgb(65, 100, 114) 100%);
  opacity: 1;
  border-image-slice: 1;
}

.light-time {
  color: black;
}

</style>