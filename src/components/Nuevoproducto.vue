<!--Componente para nuevo producto-->
<template>
  <div>
    <div
      class="text-center amber--text"
      style="
        text-transform: uppercase;
        padding-top: 1rem;
        padding-bottom: 1.5rem;
      "
    >
      <h2>Agregar Imagenes</h2>
    </div>
    <v-row>
      <v-col cols="12" md="6" lg="6" cl="6">
        <v-form ref="form" v-model="valid" lazy-validation>
          <v-radio-group v-model="estado">
            <v-radio :label="`Nuevo`" :value="Nuevo"></v-radio>
            <v-radio :label="`Usado`" :value="Usado"></v-radio>
          </v-radio-group>

          <v-text-field
            v-model="marca"
            :rules="marcaRules"
            label="Marca"
            required
          ></v-text-field>

          <v-text-field
            v-model="modelo"
            :rules="modeloRules"
            label="Modelo"
            required
          ></v-text-field>

          <v-text-field
            v-model="pantalla"
            :rules="pantallaRules"
            label="Pantalla en pulgadas"
            required
          ></v-text-field>

          <v-select
            v-model="sistema"
            :items="items"
            :rules="[(v) => !!v || 'Sistema es obligatorio']"
            label="Sistema"
            required
          ></v-select>

          <v-text-field
            v-model="rom"
            :rules="romRules"
            label="ROM"
            required
          ></v-text-field>

          <v-text-field
            v-model="ram"
            :rules="ramRules"
            label="RAM"
            required
          ></v-text-field>

          <v-text-field
            v-model="descripcion"
            :rules="descripcionRules"
            label="Descripción"
            required
          ></v-text-field>

          <v-text-field
            v-model="vendedor"
            :rules="vendedorRules"
            label="Vendedor"
            required
          ></v-text-field>

          <v-text-field
            v-model="telefono_vendedor"
            :rules="telefonoRules"
            label="Teléfono"
            required
          ></v-text-field>
          <v-text-field
            v-model="titulo"
            :rules="tituloRules"
            label="Titulo"
            required
          ></v-text-field>
          <v-text-field
            v-model="precio"
            :rules="precioRules"
            label="Precio $"
            required
          ></v-text-field>

          <v-btn
            color="success"
            class="mr-4"
            @click="agregar()"
            :disabled="agregado == true"
          >
            Guardar
          </v-btn>

          <v-btn color="amber white--text" class="mr-4" @click="cancelar()">
            Resetear
          </v-btn>
        </v-form>
      </v-col>
      <v-col cols="12" md="6" lg="6" xl="6">
        <div>
          <v-row>
            <v-col cols="12" class="text-center">
              <span
                class="subtitle-1 amber--text"
                style="text-transform: uppercase; font-weight: bold"
                >Subir Imagenes</span
              >
            </v-col>
            <v-col cols="12" md="6">
              <v-file-input
                v-show="agregado == false"
                v-model="file"
                multiple
                label="Agregar Imagen"
                accept="image/*"
              ></v-file-input>
              <v-btn :disabled="file == null" @click="upload()">Subir</v-btn>
              <v-carousel>
                <v-carousel-item
                  v-for="(imagen, i) in imagenesUrl"
                  :key="i"
                  :src="imagen"
                  reverse-transition="fade-transition"
                  transition="fade-transition"
                ></v-carousel-item>
              </v-carousel>
            </v-col>
            <v-col cols="12" md="6" class="hidden-sm-and-down">
              <v-simple-table>
                <template v-slot:default>
                  <thead>
                    <tr>
                      <th class="text-left">Nombre</th>
                      <th class="text-left">Tamaño</th>
                      <th class="text-left">-</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="(item, key) in imagenes" :key="key">
                      <td>{{ item }}</td>
                      <td></td>
                      <td>
                        <v-btn @click="eliminarImagen(key)">Borrar</v-btn>
                      </td>
                    </tr>
                  </tbody>
                </template>
              </v-simple-table>
            </v-col>
          </v-row>
        </div>
      </v-col>
    </v-row>
  </div>
</template>
<script>
export default {
  name: "Nuevoproducto",
};
</script>

<script>
export default {
  data: () => ({
    valid: true,
    marca: "",
    marcaRules: [
      (v) => !!v || "Marca es obligatorio",
      (v) =>
        (v && v.length <= 10) || "Marca debe de tener maximo 10 caracteres",
    ],
    modelo: "",
    modeloRules: [
      (v) => !!v || "Modelo es obligatorio",
      (v) =>
        (v && v.length <= 20) || "Modelo debe de tener maximo 20 caracteres",
    ],
    pantalla: "",
    pantallaRules: [(v) => !!v || "Pantalla es obligatorio"],
    rom: "",
    romRules: [(v) => !!v || "ROM es obligatorio"],
    ram: "",
    ramRules: [(v) => !!v || "RAM es obligatorio"],
    descripcion: "",
    descripcionRules: [(v) => !!v || "Descripción es obligatorio"],
    vendedor: "",
    vendedorRules: [(v) => !!v || "Vendedor es obligatorio"],
    telefono_vendedor: "",
    telefonoRules: [(v) => !!v || "Telefono es obligatorio"],
    titulo: "",
    tituloRules: [(v) => !!v || "Titulo es obligatorio"],
    precio: "",
    precioRules: [(v) => !!v || "Precio es obligatorio"],
    sistema: null,
    items: ["Item 1", "Item 2", "Item 3", "Item 4"],
    checkbox: false,
  }),
  methods: {
    validate() {
      this.$refs.form.validate();
    },
    reset() {
      this.$refs.form.reset();
    },
  },
};
</script>

