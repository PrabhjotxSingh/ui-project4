<script>
  import Tiles from "./lib/Tiles.svelte";
  import Checklist from "./lib/Checklist.svelte";
  import { onMount } from "svelte";
  import Globe from "globe.gl";
  import Swal from "sweetalert2";

  let globeInstance;

  const weatherForecast = [
    { day: "Monday", icon: "☀️", high: 75, low: 55 },
    { day: "Tuesday", icon: "🌧️", high: 70, low: 52 },
    { day: "Wednesday", icon: "⛅", high: 68, low: 50 },
  ];

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
    {
      title: "Satellite Calling Guide",
      image: "call.png",
      action: () => alert("Navigating to Satellite Calling Guide"),
    },
  ];

  const news = [
    {
      title: "Possibility of tornado forming.",
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

  onMount(() => {
    const globeContainer = document.getElementById("globe-container");

    // Initialize Globe instance
    globeInstance = new Globe(globeContainer)
      .globeImageUrl("//unpkg.com/three-globe/example/img/earth-day.jpg")
      .bumpImageUrl("//unpkg.com/three-globe/example/img/earth-topology.png")
      .pointsData([
        { lat: 20.7984, lng: -156.3319, size: 1, color: "red" },
        { lat: 40.4173, lng: -82.9071, size: 1, color: "red" },
      ])
      .pointAltitude(0.1)
      .pointColor("color")
      .pointRadius("size");

    globeInstance.controls().enableDamping = true;
    globeInstance.pointOfView(
      { lat: 20.7984, lng: -156.3319, altitude: 2 },
      2000
    );
  });

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
  <div id="globe-container" class="globe-background"></div>
  <div class="left-panel">
    <p>ReliefLink</p>
    <h1>Maui County, Hawaii</h1>
    <br />
    <div class="alertl">
      <h3>HIGH IMPORTANCE</h3>
      <h3>Hawaii Evacuation Team</h3>
      <p>
        Due to the ongoing fires, an evacuation order has been issued for
        affected areas. Residents are urged to leave immediately and proceed to
        designated evacuation shelters. Follow local authorities' instructions
        and stay tuned for updates.
      </p>
    </div>
    <br />
    <div class="alert">
      <h3>Hawaii Emergency Management Agency</h3>
      <p>
        A red flag warning is issued for the leeward portions of all Hawaiian
        Islands through 6 p.m. local time Friday night. Although red flag
        warnings don't predict new fires, the warning means that critical fire
        weather is occurring or will begin soon. Critical fire weather occurs
        when there are strong winds, low relative humidity and warm temperatures
        that contribute to extreme fire behavior.
      </p>
    </div>
    <br />
    <div class="alertm">
      <h3>Hawaii Air Quality Agency</h3>
      <p>
        Air quality in Maui, Hawaii, has been impacted by nearby fires, leading
        to elevated levels of smoke and particulate matter. Residents,
        especially those with respiratory conditions, are advised to stay
        indoors with windows closed and use air purifiers if available. Limit
        outdoor activities until conditions improve.
      </p>
    </div>
    <br />
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
    <br />
    <h2>Resources</h2>
    <Tiles tiles={resources} />
    <br />
    <h2>News</h2>
    <Tiles tiles={news} />
    <br />
    <h2>Checklist</h2>
    <Checklist items={emergencyItems} />
    <br />
    <h2>Report to Authorities</h2>
    <div class="actions">
      <a class="btn" on:click={report} href="#report">Set status to danger</a>
      <a class="btn" on:click={report} href="#report">Set status to safe</a>
      <br /><br /><br />
      <a class="btn" on:click={report} href="#report">Contact rescue team</a>
      <a class="btn" on:click={report} href="#report">Contact police</a>
      <a class="btn" on:click={report} href="#report">Contact fire services</a>
      <br /><br />
      <p>Be advised: authority services have a high load.</p>
    </div>
    <h2>Missing Persons</h2>
    <a class="btn" on:click={report} href="#report">Report Missing Person</a>
    <a class="btn" on:click={report} href="#report">Search Missing Status</a>
    <br />
    <br />
    <br />
    <br />
    <br />
    <br />
    <p>Last updated: 5min ago</p>
    <br />
    <br />
  </div>
</main>

<style>
  main {
    position: relative;
    height: 100vh;
    overflow: hidden;
    background: linear-gradient(180deg, #1e1e2f, #121212);
    color: white;
  }

  .globe-background {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: 1;
  }

  .left-panel {
    position: absolute;
    top: 0;
    left: 0;
    width: 40%;
    height: 100%;
    z-index: 2;
    backdrop-filter: blur(10px);
    background: rgba(0, 0, 0, 0.5);
    padding: 20px;
    box-shadow: inset 0 0 15px rgba(0, 0, 0, 0.5);
    border-right: 1px solid rgba(255, 255, 255, 0.1);
    overflow-y: auto;
    scrollbar-width: thin;
  }

  .left-panel h1,
  .left-panel p {
    color: #ffffff;
  }

  .left-panel h1 {
    font-size: 2rem;
    margin-bottom: 1rem;
  }

  .left-panel p {
    font-size: 1rem;
    line-height: 1.5;
  }

  .alert {
    border-style: solid;
    border-color: rgb(95, 15, 15);
    padding: 20px;
    border-radius: 10px;
    width: 93%;
  }

  .alertm {
    border-style: solid;
    border-color: rgb(96, 106, 16);
    padding: 20px;
    border-radius: 10px;
    width: 93%;
  }

  .alertl {
    border-style: solid;
    border-color: rgb(95, 15, 15);
    background-color: rgb(95, 15, 15);
    color: white;
    padding: 20px;
    border-radius: 10px;
    width: 93%;
  }

  .weather-forecast {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
    gap: 1rem;
    margin: 1rem 0;
  }

  .weather-card {
    border: 1px solid #ddd;
    border-radius: 8px;
    padding: 1rem;
    width: 83%;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    text-align: center;
  }

  .weather-card h3 {
    margin: 0;
    font-size: 1.2rem;
    color: #ffffff;
  }

  .weather-icon {
    font-size: 2rem;
    margin: 0.5rem 0;
  }

  .weather-card p {
    margin: 0.5rem 0;
    font-size: 1rem;
    color: #ffffff;
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
    background-color: transparent;
    color: white;
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
