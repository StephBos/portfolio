<div class="app-container">
	<slot />
</div>

<style>
  :global(html), :global(body) {
    margin: 0;
    padding: 0;
    width: 100%;
    height: 100%;
    background-color: #222831;
    overflow-x: hidden;
  }

  .app-container {
    width: 100vw;
    min-height: 100vh;
    background-color: #222831;
    display: flex;
    flex-direction: column;
    justify-content: center;
  }
</style>
