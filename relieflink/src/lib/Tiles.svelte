<script>
  export let tiles = [];
</script>

<div class="tiles-container">
  {#each tiles as tile}
    <button
      class="tile"
      style="background-image: url({tile.image});"
      on:click={() => tile.action && tile.action()}
      on:keydown={(event) =>
        (event.key === "Enter" || event.key === " ") &&
        tile.action &&
        tile.action()}
      aria-label={tile.title}
    >
      <div class="tile-content">
        <h2>{tile.title}</h2>
      </div>
    </button>
  {/each}
</div>

<style>
  .tiles-container {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }

  .tile {
    position: relative;
    height: 200px;
    border-radius: 8px;
    box-shadow:
      0 4px 6px rgba(0, 0, 0, 0.1),
      0 1px 3px rgba(0, 0, 0, 0.06);
    overflow: hidden;
    cursor: pointer;
    border: none;
    outline: none;
    color: white;

    transition:
      transform 0.3s ease,
      background-size 0.3s ease;
  }

  .tile::before {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
    background-image: inherit;
    filter: brightness(0.6);
    transition:
      transform 0.5s ease-in-out,
      filter 0.3s ease;
    z-index: 1;
  }

  .tile:hover::before,
  .tile:focus::before {
    transform: scale(1.1);
    filter: brightness(0.5);
  }

  .tile-content {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    z-index: 2;
    text-align: center;
    padding: 0.5rem 1rem;
    border-radius: 4px;
  }

  .tile-content h2 {
    margin: 0;
    font-size: 1.5rem;
    font-weight: bold;
  }

  @media (max-width: 600px) {
    .tile-content h2 {
      font-size: 1.2rem;
    }
  }
</style>
