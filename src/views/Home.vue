<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <div>{{ textFile }}</div>
    <HelloWorld msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import HelloWorld from "@/components/HelloWorld.vue";
import { writeFile, readTextFile } from "@tauri-apps/api/fs";

@Component({
  name: "Home",
  components: { HelloWorld },
})
export default class Home extends Vue {
  textFile = "nope";

  async created(): Promise<void> {
    writeFile({ contents: "{Hallo}", path: "test_tauri.json" });
    this.textFile = await readTextFile("test_tauri.json");
  }
}
</script>
