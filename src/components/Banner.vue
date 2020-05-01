<template>
  <div class="banner">
    <vuedraggable class="wrapper" v-model="list">
      <transition-group>
        <v-alert v-for="(item) in list" :key="item" color="#9E9E9E">
          <p>{{item}}</p>
          <p>
            <v-btn color="primary">编辑</v-btn>
            <v-btn color="error">删除</v-btn>
          </p>
        </v-alert>
      </transition-group>
    </vuedraggable>
  </div>
</template>
<script lang="ts" >
import { Vue, Component, Prop } from "vue-property-decorator";
import vuedraggable from "vuedraggable";
@Component({
  components: {
    vuedraggable
  }
})
export default class Banner extends Vue {
  @Prop(Array) readonly list: string[] | undefined;
}
</script>