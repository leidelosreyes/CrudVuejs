<template>
<div>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card">
                    <div class="card-header">Example Component</div>

                    <div class="card-body">
                        <div class="form-group">
                            <input type="text" class="form-control mb-4" v-model="form.name">
                            <input type="button" value="submit" @click="submit" class="btn btn-primary">
                        </div>
                        <table class="table">
  <thead>
    <tr>
      <th scope="col">#</th>
      <th scope="col">Name</th>
      <th scope="col">Actions</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(item,index) in crudlist" :key="item.id">
      <th scope="row">{{item.id}}</th>
      <td>{{item.name}}</td>
      <td><button type="button" class="btn btn-primary" @click="edit(item)" >Edit</button> <button type="button" @click="remove(item,index)" class="btn btn-danger">Delete</button></td>
      
    </tr>
  </tbody>
</table>

                    </div>
                </div>
            </div>
        </div>

        <!-- modal -->
         
                    <div class="modal" id="editmodal" tabindex="-1" role="dialog">
                        <div class="modal-dialog" role="document">
                            <div class="modal-content">
                            <div class="modal-header">
                                <h5 class="modal-title">Modal title</h5>
                                <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                                <span aria-hidden="true">&times;</span>
                                </button>
                            </div>
                            <div class="modal-body">
                               <div class="form-group">
                                    <input type="text" class="form-control mb-4" v-model="form_edit.name">
                               </div>
                            </div>
                            <div class="modal-footer">
                                <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
                                <button type="button" class="btn btn-primary" @click="update()">Save changes</button>
                            </div>
                            </div>
                        </div>
                        </div>
    </div>
</div>    
</template>

<script>
    export default {
           props: ['crud'],
    data(){

        return{
            crudlist: this.crud,
             form:{
                 name:null
             },
             form_edit:
             {
                 name:null
             },
             selectedId:null
            

        }
    },

    methods:{
        submit(){
              const vm = this;
            axios.post('cruds',this.form) 
                .then(function(response){
                  vm.crudlist.push(response.data);
                  vm.form.name = null
                
              })
              .catch(function(error){
                  alert("error")
              });
          
           

        },

        remove(item,index)
        {
               const vm = this;
            axios.delete(`cruds/${item.id}`) 
                .then(function(response){
                  vm.crudlist.splice(index,1);
                 
                
              })
              .catch(function(error){
                  alert("error")
              });

        },

        edit(item)
        {       const vm = this;
                $('#editmodal').modal('show');
                vm.form_edit.name = item.name;
                this.selectedId = item.id;
        },

        update()
        {
                 const vm = this;
            axios.put(`cruds/${vm.selectedId}`,this.form_edit) 
                .then(function(response){
                    alert("Successfuly Update")
                //   location.reload();
                
              })
              .catch(function(error){
                  alert("error")
              });
        }

    
       }

    }
</script>


