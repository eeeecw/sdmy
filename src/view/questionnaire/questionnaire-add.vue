<template>
  <Row>
    <Col span="2" class="questionnaire-left">
      <Button class="button" type="primary" ghost @click="addOneQuestion(1)">单选</Button>
      <Button class="button" type="primary" ghost @click="addOneQuestion(2)">多选</Button>
      <Button class="button" type="primary" ghost @click="addOneQuestion(3)">填空</Button>
    </Col>
    <Col span="22" class="questionnaire-box">
      <div
        class="questionnaire"
        v-for="(que, index) in questionnaire"
        :key="index">
        <span>{{ ['', '单选', '多选', '填空'][que.type] }}</span>
      </div>
      <div class="bottom-button-box">
        <Button type="primary">保存问卷</Button>
      </div>
    </Col>
  </Row>
</template>

<script>
export default {
  name: 'questionnaire_add',
  data () {
    return {
      questionnaire: [
        { id: null, name: '问题1', type: 1 },
        { id: null, name: '问题2', type: 2 },
        { id: null, name: '问题3', type: 3 }
      ]
    }
  },
  methods: {
    addOneQuestion (type) { // 添加一道题
      this.questionnaire.push({ id: null, name: '问题1', type: type })
    }
  }
}
</script>

<style scoped>
.questionnaire, .bottom-button-box{
  background-color: #fff;
  padding: 20px;
  margin: 10px 0;
}
.bottom-button-box {
  text-align: center;
}
.questionnaire-left .button{
  display: block;
  margin: 5px 0 0 10px;
}
</style>
