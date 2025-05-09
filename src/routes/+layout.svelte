<!-- src/routes/+layout.svelte -->
<script>
    import { page } from '$app/stores';
    import '../app.css';

    import yaml from 'js-yaml';

	let fileInput;

	function handleLoad() {
		fileInput.click();
	}

	async function handleFileChange(event) {
		const file = event.target.files[0];
		if (!file) return;

		const reader = new FileReader();

		reader.onload = (e) => {
			try {
				const contents = e.target.result;
				const data = yaml.load(contents);
				console.log('Parsed YAML:', data);
			} catch (error) {
				console.error('Error parsing YAML:', error);
			}
		};

		reader.readAsText(file);
	}

/*
    function handleLoad() {
        //alert('Load File!');
        const parsedData = yaml.load(rawData);
        console.log(parsedData);
    }
*/
    function handleSave() {
        alert('Save File!');
    }

</script>
  


  <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
    <div class="container-fluid">
      <a class="navbar-brand" href="/">pygeoapi configurator</a>
      <button class="navbar-toggler" type="button" aria-label="Toggle navigation" data-bs-toggle="collapse" data-bs-target="#navbarNav">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
          <li class="nav-item">
            <a class="nav-link" href="/">Home</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="/server">Server</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="/metadata">Metadata</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="/resources">Resources</a>
          </li>
        </ul>
      </div>
      <div>
      <button class="btn btn-light" on:click={handleLoad}>
        Load File
       </button>
       <input
           type="file"
           bind:this={fileInput}
           on:change={handleFileChange}
           style="display: none"
       />


       <button class="btn btn-light" on:click={handleSave}>
        Save File
       </button>
    </div>
    </div>
  </nav>
  
  <main class="container mt-4">
    <slot />
    <footer class="bg-light text-muted text-center py-3 fixed-bottom">
        Brought to you with ❤️ by <a href="https://byteroad.net">ByteRoad</a>.
      </footer>
  </main>
  