<template>
    <div class="container">
    <div class="row mt-5">
     <div class="col-md-12">
            <div class="card">
              <div class="card-header">
                <h3 class="card-title">Edge Consultancy</h3>

                <div class="card-tools">
                  <button class="btn btn-success" data-toggle="modal" data-target="#addNew">Add User <i class="fa fa-user-plus fa-fw"></i></button>
                </div>
              </div>
              <!-- /.card-header -->
              <div class="card-body table-responsive p-0">
                <table class="table table-hover">
                  <tbody><tr>
                    <th>ID</th>
                    <th>Name</th>
                    <th>Email</th>
                    <th>Type</th>
                    <th>Bio</th>
                    <th>Data</th>
                    <th>Modify</th>

                  </tr>
                  <tr v-for="user in users" :key="user.id">

                    <td>{{user.id}}</td>
                    <td>{{user.name}}</td>
                    <td>{{user.email}}</td>
                    <th>{{user.type | upText}}</th>
                    <td>{{user.bio}}</td>
                    <th>{{user.created_at | myDate}}</th>
                    <td>
                        <a href="">
                            <i class="fa fa-edit blue"></i>
                        </a>
                        /
                        <a href="">
                            <i class="fa fa-trash red"></i>
                        </a>
                    </td>
                  </tr>

                </tbody></table>
              </div>
              <!-- /.card-body -->
            </div>
            <!-- /.card -->
          </div>
          </div>

          <!-- Modal -->
        <div class="modal fade" id="addNew" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog modal-dialog-centered" role="document">
            <div class="modal-content">
            <div class="modal-header">
                <h5 class="modal-title" id="addNew">Add New</h5>
                <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                <span aria-hidden="true">&times;</span>
                </button>
            </div>
            <div class="modal-body">

              <form @submit.prevent="createUser">
                <div class="form-group">
                    <input v-model="form.name" type="text" name="name" placeholder="name"
                      class="form-control" :class="{ 'is-invalid': form.errors.has('name') }">
                    <has-error :form="form" field="name"></has-error>
                </div>

                <div class="form-group">
                    <input v-model="form.email" type="text" name="email" placeholder="email"
                      class="form-control" :class="{ 'is-invalid': form.errors.has('email') }">
                    <has-error :form="form" field="email"></has-error>
                </div>

                <div class="form-group">
                    <textarea v-model="form.bio" type="text" name="bio" placeholder="bio"
                      class="form-control" :class="{ 'is-invalid': form.errors.has('bio') }"></textarea>
                    <has-error :form="form" field="bio"></has-error>
                </div>

                <div class="form-group">
                    <select v-model="form.type" type="text" name="type" placeholder="type"
                      class="form-control" :class="{ 'is-invalid': form.errors.has('type') }">
                      <option value="">Select User Role</option>
                      <option value="admin">Admin</option>
                      <option value="Standard">Standard User</option>
                      <!-- <option value="Author">Author</option> -->
                    </select>
                    <has-error :form="form" field="type"></has-error>
                </div>

                <div class="form-group">
                    <input v-model="form.password" type="password" name="password" placeholder="password"
                      class="form-control" :class="{ 'is-invalid': form.errors.has('password') }">
                    <has-error :form="form" field="password"></has-error>
                </div>

                <div class="modal-footer">
                    <button type="button" class="btn btn-danger" data-dismiss="modal">Close</button>
                    <button type="submit" class="btn btn-primary">Create</button>
                </div>

              </form>

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
          users: {},
          form:new Form({
            name: '',
            email: '',
            user_type:'',
            password: ''
           
          })

        }
      },
      methods:{
        loadUsers(){
          axios.get("api/user").then(({data}) => (this.users = data.data));
        },
        createUser(){
           this.$Progress.start();
           this.form.post('api/user');
           toast({
           type: 'success',
           title: 'User Created in successfully'
         })

           this.$Progress.finish();
        }
      },
        created() {
            this.loadUsers();
        }
    }
</script>
