<template>
  <v-app>
    <v-content>
      <v-container>
        <v-btn @click="openDialog" color="primary">添加</v-btn>

        <v-dialog v-model="dialog" width="500">
          <v-card>
            <v-card-title class="headline grey lighten-2" primary-title>请输入信息</v-card-title>
            <v-text-field v-model="message" :counter="15" label="输入内容" required></v-text-field>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="primary" text @click="addTodo">添加</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>

        <Banner :list="list"></Banner>
      </v-container>
    </v-content>
  </v-app>
</template>

<script lang="ts">
import { Vue, Component } from "vue-property-decorator";

@Component({
  components: {
    Banner: () => import("./components/Banner.vue")
  }
})
export default class App extends Vue {
  public message = "";
  public editDialog = false;
  public dialog = false;
  public list: string[] = [];
  public created() {
    this.list = (localStorage.getItem("list") || "").split(",");
  }
  public openDialog() {
    this.dialog = !this.dialog;
  }
  public addTodo() {
    this.list.push(this.message);
    this.message = "";
    localStorage.setItem("list", this.list.toString());
    this.dialog = false;
  }
}
</script>
<style lang="scss">
.v-alert__wrapper {
  display: flex;
}
.v-alert__content {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>