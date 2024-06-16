<template>
  <view class="container">
    <view class="steps">
      <uni-steps :options="options" :active="active"></uni-steps>
    </view>
    <view v-if="active === 0">
      <uni-section title="鱼获(条)" padding>
        <template v-slot:decoration>
          <view class="decoration"></view>
        </template>
        <uni-easyinput v-model="count" type="number" placeholder="请输入本次收获条数" @input="input"></uni-easyinput>
      </uni-section>
      <uni-section title="钓鱼时长(小时)" padding>
        <template v-slot:decoration>
          <view class="decoration"></view>
        </template>
        <uni-easyinput v-model="time" type="number" placeholder="请输入本次钓鱼时长" @input="input"></uni-easyinput>
      </uni-section>
    </view>
    <view v-if="active === 1">
      <uni-file-picker 
        v-model="images"
        fileMediatype="image"
        mode="grid"
        limit="3"
        @select="select"
        @progress="progress"
        @success="success"
        @fail="fail"
      />
    </view>
    <view v-if="active === 2">
      <uni-section title="钓点评分" padding>
        <template v-slot:decoration>
          <view class="decoration"></view>
        </template>
        <uni-rate v-model="rateValue" @change="onRateChange" />
      </uni-section>
      
      <view class="page-section page-section-gap">
        <!-- <map style="width: 100%; height: 300px;" :latitude="latitude" :longitude="longitude"></map> -->
      </view>
    </view>
    <view class="bottom-container">
      <button v-if="active > 0" @click="goPrevious()">上一步</button>
      <button type="primary" v-if="[0,1].includes(active)" @click="goNext">下一步</button>
      <button type="primary" v-if="active === 2" @click="submit">提交</button>
    </view>
    </view>
</template>

<script>

export default {
  name: 'CreateTask',
  data() {
    return {
      active: 1,
      options: [{ title: '垂钓数据'}, { title: '成果图片' }, { title: '钓点评价' }],
      count: '',
      time: '',
      images: [],
      rateValue: 0,
      id:0, // 使用 marker点击事件 需要填写id
      title: 'map',
      latitude: 39.909,
      longitude: 116.39742,
    };
  },
  methods: {
    goPrevious: function () {
      this.active--
    },
    goNext: function () {
      console.log('imageValue:', this.imageValue)
      this.active++
    },
    submit: function () {
      console.log('submit')
    },
    select(e){
      console.log('选择文件：',e)
    },
    // 获取上传进度
    progress(e){
      console.log('上传进度：',e)
    },
    
    // 上传成功
    success(e){
      console.log('上传成功')
    },
    
    // 上传失败
    fail(e){
      console.log('上传失败：',e)
    },
    onChange(e) {
      console.log('rate发生改变:' + JSON.stringify(e))
    }
  }
}
</script>

<style lang="less">

.container {
  margin: 16px 12px;

  .steps {
    margin-bottom: 24px
  }

  .bottom-container {
    margin-top: 12px;
    display: flex;
    gap: 6px;
    button {
      flex: 1;
    }
  }
  
  .decoration{
    width: 6px;
    height: 6px;
    margin-right: 4px;
    border-radius: 50%;
    background-color: #18bc37;
  }
}

</style>
