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
                                <h3 class="text-lg text-gray-900">Editar de una nota</h3>
                                <p class="text-sm text-gray-600">Modulo para editar la nota</p>
                            </div>
                        </div>
                        <div class="md:col-span-2 md:mt-0">
                            <div class="shadow bg-white md:rounded-md p-4">
                                <form @submit.prevent="submit">
                                    <label for="" class="block font-medium text-sm text-gray-700">
                                        Resumen
                                    </label>
                                    <textarea 
                                        class="form-input w-full rounded-md shadow-sm"
                                        v-model="form.extract"
                                    ></textarea>
                                    <label for="" class="block font-medium text-sm text-gray-700">
                                        Contenido
                                    </label>
                                    <textarea 
                                        class="form-input w-full rounded-md shadow-sm"
                                        v-model="form.content"
                                        rows="8"
                                    ></textarea>
                                    <button 
                                        class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-md"
                                    >Editar</button>

                                    <inertia-link :href="route('notes.index')" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-md">
                                    Volver
                                    </inertia-link>
                                </form>

                                <hr class="my-6">

                                <a href="#" @click.prevent="destroy" class="bg-red-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-md">
                                    Eliminar Nota
                                </a>
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
            note: Object
        },
        data() {
            return {
                form: {
                    extract: this.note.extract,
                    content: this.note.content,
                }
            }
        },
        methods: {
            submit() {
                this.$inertia.put(this.route('notes.update', this.note.id), this.form)
            },
            destroy() {
                if (confirm('Desea eliminar?')) {
                    this.$inertia.delete(this.route('notes.destroy', this.note.id))
                }
            }
        }
    }
</script>