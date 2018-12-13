<template>
  <Row>
    <Col span="2" class="questionnaire-left">
      <Button class="button" type="primary" ghost @click="addOneQuestion(1)">单选</Button>
      <Button class="button" type="primary" ghost @click="addOneQuestion(2)">多选</Button>
      <Button class="button" type="primary" ghost @click="addOneQuestion(3)">填空</Button>
    </Col>
    <Col span="22" class="questionnaire-box">
      <draggable v-model="questionnaire" :options="{name: 'questionnaire-box'}">
        <div
          class="questionnaire-item"
          v-for="(que, index) in questionnaire"
          :key="index">
          <h2 class="que-title">
            [{{ ['', '单选', '多选', '填空'][que.type] }}] {{ index + 1 }}.{{ que.name }}
          </h2>
          <div class="que-btn-box">
            <Button v-if="que.type !== 3" @click="addOp(index)" size="large" shape="circle" icon="md-add" type="dashed"></Button>
            <Button @click="removeQue(index)" size="large" shape="circle" icon="md-trash" type="dashed"></Button>
          </div>
          <draggable v-model="que.children" :options="{name: 'option-box'}">
            <div
            class="option"
            v-for="(op, oindex) in que.children"
            :key="oindex">
              {{ op.name }}
              <Button class="option-btn" @click="removeOp(index, oindex)" size="small" shape="circle" icon="md-close" type="dashed"></Button>
            </div>
          </draggable>
        </div>
      </draggable>

      <div class="bottom-button-box">
        <Button type="primary">保存问卷</Button>
      </div>
    </Col>
  </Row>
</template>

<script>
import draggable from 'vuedraggable'
export default {
  name: 'questionnaire_add',
  data () {
    return {
      questionnaire: [
        {
          id: null,
          name: '问题1',
          type: 1,
          children: [
            {
              id: null,
              name: '问题1的选项1'
            },
            {
              id: null,
              name: '问题1的选项2'
            },
            {
              id: null,
              name: '问题1的选项3'
            }
          ]
        },
        {
          id: null,
          name: '问题2',
          type: 1,
          children: [
            {
              id: null,
              name: '问题2的选项1'
            },
            {
              id: null,
              name: '问题2的选项2'
            },
            {
              id: null,
              name: '问题2的选项3'
            }
          ]
        }
      ]
    }
  },
  methods: {
    addOneQuestion (type) { // 添加一道题
      if (type === 3) {
        this.questionnaire.push({
          id: null,
          name: '新增的填空',
          type: type,
          children: [
            {
              id: null,
              name: '填空项目'
            }
          ]
        })
      } else {
        this.questionnaire.push({
          id: null,
          name: '新增的问题',
          type: type,
          children: [
            {
              id: null,
              name: '选项1'
            },
            {
              id: null,
              name: '选项2'
            },
            {
              id: null,
              name: '选项3'
            }
          ]
        })
      }
    },
    removeQue (index) { // 移除一道题
      this.questionnaire.splice(index, 1)
    },
    addOp (index) { // 添加一个选项
      this.questionnaire[index].children.push({
        id: null,
        name: '选项'
      })
    },
    removeOp (index, oindex) { // 移除一个选项
      this.questionnaire[index].children.splice(oindex, 1)
    }
  },
  components: {
    draggable
  }
}
</script>

<style scoped>
.questionnaire-item, .bottom-button-box{
  position: relative;
  background-color: #fff;
  padding: 20px;
  margin: 15px 0;
  border: 1px #fff solid;
  border-radius: 3px;
}
.questionnaire-item:hover{
  border: 1px #409EFF solid;
  box-shadow: 3px 3px 5px #999;
}
.bottom-button-box {
  text-align: center;
}
.questionnaire-left .button{
  display: block;
  margin: 5px 0 0 10px;
}
.option{
  padding: 5px 10px;
  border: 1px solid #fff;
  height: 24px;
  line-height: 24px;
  box-sizing: content-box
}
.option:hover{
  border: 1px dashed darkcyan;
}
.que-title{
  font-size: 16px;
  margin-bottom: 15px;
}
.que-btn-box{
  position: absolute;
  top: 10px;
  right: 24px;
}
.que-btn-box Button{
  margin: 0 5px;
}
.option-btn{
  float: right;
}
</style>
