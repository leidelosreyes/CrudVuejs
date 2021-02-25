<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card">
                    <div class="card-header">Example Component</div>

                    <div class="card-body">
                        <div class="form-group">
                            <input type="text" v-model="form.cars_name" class="form-control mb-4">

                            <button @click="submit" >send</button>
                        </div>
                        <table class="table">
  <thead>
    <tr>
      <th scope="col">#</th>
      <th scope="col">Name</th>
      <th scope="col">Actions</th>
    </tr>
  </thead>
  <!-- <tbody>
    <tr v-for="item in crudlist" :key="item.id">
      <th scope="row">{{item.id}}</th>
      <td>{{item.name}}</td>
      <td><button type="button" class="btn btn-primary">Edit</button> <button type="button" class="btn btn-danger">Delete</button></td>
      
    </tr>
  </tbody> -->
</table>

                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
            data(){
                return{
                    form:{
                        cars_name:null
                    }
                }

            },

            methods: 
            {
                submit()
                {
                    axios.post('cruds',this.form) 
                .then(function(response){
                 
                alert('success');
              })
                     
                            // axios.post('/cruds',this.form)
                            //     .then(function (response){
                            //         alert('success');
                            //     })
                                
                            //     .catch(function (error) {
                            //         console.log(error);
                            //     });



                }
                    
            }

    }
</script>


