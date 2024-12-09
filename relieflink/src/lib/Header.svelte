<script>
  import Swal from "sweetalert2";

  let bannerTitle = "ReliefLink";
  let bannerSubtitle = "Your trusted companion in emergencies.";

  function openSettings() {
    Swal.fire({
      title: "Settings",
      html: `
       <div style="text-align: left;">
        <label for="state" style="display: block; margin-bottom: 0.5rem;">Select Your State</label>
        <select id="state" style="width: 100%; padding: 0.5rem; border-radius: 4px; margin-bottom: 1rem; border: 1px solid #ddd;">
          <option value="">Select a State</option>
          <option value="AL">Alabama</option>
          <option value="AK">Alaska</option>
          <option value="AZ">Arizona</option>
          <option value="AR">Arkansas</option>
          <option value="CA">California</option>
          <option value="CO">Colorado</option>
          <option value="CT">Connecticut</option>
          <option value="DE">Delaware</option>
          <option value="FL">Florida</option>
          <option value="GA">Georgia</option>
          <option value="HI">Hawaii</option>
          <option value="ID">Idaho</option>
          <option value="IL">Illinois</option>
          <option value="IN">Indiana</option>
          <option value="IA">Iowa</option>
          <option value="KS">Kansas</option>
          <option value="KY">Kentucky</option>
          <option value="LA">Louisiana</option>
          <option value="ME">Maine</option>
          <option value="MD">Maryland</option>
          <option value="MA">Massachusetts</option>
          <option value="MI">Michigan</option>
          <option value="MN">Minnesota</option>
          <option value="MS">Mississippi</option>
          <option value="MO">Missouri</option>
          <option value="MT">Montana</option>
          <option value="NE">Nebraska</option>
          <option value="NV">Nevada</option>
          <option value="NH">New Hampshire</option>
          <option value="NJ">New Jersey</option>
          <option value="NM">New Mexico</option>
          <option value="NY">New York</option>
          <option value="NC">North Carolina</option>
          <option value="ND">North Dakota</option>
          <option value="OH" selected>Ohio</option>
          <option value="OK">Oklahoma</option>
          <option value="OR">Oregon</option>
          <option value="PA">Pennsylvania</option>
          <option value="RI">Rhode Island</option>
          <option value="SC">South Carolina</option>
          <option value="SD">South Dakota</option>
          <option value="TN">Tennessee</option>
          <option value="TX">Texas</option>
          <option value="UT">Utah</option>
          <option value="VT">Vermont</option>
          <option value="VA">Virginia</option>
          <option value="WA">Washington</option>
          <option value="WV">West Virginia</option>
          <option value="WI">Wisconsin</option>
          <option value="WY">Wyoming</option>
        </select>

        <label for="name" style="display: block; margin-bottom: 0.5rem;">Name</label>
        <input value="Prabhjot Singh" id="name" type="text" placeholder="Enter your name" 
          style="width: 100%; padding: 0.5rem; border-radius: 4px; margin-bottom: 1rem; border: 1px solid #ddd;" />

        <label for="phone" style="display: block; margin-bottom: 0.5rem;">Phone Number</label>
        <input value="(513)-123-1234" id="phone" type="tel" placeholder="Enter your phone number" 
          style="width: 100%; padding: 0.5rem; border-radius: 4px; border: 1px solid #ddd;" />
      </div>
    `,
      confirmButtonColor: "#242424",
      confirmButtonText: "Save",
      showCancelButton: true,
      cancelButtonText: "Cancel",
      cancelButtonColor: "#242424",
    });
  }
</script>

<div class="banner">
  <div class="settings">
    <a on:click={openSettings} href="#settings" aria-label="Settings">⚙</a>
  </div>
  <h1>{bannerTitle}</h1>
  <p>{bannerSubtitle}</p>
</div>

<style>
  .banner {
    position: relative;
    background-color: #242424;
    color: white;
    text-align: center;
    padding: 2rem;
    border-radius: 8px;
    box-shadow:
      0 4px 6px rgba(0, 0, 0, 0.1),
      0 1px 3px rgba(0, 0, 0, 0.06);
    margin: 1rem;
  }

  .banner h1 {
    font-size: 2rem;
    margin: 0.5rem 0;
    font-weight: bold;
  }

  .banner p {
    font-size: 1.2rem;
    margin: 0;
  }

  .settings {
    position: absolute;
    top: 10px;
    right: 20px;
    font-size: 1.5rem;
  }

  .settings a {
    text-decoration: none;
    color: white;
    cursor: pointer;
    transition: transform 0.2s ease;
  }

  .settings a:hover {
    transform: scale(1.2);
  }
</style>
