<script>
  import ContinentList from "./ContinentList.svelte";
  export let name;

  // document.addEventListener("DOMContentLoaded", () => {
  //   const flags = countries.map((country) => country.flag);
  //   let countryCards = document.getElementsByClassName("country-card");
  //   let flagImg = [...document.getElementsByClassName("flag-image")];
  //   let urlArray = flagImg.map((flag) => {
  //     return flag.attributes[1];
  //   });

  //   async function checkRequest(imgURL) {
  //     var http = new XMLHttpRequest();

  //     http.open("HEAD", imgURL, false);
  //     http.send();

  //     return http.status != 404;
  //   }

  //   urlArray.forEach((url) => {
  //     console.log(checkRequest(url.value));
  //     if (checkRequest(url.value) === false) {
  //       console.log(url);
  //     }
  //   });
  // });
</script>

<main>
  <div class="main-heading"><h1>Hello {name}!</h1></div>
  <ContinentList />
</main>

<style lang="scss">
  main {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    max-width: 95%;
    margin: 0 auto;

    .main-heading {
      h1 {
        color: #ff3e00;
        text-transform: uppercase;
        font-size: 62px;
        font-weight: 100;
      }
    }
  }

  @media screen and (min-width: 1280px) {
    main {
      width: 95%;
      max-width: 1280px;
    }
  }
</style>
