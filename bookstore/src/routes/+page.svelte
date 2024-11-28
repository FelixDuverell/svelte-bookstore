<script>
	import Book from './Book.svelte';
	import { writable } from 'svelte/store';
  
	let title = '';
	let price = 0;
	let description = '';
	const books = writable([]);
  
	function addBook() {
	  books.update(currentBooks => [
		...currentBooks,
		{ title, price, description }
	  ]);
  
	  // Återställ formulärfält
	  title = '';
	  price = 0;
	  description = '';
	}
  </script>
  

  
  <h1>Felix Bokhandel</h1>
  
  <form on:submit|preventDefault={addBook}>
	<h2>Add book</h2>
	<div>
	  <label for="title">Title</label>
	  <input type="text" id="title" bind:value={title} required />
	</div>
	<div>
	  <label for="price">Price</label>
	  <input type="number" id="price" bind:value={price} min="0" step="0.01" required />
	</div>
	<div>
	  <label for="description">Description</label>
	  <textarea rows="3" id="description" bind:value={description} required></textarea>
	</div>
	<button type="submit">Add Book</button>
  </form>
  
  <div class="books">
	{#if $books.length === 0}
	  <p>No books added.</p>
	{:else}
	  {#each $books as book}
		<Book bookTitle={book.title} bookPrice={book.price} bookDescription={book.description} />
	  {/each}
	{/if}
  </div>

  <style>
	h1 {
	  color: #000000;
	  font-weight: bold;
	  text-align: center;
	}
	h2 {
		display: flex;
		justify-content: center;
		align-items: center;
		font-size: 22px;
		font-weight: bolder;
		color: #066f8f;
		text-decoration: underline;
	}
	form {
	  margin: auto;
	  width: 30rem;
	  padding: 1rem;
	  border: 1px solid #000000;
	  background-color: #ccc;
	  box-shadow: #000;
	  border-radius: 5px;
	}
	label, input, textarea {
	  width: 100%;
	  margin-bottom: 0.5rem;
	}
	button {
	  width: 100%;
	  padding: 0.5rem;
	  background-color: #066f8f;
	  color: white;
	  border: none;
	  border-radius: 3px;
	  cursor: pointer;
	}
	.books {
	  margin-top: 2rem;
	}

	p {
		display: flex;
		justify-content: center;
		align-items: center;
	}
  </style>
  

  