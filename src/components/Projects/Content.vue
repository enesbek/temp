<template>
  <div class="page">
    <div class="project-field">
      <div class="project-title font-semibold text-2xl tracking-wider mb-4">
        YOUR PROJECTS 
        <button class="create-project-btn text-2xl font-semibold ml-5"
                @click="toggleCreateModal = !toggleCreateModal"><i class="fa-solid fa-circle-plus"></i></button>
      </div>
      <!-- Create Modal -->
      <div v-if="toggleCreateModal"
          class="fixed overflow-x-hidden overflow-y-auto inset-0 flex justify-center items-center z-50 ">
        <div
        class="create-modal relative mx-auto w-auto max-w-4xl flex ">
          <div class="bg-white w-full shadow-2xl max-w-2xl flex flex-col rounded">
            <div class="text-2xl font-bold mt-4 ml-6 mb-2">Let's Create Project</div>
            <p class="ml-6 text-gray-600">You can manage your project with this web site.</p>
            <div class="ml-6">
              <span class="text-sm font-semibold">Project Name</span><br>
              <input class="border-2 border-gray-600 rounded" v-model="newProject.projectName"><br>
              <span class="text-sm opacity-75">This can be name of your company, team or organization</span><br>
            </div>
            <div class="ml-6 mt-4 mb-2">
              <span class="text-sm font-semibold">Project Description</span><br>
              <textarea class="border-2 border-gray-600 rounded w-64 h-24" v-model="newProject.projectDescription"></textarea><br>
              <span class="text-sm opacity-75">You can give details about the Project</span><br>
            </div>
            <div class="ml-6 mb-2">
              <span class="text-sm font-semibold">Start Date*&emsp;&emsp;&emsp;&emsp;&emsp;End Date*</span><br>
              <input type="date" class="border-2 border-gray-600 rounded" v-model="newProject.startDate">
              <input type="date" class="border-2 border-gray-600 rounded ml-4" v-model="newProject.endDate">
              <p class="mt-2 italic text-sm">Dates are optional</p>
            </div>
            <button class="rounded bg-gray-300 px-6 py-2 w-3/12 ml-28 mb-3 " @click="createNewProject">Create</button>  
          </div>
          <div class="create-modal-image rounded">
            <button class="close-modal-btn text-xl" @click="toggleCreateModal = false"><i class="fa-solid fa-xmark"></i></button>
            <img class="mt-10" src="@/assets/projects/create-modal.jpg"/>
          </div>
        </div>
      </div>
      <div v-if="toggleCreateModal" class="absolute z-40 inset-0 opacity-25 bg-black"></div>
      <!--  -->
      <ProjectsInfo class="mb-2"/>
    </div>
    <div class="bottomPage">
      <div class="project-title font-semibold text-2xl tracking-wider mb-4">
        ASSIGNED PROJECTS 
      </div>
      <AssignedProjectsInfo />
    </div>
  </div>
</template>

<script>
import ProjectsInfo from './ProjectsInfo.vue'
import AssignedProjectsInfo from './AssignedProjectsInfo.vue'
import store from '../../store'
import { mapActions } from 'vuex';
export default {
  components: {
    ProjectsInfo,
    AssignedProjectsInfo,
  },
  data() {
    return {
      newProject:{
        projectName: null,
        projectDescription: null,
        startDate: null,
        endDate: null,
        isFinished: false,
      },
      toggleCreateModal: false,
    };
  },
  setup() {
    store.commit('changeSidebarState');
  },
  methods: {
    ...mapActions(['createProject']),
    createNewProject(){
      this.toggleCreateModal = false
      this.createProject(this.newProject);
    }
  },
};
</script>


<style scoped>
.project-field {
  width: 60vw;
  margin-left: 10em;
  padding-top: 3em;
}
.bottomPage{ 
  width: 100%;
  background-color: rgb(200, 200, 200);
  padding-left: 10em;
  padding-top: 3em;
  padding-bottom: 50px;
}
.create-modal-image{
  width: 60rem;
  background-color: white;
}
.create-modal{
  height: 33rem;
}
.close-modal-btn{
  margin-left: 27rem;
  margin-top: .5rem;
}
</style>
