<template>
  <div class="questionnaire-list-container">
    <div class="questionnaire-search-container">
      <Button type="primary" @click="createQuestionnaire">创建问卷</Button>
    </div>

    <Table :columns="tableColumn" :data="tableData"></Table>
  </div>
</template>

<script>
export default {
  name: 'questionnaire_list',
  data () {
    return {
      tableColumn: [
        {
          title: '名称',
          key: 'name'
        },
        {
          title: '回收数',
          key: 'total'
        },
        {
          title: '创建时间',
          key: 'createTime'
        },
        {
          title: '操作',
          key: ''
        }
      ],
      tableData: []
    }
  },
  methods: {
    createQuestionnaire () { // 点击添加问卷按钮
      const route = {
        name: 'questionnaire_add'
      }
      this.$router.push(route)
    }
  }
}
</script>

<style scoped>
  .questionnaire-search-container{
    margin-bottom: 20px;
  }
</style>
