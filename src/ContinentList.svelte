<script>
  import * as Countries from "../API/countryList.json";
  import Continent from "./Continent.svelte";

  const { countries } = Countries;

  const continentObj = { unknown: [] };

  for (const country of countries) {
    if (!country.region) {
      continentObj.unknown.push(country);
    } else if (!continentObj[country.region]) {
      continentObj[country.region] = [];
      continentObj[country.region].push(country);
    } else {
      continentObj[country.region].push(country);
    }
  }

  // for (let i = 0; i < countries.length; i++) {
  //   const country = countries[i];
  //   if (!country.region) {
  //     continentObj.unknown.push(country);
  //     continue;
  //   }
  //   if (!continentObj[country.region]) {
  //     continentObj[country.region] = [];
  //     continentObj[country.region].push(country);
  //     continue;
  //   }
  //   continentObj[country.region].push(country);
  // }
</script>

<ul class="main-list">
  {#each Object.entries(continentObj) as continent}
    <Continent continentName={continent[0]} continentArea={continent[1]} />
  {/each}
</ul>

<style lang="scss">
  .main-list {
    display: block;
    width: 100%;
  }

  /* @media screen and (min-width: 747px) {
    .main-list {
    }
  } */
</style>
