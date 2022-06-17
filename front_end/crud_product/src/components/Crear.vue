<template>
    <div class="container col-md-6">
        <div class="card">
            <h5 class="card-header">Agregar Producto</h5>
            <div class="card-body">
                <form v-on:submit.prevent="agregarRegistro()">
                    <div class="mb-3">
                        <label for="name" class="form-label">Nombre:</label>
                        <input name="name" v-model="producto.name" type="text" placeholder="nombre" class="form-control" id="name"
                            aria-describedby="nombre">
                    </div>
                    <div class="mb-3">
                        <label for="category" class="form-label">Category:</label>
                        <select name="category" v-model="producto.category" class="mb-3 form-control" aria-label="select category">
                            <option value="">Seleccionar...</option>
                            <option value="bebidas">bebidas</option>
                            <option value="panadería">panadería</option>
                            <option value="pastelería">pastelería</option>
                            <option value="postres">postres</option>
                            <option value="tortas">tortas</option>
                        </select>
                    </div>
                    <div class="mb-3">
                        <label for="reference" class="form-label">Reference:</label>
                        <select name="reference" v-model="producto.reference" class="mb-3 form-control" aria-label="select reference">
                            <option value="">Seleccionar...</option>
                            <option value="250ml">250ml</option>
                            <option value="500ml">500ml</option>
                            <option value="600ml">600ml</option>
                            <option value="1l">1l</option>
                            <option value="1.5l">1.5l</option>
                            <option value="und[s]">und[s]</option>
                            <option value="libra[s]">libra[s]</option>
                            <option value="kilo[s]">kilo[s]</option>
                        </select>
                    </div>
                    <div class="mb-3">
                        <label for="stock" class="form-label">Stock:</label>
                        <input type="number" v-model="producto.stock" placeholder="stock" class="form-control" id="stock" name="stock"
                            aria-describedby="stock">
                    </div>
                    <div class="mb-3">
                        <label for="price" class="form-label">Precio:</label>
                        <input type="number" v-model="producto.price" placeholder="price" class="form-control" id="price" name="price"
                            aria-describedby="precio">
                    </div>
                    <div class="bnt-group" role="group">
                        <button class="btn btn-success align-left" type="submit">agregar</button>
                        <button class="btn btn-danger align-right" type="">cancelar</button>
                    </div>
                </form>
            </div>
        </div>
    </div>
</template>
<script>
export default {

    data(){
        return {
            producto: {

            }
        }
    },
    methods:{
        agregarRegistro(){
            
            const optionsRequest = {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify(this.producto)
            }

            fetch("http://localhost:8000/api/product_create",optionsRequest)
            .then(response => response.json())
            .then((data) => {
                console.log(data); 
                window.location.href = 'listar' 
            })
            .catch(console.log)
    

        }
    }
}
</script>