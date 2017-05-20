<template>
    <div class="container">
        <div class="row">
            <div class="col-md-8 col-md-offset-2">
                <div class="panel panel-default">
                    <div class="panel-heading">Creando Nota</div>

                    <div class="panel-body">
                       <form @submit.prevent="addNote">
												 <div class="form-group">
													 <label>Titulo</label>
													 <input type="text" class="form-control" v-model="noteData.title" >
												 </div>
												 <div class="form-group">
													 <label>Descripcion De la Nota</label>
													 <input type="text" class="form-control" v-model="noteData.body">
												 </div>
												 <button type="submit" class="btn btn-primary pull-right">Crear Nota</button>
                       </form>
                    </div>
											 <hr>
											 
	<div class="panel panel-default" v-for="indexData in note">
		<div class="panel-heading">
			<strong>{{ indexData.title }}</strong>
		</div>
	
		<div class="panel-body">
			<strong>{{ indexData.body }}</strong>
		</div>
	</div>

                </div>
            </div>
        </div>
    </div>
</template>
<style>

</style>
<script>
    export default {
			data () {
					return{
						noteData:{
							title:'',
							body:''
						},
						note: []	
					}
			},
			created () {
				this.fetchnote();
			},
        methods: {
					addNote() {
					axios.post('/api/notes', this.noteData)
						.then(response => {
							this.noteData="";
							console.log(this.note)
							this.note.push(response.data);
						});
				},
					fetchnote() {
         		 axios.get('/api/notes')
							.then(response => {
								//console.log(response);
								this.note = response.data.note;
							});
					},
          ready() {
                this.fetchnote();
          }
      }
   }
</script>