<script>
  import * as d3 from 'd3';
  import BarChart from './lib/BarChart.svelte';

  let populationData, sortedData;

  d3.csv('/data/populationInProvinces.csv').then(data => {
    populationData = data;
    sortedData = populationData.sort(
      (a, b) => a['population'] - b['population'],
    );
  });
</script>

<main>
  <div class="app">
    <div class="text">
      <h1>Dutch provinces by population (September, 2022)</h1>
    </div>
    {#if sortedData}
      <BarChart data={sortedData} />
    {/if}

    <div class="text">
      <p>
        Developed by
        <a
          href="https://leandrocollares.netlify.app"
          target="_blank"
          rel="noopener noreferrer"
        >
          Leandro Collares
        </a>
        &middot; Source:
        <a
          href="https://opendata.cbs.nl/statline/#/CBS/nl/dataset/71488ned/table?dl=6DEE4"
          target="_blank"
          rel="noopener noreferrer"
        >
          Centraal Bureau voor de Statistiek
        </a>
      </p>
    </div>
  </div>
</main>

<style>
  @font-face {
    font-family: 'Merriweather';
    font-style: normal;
    font-weight: 700;
    src: url('../fonts/merriweather-v30-latin-700.eot'); /* IE9 Compat Modes */
    src: local(''),
      url('../fonts/merriweather-v30-latin-700.eot?#iefix')
        format('embedded-opentype'),
      /* IE6-IE8 */ url('../fonts/merriweather-v30-latin-700.woff2')
        format('woff2'),
      /* Super Modern Browsers */
        url('../fonts/merriweather-v30-latin-700.woff') format('woff'),
      /* Modern Browsers */ url('../fonts/merriweather-v30-latin-700.ttf')
        format('truetype'),
      /* Safari, Android, iOS */
        url('../fonts/merriweather-v30-latin-700.svg#Merriweather')
        format('svg'); /* Legacy iOS */
  }

  @font-face {
    font-family: 'Source Sans Pro';
    font-style: normal;
    font-weight: 400;
    src: url('../fonts/source-sans-pro-v21-latin-regular.eot'); /* IE9 Compat Modes */
    src: local(''),
      url('../fonts/source-sans-pro-v21-latin-regular.eot?#iefix')
        format('embedded-opentype'),
      /* IE6-IE8 */ url('../fonts/source-sans-pro-v21-latin-regular.woff2')
        format('woff2'),
      /* Super Modern Browsers */
        url('../fonts/source-sans-pro-v21-latin-regular.woff') format('woff'),
      /* Modern Browsers */
        url('../fonts/source-sans-pro-v21-latin-regular.ttf') format('truetype'),
      /* Safari, Android, iOS */
        url('../fonts/source-sans-pro-v21-latin-regular.svg#SourceSansPro')
        format('svg'); /* Legacy iOS */
  }

  :root {
    font-family: 'Source Sans Pro', sans-serif;
    font-size: 16px;
    font-weight: 400;
    line-height: 24px;
    color: #282828;
    background: #ffffff;
    margin: 0 15px;
  }

  .app {
    display: flex;
    flex-direction: column;
    align-items: center;
    height: 100%;
    width: 100%;
    user-select: none;
  }

  .text {
    width: 100%;
    max-width: 700px;
    margin-top: 20px;
  }

  h1 {
    font-family: 'Merriweather', serif;
    font-size: 20px;
    font-weight: 700;
    line-height: 28px;
  }

  a {
    color: #ff4941;
    text-underline-offset: 0.2em;
  }

  a:visited {
    color: #ff4941;
  }

  a:active {
    color: #ff4941;
  }

  a:hover {
    color: #1313db;
  }
</style>