<script>
import { db } from "../db.js";
import { st } from "../db.js";
export default {
  data() {
    return {
      estado: "Nuevo",
      nid: 1,
      titulo: null,
      descripcion: null,
      estado: null,
      marca: null,
      modelo: null,
      pantalla: null,
      precio: null,
      ram: null,
      rom: null,
      sistema: null,
      telefono_vendedor: null,
      vendedor: null,
      fecha: new Date().toLocaleDateString(),
      borrado: false,
      file: null,
      downloadURL: "",
      fileName: "",
      imagenes: [],
      imagenesUrl: [],
      imagen: null,
      items: ["Android", "iOS"],
      productos: [],
      agregado: false,
    };
  },
  methods: {
    agregar() {
      let nuevo = {
        estado: this.estado,
        nid: this.nid,
        titulo: this.titulo,
        descripcion: this.descripcion,
        estado: this.estado,
        marca: this.marca,
        modelo: this.modelo,
        pantalla: this.pantalla,
        precio: parseFloat(this.precio),
        ram: this.ram,
        rom: this.rom,
        sistema: this.sistema,
        telefono_vendedor: this.telefono_vendedor,
        vendedor: this.vendedor,
        imagenes: this.imagenesUrl,
        fecha: this.fecha,
      };
      db.collection("celulares").add(nuevo);
      this.agregado = true;
      this.titulo = null;
      this.descripcion = null;
      this.estado = null;
      this.marca = null;
      this.modelo = null;
      this.pantalla = null;
      this.precio = null;
      this.ram = null;
      this.rom = null;
      this.sistema = null;
      this.telefono_vendedor = null;
      this.vendedor = null;
      this.imagenesUrl = [];
      (this.fecha = new Date()), (this.nid = null), this.listarImagenes();
    },
    cancelar() {
      this.titulo = null;
      this.descripcion = null;
      this.estado = null;
      this.marca = null;
      this.modelo = null;
      this.pantalla = null;
      this.precio = null;
      this.ram = null;
      this.rom = null;
      this.sistema = null;
      this.telefono_vendedor = null;
      this.vendedor = null;
      this.imagenesUrl = [];
      this.imagenes = [];
      this.fecha = new Date();
      this.nid = null;
      this.borrado = false;
      this.limpiarCarpeta();
    },
    validacionID() {
      db.collection("celulares")
        .get()
        .then((res) => {
          res.forEach((item) => {
            this.productos.push(item.data());
          });
        });
      if (this.productos.length === 0) {
        this.nid = 1;
      } else {
        this.nid = this.productos.length + 1;
      }
      console.log(this.nid);
    },
    limpiarCarpeta() {
      // let images = [];
      st.ref()
        .child("IDanuncio/" + this.nid + "/")
        .listAll()
        .then((res) => {
          let x = res.items.length;
          // carpeta nueva
          if (this.borrado === false && x === 0) {
            this.borrado = true;
            // carpeta existente con imagenes
          } else if (this.borrado === false && x > 0) {
            for (let i = 0; i < x; i++) {
              st.ref(
                "IDanuncio/" + this.nid + "/" + res.items[i].name
              ).delete();
            }
            this.borrado = true;
            // misma carpeta con imagenes
          }
        });
    },
    upload() {
      let bandera = true;
      this.fileName = this.file[0].name;
      this.limpiarCarpeta();
      let carpeta = "IDanuncio/" + this.nid + "/" + this.fileName;
      var archivo = st.ref(carpeta);
      archivo
        .put(this.file[0])
        .then(() => {
          archivo.getDownloadURL().then((url) => {
            this.downloadURL = url;
            for (let nombre in this.imagenes) {
              if (this.imagenes[nombre] == this.fileName) {
                bandera = false;
                let ultimo = Object.keys(this.imagenesUrl).length;
                this.imagenesUrl.push(this.downloadURL);
                this.imagenesUrl[nombre] = this.imagenesUrl[ultimo];
                this.imagenesUrl.pop(this.downloadURL);
              }
            }
            this.file = null;
            this.fileName = "";

            if (bandera == true) {
              this.imagenesUrl.push(this.downloadURL);
              this.listarImagenes();
            } else {
              this.listarImagenes();
            }
          });
        })
        .catch((error) => {
          console.log(error);
        });
    },
    eliminarImagen(index) {
      this.imagenesUrl.splice(index, 1);
      st.ref("IDanuncio/" + this.nid + "/" + this.imagenes.splice(index, 1))
        .delete()
        .then(() => {
          this.downloadURL = "";
        })
        .catch((error) => {
          console.log(error);
        });
      this.file = null;
      this.fileName = "";
    },
    listarImagenes() {
      var this2 = this;
      this2.imagenes = [];
      st.ref()
        .child("IDanuncio/" + this2.nid + "/")
        .listAll()
        .then((res) => {
          res.items.forEach(function (itemRef) {
            /* console.log(itemRef.tamanio) */
            this2.imagenes.push(itemRef.name);
          });
        })
        .catch((error) => {
          console.log(error);
        });
      this.imagenesUrl.sort();
    },
  },
  mounted() {
    this.validacionID;
  },
};
</script>





