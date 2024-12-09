<script>
  export let items = [];
  export let name = "";
  export let subheading = "";
  let checkedItems = new Set();

  function toggleItem(item) {
    if (checkedItems.has(item)) {
      checkedItems.delete(item);
    } else {
      checkedItems.add(item);
    }
  }
</script>

<div class="checklist">
  <br />
  <h2>{name}</h2>
  <p>{subheading}</p>
  <ul>
    {#each items as item}
      <li>
        <label class="custom-checkbox">
          <input
            type="checkbox"
            id={item}
            on:change={() => toggleItem(item)}
            checked={checkedItems.has(item)}
          />
          <span class="checkmark"></span>
          <span class="label-text">{item}</span>
        </label>
      </li>
    {/each}
  </ul>
</div>

<style>
  .checklist {
    margin: 20px;
    text-align: center;
  }

  .checklist ul {
    list-style: none;
    padding: 0;
  }

  .checklist li {
    margin-bottom: 1rem;
    display: flex;
    justify-content: center;
    padding: 5px;
    display: inline-block;
  }

  .custom-checkbox {
    display: flex;
    align-items: center;
    cursor: pointer;
    position: relative;
    font-size: 1rem;
  }

  .custom-checkbox input {
    position: absolute;
    opacity: 0;
    cursor: pointer;
  }

  .checkmark {
    width: 20px;
    height: 20px;
    background-color: #e6e6e6;
    border: 2px solid #ccc;
    border-radius: 4px;
    display: inline-block;
    margin-right: 1rem;
    position: relative;
    transition:
      background-color 0.3s,
      border-color 0.3s;
  }

  .custom-checkbox input:checked ~ .checkmark {
    background-color: #c3c3c3;
    border-color: #c3c3c3;
  }

  .custom-checkbox input:checked ~ .checkmark::after {
    content: "";
    position: absolute;
    left: 5px;
    top: 2px;
    width: 6px;
    height: 12px;
    border: solid white;
    border-width: 0 2px 2px 0;
    transform: rotate(45deg);
  }

  .label-text {
    font-size: 1rem;
    color: #fff;
    transition: color 0.3s;
  }

  .custom-checkbox input:checked ~ .label-text {
    color: #c3c3c3;
  }

  .custom-checkbox:hover .checkmark {
    border-color: #c3c3c3;
  }
</style>
