<script>
	// `lang="javascript"`
	let notes = [
        {
			id: 1,
			accountname: "Current",
			email : "deepak@gmail.com",
			mobile : "9878652310",
			description :"My Self JAI HIND",
			date:new Date(),
		 }
		]; 
		// Data to be input by fields
	let data = {
		accountname: "",
		email : "",
		mobile : "",
		description :"",
		date:new Date(),
		id: null
	}
	   // Add note data function
		let addNote = () => {
        const newNote = {
          id: notes.length + 1,
		  accountname:data.accountname,
          email: data.email,
          mobile: data.mobile,
          description: data.description,
          date: data.date,
		};
		
        notes = notes.concat(newNote);
        data = {
          id: null,
          accountname: "",
          email : "",
		  mobile : "",
		  description :"",
		  date:"",
        };
        // console.log(notes);
	  };
	  

	  // Delete a note function

	  let deleteNote=(id)=>{
	    notes = notes.filter(note => note.id !== id);
	  };
	
  // Editing a note
    let isEdit=false;
    let editNote =(note)=>{
		 isEdit=true;
		 data=note;
	};
  // Updating a note

  let updateNote = () => {
    isEdit = !isEdit;
    let noteDB = {
		  accountname:data.accountname,
          email: data.email,
          mobile: data.mobile,
          description: data.description,
		  date: data.date,
		  id: data.id
    };
  
	let objIndex = notes.findIndex(obj => obj.id == noteDB.id);
    // console.log("Before update: ", notes[objIndex]);
    notes[objIndex] = noteDB;
    data = {
		  id: null,
          accountname: "",
          email : "",
		  mobile : "",
		  description :"",
		  date:"",
    };
  };

</script>






<style>
  @import url("https://fonts.googleapis.com/css?family=Nunito&display=swap");
  * {
    font-family: "Nunito", sans-serif;
  }
</style>


<section>
  <div class="container">
	  <h2 class="text-center text-uppercase text-warning my-3">Svelte CRUD APP</h2>
    <div class="row mt-5">
      <div class="col-md-6">
        <div class="card p-2 shadow">
          <div class="card-body">
            <h5 class="card-title mb-4">Svelte CRUD App</h5>
            <form>
              <div class="form-group">
                <label for="title">Account name</label>
				<input
				  bind:value={data.accountname}
                  type="text"
                  class="form-control"
                  id="text"
                  placeholder="Enter Your Account Name"/>
              </div>
              <div class="form-group">
                <label for="category">Email</label>
					<input
					bind:value={data.email}
					type="email"
					class="form-control"
					id="email"
					placeholder="Enter Your Email" />
              </div>
              <div class="form-group">
                <label for="content">Mob No</label>
					<input
					bind:value={data.mobile}
					type="number"
					class="form-control"
					id="number"
					placeholder="Enter Your Mobile No" />
			  </div>
			  <div class="form-group">
                <label for="content">Description</label>
					<textarea
					bind:value={data.description}
					class="form-control"
					id="content"
					rows="3"
					placeholder="Enter Your Description Here" />
			  </div>
			  <div class="form-group">
                <label for="content">Date</label>
					<input
					bind:value={data.date}
					type="date"
					class="form-control"
					id="date"
					placeholder="Enter Date" />
			  </div>

              {#if isEdit === false}
                 <button type="submit" on:click|preventDefault={addNote} class="btn btn-success">Add Note</button>
              {:else}
                  <button type="submit" on:click|preventDefault={updateNote} class="btn btn-info">Edit Note</button>
              {/if}

            </form>
          </div>
        </div>
      </div>
	
	  <div class="col-md-6">
		{#each notes as note}
			<div class="card mb-3">
			<div class="card-header">{note.accountname}</div>
			<div class="card-body">
				<h5 class="card-title">{note.email}</h5>
				<p class="card-text">{note.mobile}</p>
				<p class="card-text">{note.description}</p>
				<p class="card-text">{note.date}</p>
				<button on:click={editNote(note)} class="btn btn-info">Edit</button>
				<button on:click={deleteNote(note.id)} class="btn btn-danger">Delete</button>
			</div>
			</div>
	  {/each}
  </div>
</section>