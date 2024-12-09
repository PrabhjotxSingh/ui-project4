<script>
  import { onMount } from "svelte";

  let alerts = [];

  onMount(async () => {
    alerts = await fetchDisasterAlerts();
  });

  async function fetchDisasterAlerts() {
    const apiUrl = "https://api.weather.gov/alerts/active?area=OH";

    try {
      const response = await fetch(apiUrl);
      if (!response.ok) throw new Error("Failed to fetch alerts");

      const data = await response.json();
      return data.features;
    } catch (error) {
      console.error("Error fetching alerts:", error);
      return [];
    }
  }
</script>

<section class="alerts-section">
  <h3>Local Disaster Alerts for Ohio</h3>

  {#if alerts.length > 0}
    <ul class="alerts-list">
      {#each alerts as alert}
        <li class="alert-item">
          <h3>{alert.properties.event}</h3>
          <p>{alert.properties.headline}</p>
          <p>{alert.properties.description}</p>
          <small
            >Effective: {new Date(
              alert.properties.effective
            ).toLocaleString()}</small
          >
        </li>
      {/each}
    </ul>
  {:else}
    <p>No active alerts for Ohio at this time.</p>
  {/if}
</section>

<style>
  .alerts-section {
    padding: 1rem;
    background-color: #f9f9f9;
    border-radius: 8px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    color: #000;
    margin: 15px;
  }

  .alerts-list {
    list-style: none;
    padding: 0;
  }

  .alert-item {
    background-color: #ffffff;
    border: 1px solid #ddd;
    padding: 1rem;
    margin-bottom: 1rem;
    border-radius: 4px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05);
  }

  .alert-item small {
    color: #888;
  }
</style>
