<script>
  export let name;
  export let alpha2;

  $: formatNames = (name) => {
    return name
      .split("-")
      .map((str) => {
        return str[0].toUpperCase() + str.substr(1);
      })
      .join(" ");
  };

  // Check if image has been loaded after first render
  // document.addEventListener("DOMContentLoaded", () => {});
</script>

<li class="country-card">
  <div class="country-flag">
    {#if alpha2 !== ""}
      <img
        class="flag-image"
        src={`/assets/images/flags/${alpha2.toLowerCase()}.svg`}
        alt={alpha2.toLowerCase()}
      />
    {/if}
    <div class="country-code">
      {#if alpha2 !== ""}
        <span>{alpha2}</span>
      {:else}
        <span>&times;</span>
      {/if}
    </div>
  </div>
  <h2 class="country-name">{formatNames(name)}</h2>
</li>

<style lang="scss">
  .country-card {
    display: flex;
    align-items: center;
    justify-content: center;
    border: 1px dotted grey;
    height: 35px;
    width: 200px;

    .country-flag {
      position: relative;
      width: 30%;
      height: 100%;
      margin-right: 12px;
      cursor: pointer;

      .flag-image {
        display: block;
        min-width: 30px;
        width: 100%;
        height: 100%;
        min-height: 30px;
        opacity: 1;
        transition: opacity ease-in 0.1s;
      }

      .country-code {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        opacity: 0;
        transition: opacity ease-in 0.2s;

        span {
          position: absolute;
          top: 50%;
          left: 50%;
          width: 28px;
          height: 28px;
          padding: 8px 4px 0px 4px;
          border: 2px solid #444;
          border-radius: 50%;
          transform: translate(-50%, -50%);
          text-align: center;
        }
      }
      &:hover {
        .flag-image {
          opacity: 0;
        }
        .country-code {
          opacity: 1;
        }
      }
    }
    .country-name {
      width: 70%;
      font-size: 12px;
      font-weight: 600;
      color: #333;
      overflow: hidden;
      white-space: nowrap;
      text-overflow: ellipsis;
    }
  }
  /* @media screen and (min-width: 747px) {
    .country-card {
    }
  } */
</style>
