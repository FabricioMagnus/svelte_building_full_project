<script>
  import ContactCard from "./ContactCard.svelte";

  let name = "Fabricio";
  let title = "";
  let image = "https://cdn-icons-png.flaticon.com/512/3135/3135715.png";
  let description = "";
  let formState = "empty";

  let createdContact = [];

  function addContact() {
    if (
      name.trim().length === 0 ||
      title.trim().length === 0 ||
      image.trim().length === 0 ||
      description.trim().length === 0
    ) {
      formState = "invalid";
      return;
    }
    formState = "done";
    createdContact = [
      ...createdContact,
      {
        id: Math.random(),
        name: name,
        jobTitle: title,
        imageURL: image,
        desc: description,
      },
    ];
  }

  function deleteFirst() {
    createdContact = createdContact.slice(1);
  }

  function deleteLast() {
    createdContact = createdContact.slice(0, -1);
  }
</script>

<div id="form">
  <div class="form-control">
    <label for="userName">User Name</label>
    <input type="text" bind:value={name} id="userName" />
  </div>
  <div class="form-control">
    <label for="jobTitle">Job Title</label>
    <input type="text" bind:value={title} id="jobTitle" />
  </div>
  <div class="form-control">
    <label for="image">Image URL</label>
    <input type="text" bind:value={image} id="image" />
  </div>
  <div class="form-control">
    <label for="desc">Description</label>
    <textarea rows="3" bind:value={description} id="desc" />
  </div>
</div>

<button on:click={addContact}>Add Contact Card</button>
<button on:click={deleteFirst}>Delete First Card</button>
<button on:click={deleteLast}>Delete Last Card</button>

{#if formState === "invalid"}
  <p>Invalid input</p>
{/if}
{#each createdContact as contact, index (contact.id)}
  <h2># {index}</h2>
  <ContactCard
    userName={contact.name}
    jobTitle={contact.jobTitle}
    description={contact.desc}
    userImage={contact.imageURL}
  />
{:else}
  <p>Card list is empty!</p>
{/each}

<style>
  #form {
    width: 30rem;
    max-width: 100%;
  }
</style>
