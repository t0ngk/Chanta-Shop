<script context="module">
  export async function load({fetch}){
    const res = await fetch('/api/products.json');
    const { products } = await res.json();

    if (res.ok) {
      return {
        props: {
          products
        }
      }
    }

    return {
      status: res.status,
      error: new Error(res.statusText)
    }
  }
</script>

<script>
  export let products;
  import Productcards from "$lib/productcards.svelte";
</script>

<svelte:head>
  <title>Chanta Shop</title>
</svelte:head>

<div class="container content-center mx-auto">
  <div class="flex flex-row flex-wrap my-5">
    {#each products as product}
      <Productcards title={product.title} desc={product.desc} img={product.img} price={product.price}/>
    {/each}
  </div>
</div>



