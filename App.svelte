<script>
  // Array to store healthcare services
  let services = [
    { id: 1, name: "General Checkup", description: "Routine general checkup", price: 50 },
    { id: 2, name: "Dental Cleaning", description: "Professional dental cleaning", price: 80 }
  ];

  let newService = { name: "", description: "", price: "" };

  // Function to add new service
  function addService() {
    if (newService.name && newService.description && newService.price) {
      services = [...services, { ...newService, id: Date.now() }];
      newService = { name: "", description: "", price: "" };
    } else {
      alert("Please fill out all fields");
    }
  }

  // Function to delete service
  function deleteService(id) {
    services = services.filter(service => service.id !== id);
  }

  // Function to update service
  let editingService = null;

  function editService(service) {
    editingService = { ...service };
  }

  function updateService() {
    if (editingService.name && editingService.description && editingService.price) {
      services = services.map(service =>
        service.id === editingService.id ? editingService : service
      );
      editingService = null;
    } else {
      alert("Please fill out all fields");
    }
  }
</script>

<div class="background-container">
<h1>Healthcare Services</h1>

<!-- Display List of Services -->
<ul>
  {#each services as service}
    <li>
      <strong>{service.name}</strong> - {service.description} (${service.price})
      <button on:click={() => editService(service)}>Edit</button>
      <button on:click={() => deleteService(service.id)}>Delete</button>
    </li>
  {/each}
</ul>

<!-- Form to Add New Service -->
<h2>Add New Service</h2>
<form on:submit|preventDefault={addService}>
  <input type="text" placeholder="Name" bind:value={newService.name} />
  <input type="text" placeholder="Description" bind:value={newService.description} />
  <input type="number" placeholder="Price" bind:value={newService.price} />
  <button type="submit">Add Service</button>
</form>

<!-- Form to Edit Existing Service -->
{#if editingService}
  <h2>Edit Service</h2>
  <form on:submit|preventDefault={updateService}>
    <input type="text" placeholder="Name" bind:value={editingService.name} />
    <input type="text" placeholder="Description" bind:value={editingService.description} />
    <input type="number" placeholder="Price" bind:value={editingService.price} />
    <button type="submit">Update Service</button>
    <button on:click={() => (editingService = null)}>Cancel</button>
  </form>
{/if}
</div>

<style>
 .background-container {
    background-image: url('https://img.hcinnovationgroup.com/files/base/ebm/hci/image/2020/09/dreamstime_xl_168582340.5f590ad631297.png?auto=format,compress&fit=fill&fill=blur&w=1200&h=630');
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
    min-height: 100vh;
    padding: 20px;
    color: white;
  }

h1, h2 {
    text-align: center;
  }

  /* Rest of your app styles */
  ul {
    list-style: none;
    padding: 0;
  }

  li {
    margin-bottom: 1rem;
  }


  form {
    margin-bottom: 1rem;
  }

  ul {
    list-style: none;
    padding: 0;
  }

  li {
    margin-bottom: 1rem;
  }

  button {
    margin-left: 0.5rem;
  } 
</style>
