<template>
    <app-layout title="Dashboard">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                User
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-xl sm:rounded-lg">
                    <div class="p-6 sm:px-20 bg-white border-b border-gray-200">

                        <Link :href="route('user.create')">Crear Usuario</Link>
                        <table class="table-auto w-full">
                            <thead>
                                <tr>
                                    <th class="p-3">Id</th>
                                    <th class="p-3">Nombre</th>
                                    <th class="p-3">Email</th>
                                    <th class="p-3">Acciones</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="u in users" :key="u.id">
                                    <td class="p-3">{{ u.id }}</td>
                                    <td class="p-3">{{ u.name }}</td>
                                    <td class="p-3">{{ u.email }}</td>
                                    <td class="p-3">
                                        <Link :href="route('user.show',{'customer':u})">Ver</Link>
                                        <Link :href="route('user.edit',{'customer':u})">Editar</Link>

                                        <!-- <Link :href="route('user.destroy',{'customer':u})" method="DELETE">Borrar</Link> -->
                                        <button @click="modalOpen=true;selectedUser=u">Borrar</button>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>

    <jet-dialog-modal :show="modalOpen">

        <template v-slot:title>
           <h1>Eliminar Usuario</h1>
        </template>
         <template v-slot:content>
           <p v-if="selectedUser">Seguro que quieres eliminar el usuario: {{ selectedUser.email }}</p>
        </template>
         <template v-slot:footer>
           <jet-button class="bg-red-500 hover:bg-red-800 float-left" @click="deleteUser()">
               Eliminar
           </jet-button>
           <jet-button class="bg-green-500 hover:bg-green-800" @click="modalOpen = false">
               Cerrar
           </jet-button>
        </template>
    </jet-dialog-modal>
    </app-layout>
</template>

<script>
    import { defineComponent } from 'vue'
    import AppLayout from '@/Layouts/AppLayout.vue'
    import { Link } from '@inertiajs/inertia-vue3'
    import { Inertia } from '@inertiajs/inertia'
    import JetDialogModal from "@/Jetstream/DialogModal"
    import JetButton from "@/Jetstream/Button"

    export default defineComponent({
        props:['users'],
        data(){
            return {
                modalOpen:false,
                selectedUser: Object
            }
        },
        components: {
            AppLayout,
            Link,
            JetDialogModal,
            JetButton
        
        },
        methods:{
            deleteUser: function(data){
                // if(!confirm("¿Seguro que quieres eliminar el usuario: " +data.email+"?"))return;
                Inertia.delete(route("user.destroy", {customer:this.selectedUser}));
                this.modalOpen = false;

            }
        },
    })
</script>

