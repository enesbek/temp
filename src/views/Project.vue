<template>
  <div>
    <div class="project-top flex flex-col">
      <div class="project-info flex">
        <span class="project-icon text-4xl flex-initial m-2 text-white">{{ project.projectName[0] }}</span>
        <div class="flex-initial ml-2">
          <div class="text-xl font-semibold mt-1">{{ project.projectName }}</div>
          <div> {{ project.projectDescription }}</div>
          <div class="italic text-sm"> Start: {{project.startDate[8]}}{{project.startDate[9]}}{{project.startDate[7]}}{{project.startDate[5]}}{{project.startDate[6]}}{{project.startDate[4]}}{{project.startDate[2]}}{{project.startDate[3]}}
            <br />    End: &nbsp;{{project.endDate[8]}}{{project.endDate[9]}}{{project.endDate[7]}}{{project.endDate[5]}}{{project.endDate[6]}}{{project.endDate[4]}}{{project.endDate[2]}}{{project.endDate[3]}}</div>
        </div>
        <div></div>
      </div>
      <div class="tabs flex">
        <button class="tabs-btn" 
          v-on:click="changeTab(0)"><fa icon="clipboard"></fa> Boards</button>
        <button class="tabs-btn"
          v-on:click="changeTab(1)"><i class="fa-solid fa-users"></i> Members</button>
        <button class="tabs-btn"
          v-on:click="changeTab(2)"><i class="fa-solid fa-gear"></i> Settings</button>
      </div>
    </div>
    <div>
      <Boards v-show="selectedTab[0]"/>
      <Members v-show="selectedTab[1]"/>
      <Settings v-show="selectedTab[2]"/>
    </div>
  </div>
</template>

<script>
import Boards from '../components/Project/Boards.vue'
import Members from '../components/Project/Members.vue'
import Settings from '../components/Project/Settings.vue'
import store from '../store'
export default {
  data(){
    return {
      selectedTab: [true, false, false],
    }
  },
  components:{
    Boards,
    Members,
    Settings
  },
  methods:{
    changeTab(index) {
      this.selectedTab = [false, false, false]
      this.selectedTab[index] = true
    }
  },
  created() {
    store.commit('changeSidebarState');
    this.$store.dispatch("loadProject");
  },
  computed: {
    project(){
      return this.$store.state.project
    },
  },
};
</script>

<style scoped>
.project-top {
  background-color: rgb(225, 225, 225);
  height: 30vh;
  margin-top: 0;
  padding-top: 2rem;
  position: relative;
}
.project-info {
  margin-left: 35%;
  width: 35%;
  @apply rounded;
}
.project-icon{
  padding: 1rem;
  padding-left: 1.5rem;
  padding-right: 1.5rem;
  background-image: linear-gradient(to bottom, rgba(22, 133, 141), rgba(43, 226, 240));
  @apply rounded font-bold text-6xl;
}
.tabs{
  margin-left: 30%;
  margin-bottom: 0;
  width: 40%;
  position: absolute;
  bottom: 0;
}
.tabs-btn{
  background-color: rgb(201, 201, 201);
  @apply pl-4 pr-4 pt-2 pb-2 mx-1 mt-1 rounded;
}
.tabs-btn:hover{
  background-color: white;
}
.edit-btn{
  background-color: rgb(201, 201, 201);
  border-radius: 3px;
  height: 30px;
  width: 140px;
}
.edit-btn:hover{
  background-color: white;
}
</style>