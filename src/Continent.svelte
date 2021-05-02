<script>
  export let continentName;
  export let continentArea;
  import Country from "./Country.svelte";

  $: formatNames = (name) => {
    return name
      .split("-")
      .map((str) => {
        return str[0].toUpperCase() + str.substr(1);
      })
      .join(" ");
  };
</script>

{#if continentName !== "unknown"}
  <li class="continent-item {continentName}">
    <input id="collapse-continent" class="toggle" type="checkbox" />
    <label for="collapse-continent" class="lbl-toggle">
      <h2 class="collapse-title">{formatNames(continentName)}</h2>
    </label>
    <div class="continent-content">
      <div class="continent-heading">
        {#if continentName === "antarctica"}
          <p>
            {formatNames(continentName)} <strong>is not a nation</strong>
            but it's own continent !
          </p>
        {:else}
          <p>
            There are at least <strong>{continentArea.length} countries</strong>
            on the continent of {formatNames(continentName)}
          </p>
        {/if}
      </div>
      <ul class="country-list">
        {#each continentArea as country}
          <Country name={country.name} alpha2={country.alpha2} />
        {/each}
      </ul>
    </div>
  </li>
{/if}

<style lang="scss">
  .continent-item {
    display: block;
    width: 100%;
    height: 100%;
    list-style: none;
    border: 1px solid green;

    /* Collapse */
    .toggle[type="checkbox"] {
      display: block;
    }

    .toggle:checked + label {
      border-bottom-right-radius: 0;
      border-bottom-left-radius: 0;
    }

    .toggle:checked + label::before {
      transform: rotate(90deg) translateX(-3px);
    }

    .toggle:checked + label + .continent-content {
      max-height: 100vh;
    }

    label {
      display: block;
      cursor: pointer;

      h2 {
        font-size: 40px;
      }
    }

    .lbl-toggle::before {
      content: " ";
      display: inline-block;
      height: 100%;
      width: 100%;
      border: 1px solid pink;

      border-top: 5px solid transparent;
      border-bottom: 5px solid transparent;
      border-left: 5px solid currentColor;

      vertical-align: middle;
      margin-right: 0.7rem;
      transform: translateY(-2px);

      transition: transform 0.2s ease-out;
    }

    /* List item content */
    .continent-content {
      max-height: 0px;
      overflow: hidden;
      transition: max-height 0.25s ease-in-out;

      .country-list {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        width: 100%;
        margin: 0 auto;
      }
    }
  }
  @media screen and (min-width: 747px) {
    .continent-item {
      .continent-content {
        .country-list {
          display: grid;
          grid-template-columns: repeat(auto-fill, minmax(220px, 220px));
          grid-template-rows: repeat(auto-fit, minmax(240px));
          gap: 12px 12px;
        }
      }
    }
  }
</style>
