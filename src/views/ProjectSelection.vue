<template>
  <main>
    <div id="projects-wrapper">
      <h1>Projektwahl</h1>
      <Project
        v-for="project in projects"
        :key="project.caption"
        :selected="selectedProjects.includes(project.id)"
        :project="project"
        @click="
          () => {
            toggleProject(project.id);
          }
        "
      >
      </Project>
    </div>
    <ProjectCart></ProjectCart>
  </main>
</template>

<style lang="sass" scoped>

main
  display: flex
  color: var(--color3)
  font-size: 1.2em
  min-height: 100vh
  #projects-wrapper
    box-sizing: border-box
    display: flex
    width: 100%
    max-width: 80vw
    flex-direction: column
    align-items: center

    background: var(--color2)
    padding: 1em
    padding-right: 2em
    > h1
      justify-self: left
      font-size: 3em
</style>

<script>
import { defineComponent } from 'vue'
import useUser from '@/compositions/useUser'
import useProjects from '@/compositions/useProjects'
import Project from '@/components/Project'
import ProjectCart from '@/components/ProjectCart'

export default defineComponent({
  components: {
    Project,
    ProjectCart
  },
  async setup () {
    const { toggleProject, selectedProjects } = await useUser()
    const { projects } = await useProjects()

    return { toggleProject, selectedProjects, projects }
  }
})
</script>
