<template>
    <AddTask v-show="showForm" @add-task="addTask" />
    <Tasks :tasks="tasks" @delete-task="deleteTask" @toggle-reminder="toggleReminder" />
</template>

<script>
import AddTask from '../components/AddTask'
import Tasks from '../components/Tasks'
export default {
    name: 'Home',
    components: {
        Tasks,
        AddTask
    },
    props: {
        showForm: Boolean
    },
    data(){
        return{
            tasks : []
        }
    },
    methods: {
        async addTask(task){
        const res = await fetch(
            "api/tasks",
            {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(task)
            }
            )
        this.tasks = [...this.tasks, task]
        },
        async deleteTask(id){
        const res = await fetch(`api/tasks/${id}`, {
            method: 'DELETE'
        })
        res.status === 200 ? this.tasks = this.tasks.filter((task) => task.id!==id) : alert("Error in deleting")
        },
        async toggleReminder(id){
        const taskToToggle = await this.fetchTask(id)
        const updTask = {...taskToToggle, reminder: !taskToToggle.reminder}

        const res = await fetch(`api/tasks/${id}`, {
            method: 'PUT',
            headers: {
            'Content-Type': 'application/json'
            },
            body: JSON.stringify(updTask)
        })

        const data = await res.json()
        this.tasks = this.tasks.map((task) => task.id === id ? {...task, reminder:data.reminder} : task)
        },
        async fetchTasks(){
        const res = await fetch("api/tasks")
        const data = await res.json()
        return data
        },
        async fetchTask(id){
        const res = await fetch(`api/tasks/${id}`)
        const data = await res.json()
        return data
        }
    },
    async created(){
        this.tasks = await this.fetchTasks()
    }
}
</script>