<script>
  import { goto } from "$app/navigation";

  function switchPage(event, page) {
    event.preventDefault();
    goto(page);
  }
</script>

<svelte:head>
  <link rel="stylesheet" href="/css/main.css" />
</svelte:head>

<main class="blog">
  <h1>Tales From the High Sea!</h1>
  <h1>Book 2: Raiders of the Fever Sea</h1>
  <br />
  <div class="dropdown">
    <button class="dropbtn">Select Book</button>
    <div class="dropdown-content">
      <a
        href="/adventure1"
        on:click={(event) => switchPage(event, "/adventure1")}>Book 1</a
      >
      <a href="/adventure" on:click={(event) => switchPage(event, "/adventure")}
        >Book 2</a
      >
    </div>
  </div>
  <br />
  <article id="new">
    <h2>The Rebirth of the Man's Promise</h2>
    <h3>April 27, 2024</h3>
    <img
      src="images/birth_of_scourges_bane.jpg"
      alt="The new ship being squibbed."
      class="left"
    />

    <p>
      With the fall of Plugg and Scourge, our heroes found themselves the new
      captains of the merchant ship, the Man's Promise. The crew, grateful for
      their liberation from tyranny, swore their unwavering loyalty to the
      group. After a brief but profound discussion, Kasmira de la Torre was
      anointed as Captain, Finn as First Mate, Red as Master-of-Arms, and Varen
      as the Alchemist and Ship Mage. Their new roles cemented, the group turned
      to Kroop, the most knowledgeable in pirate ways aboard the ship, for
      counsel.
    </p>

    <p>
      Kroop advised them to take the Man’s Promise to Rickety’s Squibs for
      "squibbing," a process that would alter the ship's masts and rigging,
      giving it a new, unrecognizable profile. With determination and
      anticipation, they set sail for the hidden haven of Rickety’s Squibs. Upon
      arrival, they received a signal from the watchtower, granting them passage
      into the estuary. There, they were greeted by Rickety Hake and his men.
      Hake, with a keen eye, assessed the Man's Promise and named his price.
      Eager to see their ship transformed, the crew agreed, and the Man's
      Promise was towed into dry dock to begin its metamorphosis.
    </p>

    <p>
      As work commenced, the crew mingled with the off-duty workers, sharing
      tales of infamy and plunder. The locals, charmed by the stories, invited
      the crew to games of ninepins and rounds of beer. It was during one such
      event that disaster struck. A juvenile water naga, driven mad by the
      drought conditions, attacked, pulling a local into the river's depths.
      Without hesitation, Finn and Varen dove in, followed by Red, who cast a
      bubble spell on himself. Confronting the enraged naga, they discovered her
      home had been devastated by the drought. With swift and coordinated
      efforts, they dispatched the naga and rescued the local, earning the
      profound gratitude of Rickety and the island's inhabitants.
    </p>

    <p>
      The oppressive heat weighed heavily on everyone, and on the fourth day of
      their stay, a swarm of giant wasps, displaced by the weather and drawn to
      the noise of construction, descended upon the village. The heroes sprang
      into action, battling the horse-sized insects and saving many lives.
      Amidst the chaos, a Chelish galleon slipped into the estuary unnoticed,
      anchoring nearby and dispatching a boat towards the shore. Panic ensued,
      as many feared an attack by the Chelish navy. However, it soon became
      clear that this was another group of pirates seeking to have their ship
      squibbed.
    </p>

    <p>
      The tension was palpable as the captain of the galleon, Free Captain
      Merrill Pegsworthy, realized his blunder—intruding on the secret
      operations of Rickety’s Squibs. Preparing for a confrontation, he and his
      crew readied themselves for a fight. But Kasmira, with calm authority,
      stepped forward, reassuring Captain Pegsworthy that they meant no harm.
      Grateful for the reprieve, Pegsworthy asked if he could christen the newly
      transformed ship. Knowing it was considered good luck for a ship to be
      christened by a Free Captain, the crew readily agreed, easing the tensions
      and bringing a sense of camaraderie to the gathering.
    </p>

    <p>
      However, Rickety Hake remained troubled. His lookout had failed to stop
      the galleon, and Pegsworthy confirmed no flag had been flown. Rickety
      requested the heroes to check on his man, fearing something amiss.
      Agreeing to help, they embarked on a trek through treacherous terrain.
      Upon reaching the lookout's post, they found a grim scene—the lookout had
      been attacked by wasps and succumbed to a severe allergic reaction. With
      heavy hearts, they returned to Rickety, bearing the sad news.
    </p>

    <p>
      The Man's Promise was on the brink of a new chapter, its crew forged in
      the fires of battle and bound by loyalty and honor. As they prepared to
      sail under their new Captain, the specter of future adventures loomed
      large on the horizon, promising both peril and glory on the high seas.
    </p>
  </article>
</main>

<style>
  /* Adventure Log Styles */
  .blog {
    width: 100%;
    border-bottom: 1px solid black;
  }

  .blog img {
    width: 100%;
  }

  .blog h2 {
    text-align: start;
    font-size: 1.4em;
  }

  .dropdown {
    position: relative;
    display: inline-block;
    margin-bottom: 30px;
  }

  .dropbtn {
    background-color: var(--secondary);
    color: var(--text);
    font-size: 28px;
    border: 1px solid var(--text);
    cursor: pointer;
    border-radius: 20px;
    padding: 10px;
  }

  .dropdown-content {
    display: none;
    position: absolute;
    font-family: Alkatra, Arial, Helvetica, sans-serif;
    background-color: #f9f9f9;
    min-width: 140px;
    box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
    left: 60px;
    z-index: 1;
  }

  .dropdown-content a {
    color: black;
    padding: 8px 25px;
    text-decoration: none;
    display: block;
    border: 1.5px solid var(--background);
  }

  .dropdown-content a:hover {
    background-color: #f1f1f1;
  }

  .dropdown:hover .dropdown-content {
    display: block;
    border: 1px solid var(--text);
  }

  .dropdown:hover .dropbtn {
    background-color: var(--tertiary);
  }

  @media screen and (min-width: 1000px) {
    .blog {
      width: 70%;
      padding: 10px;
      border-bottom: 1px solid black;
      margin: auto;
    }

    .blog .left {
      float: left;
      width: 35%;
      margin-right: 20px;
    }
    /*
    .blog .right {
      float: right;
      width: 35%;
      margin-right: 20px;
    } */
  }
</style>
