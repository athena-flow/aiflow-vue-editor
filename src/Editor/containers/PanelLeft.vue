/**
* Created by aiflow on 2019/7/2.
*
* PanelLeft 左侧面板
*/

<style scoped lang="less" rel="stylesheet/less">
  .panel-left {
    .card-item {
      display: flex;
      flex-wrap: wrap;
      justify-content: flex-start;
      align-content: flex-start;
    }
  }
</style>

<template>
  <CardBox class="panel-left" placement="left" position="right" :width="250" :title="$t('L10300')" @expand="toggleHandler">
    <CardItem
      v-for="(item, index) in materials"
      :key="index"
      :title="$t(item.lang) || item.label"
      :enableFold="true"
      :bold="true"
    >
      <NodeElement
        v-for="(child, childIndex) in item.children.filter(target => target.enable)"
        :key="childIndex"
        :title="child.label"
        :info="child"
      >
      </NodeElement>
    </CardItem>
  </CardBox>
</template>

<script>
  import CardBox from '../components/CardBox'
  import CardItem from '../components/CardItem'
  import NodeElement from '../components/NodeElement'

  export default {
    name: 'PanelLeft',
    components: {
      CardBox,
      CardItem,
      NodeElement
    },
    props: {
      materialList: Array
    },
    data () {
      return {}
    },
    computed: {
      materials () {
        return this.materialList.filter(item => item.enable)
      }
    },
    methods: {
      toggleHandler (data) {
        const _t = this
        _t.$X.utils.bus.$emit('editor/panel/toggle', data)
      }
    }
  }
</script>
