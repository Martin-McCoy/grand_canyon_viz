<script>
  import Scrolly from "./Scrolly.svelte";
  import Areaplot from "./Areaplot.svelte";
	
  let value;
  const steps = [
		 "<p>This is Lake Powell at <strong>high elevation</strong>. Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam.</p>",
    "<p>This is Lake Powell at <strong>medium elevation</strong>. Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</p>",
    "<p>This is Lake Powell at <strong>low elevation</strong>. Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>",
  ];
</script>

<section>
	<div class='hero-container'>
		<div class='hero'>
			<h1> 
				Lake Powell & Grand Canyon Visualization
			</h1>
		</div>
	</div>
	
  <div class="section-container">
    <div class="steps-container">
      <Scrolly bind:value>
        {#each steps as text, i}
          <div class="step" class:active={value === i}>
            <div class="step-content">{@html text}</div>
          </div>
        {/each}
        <div class="spacer" />
      </Scrolly>
    </div>
    <div class="sticky">
      <Areaplot step={value} />
    </div>
  </div>
	<div class='footer'>
		<h2> 
			EDF Storymap Grand Canyon Pillar
		</h2>
	</div>
</section>

<style>
	:global(body) {
		overflow-x: hidden;
		background: #514348;
		color: #DFBC86;
		margin: 0;
		padding: 0;
	}
	
	.hero-container {
		background: #6D524D;
	}
	
	.hero {
		height: 60vh;
		font-size: 4rem;
		margin: 0 3em;
		display: flex;
		place-items: center;
		flex-direction: column;
		justify-content: center;
		text-align: center;
	}
	
	.footer {
		height: 30vh;
		font-size: 30px;
		margin: 0px 40px 0px 40px;
		display: flex;
		place-items: center;
		flex-direction: column;
		justify-content: center;
		text-align: center;
	}
	
  .spacer {
    height: 40vh;
  }

  .sticky {
    position: sticky;
    top: 3%;
		flex: 1 1 60%;
    width: 60%;
  }

  .section-container {
    margin-top: 1em;
    text-align: center;
    transition: background 100ms;
    display: flex;
  }

  .step {
    height: 80vh;
    display: flex;
    place-items: center;
    justify-content: center;
  }

  .step-content {
    font-size: 1rem;
    background: #89726E;
    color: #DFBC86;
    border-radius: 5px;
    padding: .5rem 1rem;
    display: flex;
    flex-direction: column;
    justify-content: center;
    transition: background 500ms ease;
    box-shadow: 1px 1px 10px rgba(0, 0, 0, .2);
    text-align: left;
		width: 75%;
		margin: auto;
		max-width: 500px;
  }

	.step.active .step-content {
		background: #6D524D;
		color: #DFBC86;
		
	}
	
  .steps-container,
  .sticky {
    height: 100%;
  }

  .steps-container {
    flex: 1 1 40%;
    z-index: 10;
  }
	
/* Comment out the following line to always make it 'text-on-top' */
  @media screen and (max-width: 768px) {
    .section-container {
      flex-direction: column-reverse;
    }
    .sticky {
      width: 95%;
			margin: auto;
    }
    .hero {
      font-size: 3rem;
    }
  }
</style>
