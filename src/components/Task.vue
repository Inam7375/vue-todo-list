<template>
    <div 
    :class="[task.reminder ? 'reminder': '', 'task']"
    @dblclick="$emit('toggle-reminder', task.id)">
        <h3 class="task">
            {{task.title}}
            <i 
            class="fas fa-times" 
            @click="$emit('delete-task', task.id)"
            ></i>
        </h3>
        <h5 class="task">
            {{task.date}}
        </h5>
    </div>
</template>

<script>
export default{
    name: "Task",
    props: {
        task: Object
    }
}
</script>

<style scope>
    .fas {
    color: grey;
    }
    .task {
    background: #f4f4f4;
    margin: 5px;
    padding: 10px 20px;
    cursor: pointer;
    }
    .task.reminder {
    border-left: 5px solid green;
    }
    .task h3, h5 {
    display: flex;
    align-items: center;
    justify-content: space-between;
    }
</style>