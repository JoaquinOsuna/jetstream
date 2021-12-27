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
                                <jet-label for="" value="Nombre"/>
                                <jet-input class="mt-1 block w-full" type="text" v-model="form.name"/>
                                <jet-input-error :message="errors.name"/>
                            </div>

                            <div class="mt-4">
                            <jet-label for="" value="Apellido"/>
                            <jet-input class="mt-1 block w-full" type="text" v-model="form.email"/>
                            <jet-input-error :message="errors.email"/>
                            </div>

                            <div class="mt-4">
                            <jet-label for="" value="Password"/>
                            <jet-input class="mt-1 block w-full" type="password" v-model="form.password"/>
                            <jet-input-error :message="errors.password"/>
                            </div>

                            <jet-button type="submit" class="mt-4">Enviar</jet-button>
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
    import JetInputError from '@/Jetstream/InputError'
    import JetInput from '@/Jetstream/Input'
    import JetLabel from '@/Jetstream/Label'
    import JetButton from '@/Jetstream/Button'
    import { Inertia } from '@inertiajs/inertia'
   

    export default defineComponent({
        props:['errors'],
        data(){
            return{
               form: {
                    name: "",
                    email: "",
                    password: "",     
               }           
            }
        },
        components: {
            AppLayout,
            JetInputError,
            JetInput,
            JetLabel,
            JetButton
        
        },
        methods: {
            submit(){
                Inertia.post(route('user.store'),this.form);
            }
        }
    })
</script>

