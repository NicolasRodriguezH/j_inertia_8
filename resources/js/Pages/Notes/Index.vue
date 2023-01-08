<template>
    <AppLayout title="Dashboard">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Modulo Notas
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-xl sm:rounded-lg">
                    <div class="md:grid md:grid-cols-3 md:gap-6">
                        <div class="md:col-span-1">
                            <div class="px-4 sm:px0">
                                <h3 class="text-lg text-gray-900">Listado de notas</h3>
                                <p class="text-sm text-gray-600">Toma un registro y ejecuta cualquier funcion de CRUD</p>
                            </div>
                        </div>
                        <div class="md:col-span-2 md:mt-0">
                            <div class="shadow bg-white md:rounded-md p-4">
                                <div class="flex justify-between ">
                                    <!-- Esta es la caja y su nombre o ID es "q" -->
                                    <input type="text" class="form-input rounded-md shadow-sm" placeholder="Buscar..." v-model="q">

                                    <inertia-link :href="route('notes.create')" class="bg-blue-500 text-white font-bold py-2 px-4 rounded">
                                        Crear
                                    </inertia-link>
                                </div>
                                <hr class="my-6">
                                <table>
                                    <tr v-for="note in notes">
                                        <td class="border px-4 py-2">
                                            {{ note.extract }}
                                        </td>
                                        <td class="px-4 py-2">
                                            <inertia-link :href="route('notes.show', note.id)" class="bg-gray-500 hover:bg-gray-700 text-white font-bold py-2 px-4 rounded-md">
                                                Ver
                                            </inertia-link>
                                        </td>
                                        <td class="px-4 py-2">
                                            <inertia-link :href="route('notes.edit', note.id)" class="bg-green-500 hover:bg-green-700 text-white font-bold py-2 px-4 rounded-md">
                                                Editar
                                            </inertia-link>
                                        </td>
                                    </tr>
                                </table>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </AppLayout>
</template>

<script>
    import AppLayout from '@/Layouts/AppLayout.vue'

    export default {
        components: {
            AppLayout
        },
        props: {
            notes: Array,
        },
        data() {
            return {
                q: ''
            }
        },
        watch: {
            q: function(value) {
                this.$inertia.replace(this.route('notes.index', {q: value}))
            }
        }
    }
    /* const props = defineProps({
        notes : Array,
    }); */
</script>