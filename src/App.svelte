<script>
	
  import Scrolly from "./Scrolly.svelte";
  import Scatterplot from "./Scatterplot.svelte";
  import Line from "./Line.svelte";
	
  let value;
  const steps = [
		"<p>Magnus Carlsen was born in Norway on 1990. Early on, he showed a knack for memorization, and driven by a desire to beat his older sister in chess, started taking the game seriously. With the help of prominent Norwegian chess players, Carlsen quickly improved. <br> <br> By the time he was nine (in 2000), he was already hit a rating of 1900. Three years later, Carlsen claimed his International Master (IM) title.</p>",
		"<p>At age 13, Carlsen became the world's youngest Grandmaster (GM) at the time. Two prominent matches of his at the time included beating former world champion Anatoly Karpov in a blitz tournament and drawing with Garry Kasparov, who was then the number one player in the world, in a rapid tournament. <br><br> In 2006, he won his first Norwegian Chess Championship. The following year, he participated in the Candidates Tournament for the FIDE World Chess Championship, but ultimately fell to GM Levon Aronian</p>",
		"<p>Carlsen won the 2009 Pearl Spring Chess Tournament with a performance rating of 3002, which ranks as the fourth-highest performance rating in a tournament of all time. This tournament win also boosted his rating from 2772 to 2801, making him the youngest player to break 2800 at the time. <br><br> He later went on the win the World Blitz Championship Tournament, claimed the number-one position in the world (which he still holds today), and in 2013, overcame reigning champion Viswanathan Anand to claim his first World Chess Champion title. </p>",
    "<p>In 2014, Carlsen made history by achieving an all-time high record rating of 2882. In the same year, he became a triple world champion by winning the World Rapid and Blitz Championships, and defended his World Championship title in a rematch against Anand. <br><br> In 2015 he was briefly the highest-rated player in all three time controls (blitz, rapid, classical) simultanesouly. In 2016 and 2018, he defended his World Chess Champion titles again.</p>",
    "<p>In 2019, Carlsen attained the longest unbeaten streak in history of 125 straight classical games. He also tied his peak rating of 2882.  <br><br>  In 2021 he defended his World Chess Champion title against Ian Nepomniachtchi, before announcing that he would not defend his title next year. In 2022 he won both World Rapid and Blitz Championships once again (previously: 2014, 2019). <br><br> In present day, Carlsen has expressed a disinterest in classical chess, preferring rapid and blitz formats instead. He has also made various forays into poker, fantasy sports, hosting a podcast, and more. </p>",
  ];
</script>

<section>
	<div class='hero'>
		<h1> 
			Following Magnus Carlsen's chess journey by rating
		</h1>
		
	</div>

  <div id='intro'>
    <p>Magnus Carlsen is widely considered to be the greatest chess player of all time.
      A five-time World Chess Champion who has achieved the highest rating in history and been ranked No. 1 in the world since 2011, 
      he boasts a very decorated resume.</p>
    <p style='margin-bottom: 30px'>But how did he get there? This visualization follows Carlsen's path to greatness by his rating.</p>
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
      <Scatterplot step={value} />
    </div>
  </div>

  <p>View Carlsen's full rating chart below.</p>

  <div style='margin-top: 40px'>
    <Line />
  </div>

  <p style='margin-top: 15px'>
    Source code can be found <a href='https://github.com/unoptimal/magnus-journey' target="_blank">here</a>.
  </p>
</section>

<style>
	:global(body) {
		overflow-x: hidden;
	}

  #intro{
    display: flex;
    justify-content: left;
    flex-direction: column;
    margin: 0 auto;
    max-width: 800px;
  }
	
	.hero {
		height: 20vh;
		display: flex;
		place-items: center;
		flex-direction: column;
		justify-content: center;
		text-align: center;
    margin-bottom: -30px
	}
	
	.sticky {
    position: sticky;
    top: 10%;
		flex: 1 1 60%;
    width: 60%;
  }

  .section-container {

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
    background: whitesmoke;
    color: #ccc;
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
		background: white;
		color: black;
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
  }
</style>
