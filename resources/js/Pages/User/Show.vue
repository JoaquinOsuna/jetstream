<template>
    <app-layout title="Dashboard">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Create User
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-xl sm:rounded-lg">
                    <div class="p-6 sm:px-20 bg-white border-b border-gray-200">
                        
                        <form @submit.prevent="submit" action="">
                            <div class="mt-4">
                                <jet-label for="" :value="'Nombre: ' + customer.name"/>
                                <jet-label for="" :value="'Email: ' + customer.email"/>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </app-layout>
</template>

<script>
    import { defineComponent } from 'vue'
    import AppLayout from '@/Layouts/AppLayout.vue'
    import JetLabel from '@/Jetstream/Label'
    import { Inertia } from '@inertiajs/inertia'
   

    export default defineComponent({
        props:['customer'],
        components: {
            AppLayout,
            JetLabel
        
        },
    })
</script>

