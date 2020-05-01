<template>
  <v-app>
    <v-content>
      <v-container>
        <v-btn @click="openDialog" color="primary">添加</v-btn>

        <div class="text-center">

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

        </div>

          <v-dialog v-model="editDialog" width="500">
            <v-card>
              <v-card-title class="headline grey lighten-2" primary-title>请输入修改内容</v-card-title>
              <v-text-field v-model="message" :counter="15" label="输入内容" required></v-text-field>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="primary" text @click="closeEdit" >完成</v-btn>
              </v-card-actions>
            </v-card>
          </v-dialog>


        <vuedraggable class="wrapper" v-model="list">
          <transition-group>
            <!-- <div v-for="item in list" :key="item" class="item">
              <p>{{item}}</p>
            </div>-->
            <v-alert v-for="(item,key) in list" :key="item" color="#9E9E9E">
              <p>{{item}}</p>
              <p>
                <v-btn @click="edit(key)" color="primary" >编辑</v-btn>
                <v-btn color="error" @click="deleteList(key)" >删除</v-btn>
              </p>
            </v-alert>
          </transition-group>
        </vuedraggable>
      </v-container>
    </v-content>
  </v-app>
</template>

<script lang="ts">
import vuedraggable from "vuedraggable";
import { Vue, Component } from "vue-property-decorator";

@Component({
  components: {
    vuedraggable
  }
})
export default class App extends Vue {
  public list: string[] = [];
  public dialog = false;
  public editDialog = false
  public message = "";
  public key = 0
  public openDialog() {
    this.dialog = !this.dialog;
  }
  public created() {
    const local = localStorage.getItem("list") || "";
    this.list = local.split(",");
  }
  public addTodo() {
    this.list.push(this.message);
    this.message = "";
    localStorage.setItem("list", this.list.toString());
    this.dialog = false;
  }
  public edit(key: number) {
    this.key = key
    this.editDialog = true
  }
  public closeEdit() {
    console.log(this.message)
    this.list[this.key] = this.message
    localStorage.setItem("list", this.list.toString());
    this.editDialog = false
  }
  public deleteList(key: number) {
    this.list.splice(key,1)
    localStorage.setItem("list", this.list.toString());
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