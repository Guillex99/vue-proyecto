<template>
    <div>
        <v-card elevation="4">
            <v-container style="padding-left: 2rem;">
                <h2>Filtrar por:</h2>
                <h3>Estado</h3>
                <v-checkbox
                label="Nuevo"
                color="amber darken-4"
                ></v-checkbox>
                <h3>Marca</h3>
                <div>
                    <v-checkbox
                        color="amber darken-4"
                        v-for="marca in marcas" :key="marca"
                        :label="`${marca}`"
                    > 
                    </v-checkbox>
                </div>
                <h3>Sistema</h3>
                <v-checkbox
                    color="amber darken-4"
                    v-for="sistema in sistemas" :key="sistema"
                    :label="`${sistema}`"
                >
                </v-checkbox>
                <h3>Pantalla</h3>
                <v-checkbox
                    color="amber darken-4"
                    v-for="tamanio in tamanios" :key="tamanio"
                    :label="`${tamanio}`"
                >
                </v-checkbox>
            </v-container>
        </v-card>
    </div>
</template>

<script>
    export default {
        name: 'Filtrado',
        data(){
            return{
                marcas:['iPhone','Samsung','Huawei','OnePlus','Xiaomi','Oppo','LG','Vivo'],
                sistemas:['iOS','Android'],
                tamanios:['5"','5,5"','6"','6,5"','7"'],
            }
        }
    }
</script>

