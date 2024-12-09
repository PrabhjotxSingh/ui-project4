<script>
  import Swal from "sweetalert2";
  import Alerts from "./lib/Alerts.svelte";
  import Header from "./lib/Header.svelte";
  import Tiles from "./lib/Tiles.svelte";
  import Checklist from "./lib/Checklist.svelte";

  const resources = [
    {
      title: "Shelters",
      image: "shelter.webp",
      action: () => alert("Navigating to Shelters"),
    },
    {
      title: "Food Banks",
      image: "food.jpg",
      action: () => alert("Navigating to Food Banks"),
    },
    {
      title: "Medical Aid",
      image: "medical.jpg",
      action: () => alert("Navigating to Medical Aid"),
    },
    {
      title: "Evacuation Routes",
      image: "evac.jpg",
      action: () => alert("Navigating to Evacuation Routes"),
    },
  ];

  const news = [
    {
      title: "A tornado sweeps the mid-west.",
      image: "news/tornado.jpg",
      action: () => alert("Navigating to News"),
    },
    {
      title: "More food banks open.",
      image: "news/foodbank.jpg",
      action: () => alert("Navigating to News"),
    },
    {
      title: "Rescue teams arrive.",
      image: "news/rescue.jpg",
      action: () => alert("Navigating to News"),
    },
    {
      title: "Death toll rises.",
      image: "news/deathtoll.jpg",
      action: () => alert("Navigating to News"),
    },
  ];

  const emergencyItems = [
    "First-aid kit",
    "Flashlight with batteries",
    "Bottled water",
    "Non-perishable food",
    "Medications",
    "Portable phone charger",
    "Important documents",
  ];

  const weatherForecast = [
    { day: "Monday", icon: "☀️", high: 75, low: 55 },
    { day: "Tuesday", icon: "🌧️", high: 70, low: 52 },
    { day: "Wednesday", icon: "⛅", high: 68, low: 50 },
  ];

  function report(event) {
    const action = event.target.textContent.trim();

    Swal.fire({
      title: `Confirm Action`,
      text: `Are you sure you want to proceed with "${action}"? Your name, phone number, and current location will be sent.`,
      icon: "warning",
      showCancelButton: true,
      confirmButtonText: "Yes, proceed",
      cancelButtonText: "Cancel",
      confirmButtonColor: "#242424",
      cancelButtonColor: "#d33",
    }).then((result) => {
      if (result.isConfirmed) {
        Swal.fire({
          title: "Report Sent",
          text: `"${action}" report has been successfully sent.`,
          icon: "success",
          confirmButtonColor: "#242424",
        });
      }
    });
  }
</script>

<main>
  <Header />
  <div class="tiles-container">
    <br />
    <h2>Weather</h2>
    <p>See the forecast ahead to prepare.</p>
    <div class="weather-forecast">
      {#each weatherForecast as day}
        <div class="weather-card">
          <h3>{day.day}</h3>
          <div class="weather-icon">{day.icon}</div>
          <p>High: {day.high}°F</p>
          <p>Low: {day.low}°F</p>
        </div>
      {/each}
    </div>
    <Alerts />
    <br />
    <br />
    <h2>Quick Links</h2>
    <p>Quickly access local resources.</p>
    <Tiles tiles={resources} />
    <Checklist
      items={emergencyItems}
      name="Emergency Items"
      subheading="Make sure you have all the items you need."
    />
    <br />
    <h2>News at a Glance</h2>
    <p>See what is happening around you.</p>
    <Tiles tiles={news} />
    <br />
    <h2>Report to Authorities</h2>
    <p>Report emergencies quickly.</p>
    <br />
    <div class="actions">
      <a class="btn" on:click={report} href="#report">I am in danger</a>
      <a class="btn" on:click={report} href="#report">Report missing person</a>
      <a class="btn" on:click={report} href="#report">Contact rescue team</a>
      <a class="btn" on:click={report} href="#report">Contact police</a>
      <a class="btn" on:click={report} href="#report">Contact fire services</a>
    </div>
  </div>
  <br />
  <br />
  <br />
  <br />
</main>

<style>
  .tiles-container {
    text-align: center;
  }

  .weather-forecast {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 1rem;
    margin: 1rem 0;
  }

  .weather-card {
    background: #f9f9f9;
    border: 1px solid #ddd;
    border-radius: 8px;
    padding: 1rem;
    width: 150px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    text-align: center;
  }

  .weather-card h3 {
    margin: 0;
    font-size: 1.2rem;
    color: #333;
  }

  .weather-icon {
    font-size: 2rem;
    margin: 0.5rem 0;
  }

  .weather-card p {
    margin: 0.5rem 0;
    font-size: 1rem;
    color: #555;
  }

  @media (max-width: 600px) {
    .weather-card {
      width: 100px;
    }

    .weather-card h3 {
      font-size: 1rem;
    }

    .weather-icon {
      font-size: 1.5rem;
    }

    .weather-card p {
      font-size: 0.9rem;
    }
  }

  .actions {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 15px;
    margin: 20px 0;
  }

  .btn {
    margin: 0;
    padding: 10px 20px;
    color: white;
    border: 1px solid #db3434;
    border-radius: 3px;
    font-size: 1em;
    cursor: pointer;
    text-decoration: none;
    background-color: #db3434;
    transition: all 0.3s ease;

    width: calc(33% - 20px);
    text-align: center;
    box-sizing: border-box;
  }

  .btn:hover {
    background-color: white;
    color: black;
  }

  @media (max-width: 768px) {
    .btn {
      width: calc(50% - 20px);
    }
  }

  @media (max-width: 480px) {
    .btn {
      width: calc(100% - 20px);
    }
  }
</style>
