<script>
  import Preview from './Preview.svelte';
  import Authors from './Authors.svelte';

  export let article;

  let windowWidth;
</script>

<style>
  .article {
    background-color: $lavender;
    margin: 3rem 0;
    padding: 0 1rem;

    .article_inner {
      max-width: $max-width;
      margin: 0 auto;
      padding: 2rem 0;
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(20rem, 1fr));
      grid-gap: 2rem;

      .description {
        h2 {
          font-size: 28px;
          margin: 0 0 1rem 0;
        }
        p {
          font-size: 20px;
          margin: 0.5rem 0;
        }
      }
    }
    .line {
      margin: 0 4rem 0 0rem;
      border: 2px solid $lightgray;
      border-radius: 0.5rem;
    }
  }
  @media only screen and (max-width: $mobile-cutoff) {
    .article {
      background-color: transparent;
    }
  }
  @media only screen and (max-width: $mobile-cutoff-xs) {
    .article {
      padding: 0 0.5rem;
      .article_inner {
        grid-template-columns: auto;
      }
    }
  }
</style>

<svelte:window bind:outerWidth={windowWidth}/>
<div class="article">
  {#if windowWidth <= 950}
    <div class="line"></div>
  {/if}
  <div class="article_inner">
    <Preview slug={article.slug} component={article.component} />
    <div class="description">
      <h2><a href={article.slug}>{article.title}</a></h2>
      <p>{article.description}</p>
      <Authors authors={article.authors} />
    </div>
  </div>
</div>

