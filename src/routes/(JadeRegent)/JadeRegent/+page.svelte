<script>
  import { onMount } from "svelte";

  var bannerArray = [
    "jaderegentImages/aelfread.png",
    "jaderegentImages/edam.png",
    "jaderegentImages/haldir.png",
    "jaderegentImages/shura.png",
    "jaderegentImages/tim.png",
  ];

  var headerArray = ["Aelfread", "Edam", "Haldir", "Shura", "Tim"];

  var subHeaderArray = [
    "Gestalt Inquisitor-Ninja",
    "Gestalt Paladin-Rogue",
    "Gestalt Wizard-Skald",
    "Gestalt Cleric-Paladin",
    "Gestalt Fighter-Bloodrager",
  ];

  var descriptionArray = [
    "Aelfread is a ghost of the battlefield, stalking his prey invisible and bringing the inquistion of Serenrae upon our foes.",
    "Edam is a little guy. Small of stature, huge on pain...dealing it.",
    "Haldir is a squishy mage. A squishy mage that has a whole lot of tricks up his sleeve. Don't mess with Haldir.",
    "Every party needs a healer. Every party needs a tank. Shura is our rock that heals. No really, he's a rock!",
    "Tim smashes things. That saying, \"You wouldn't like him when he's angry\" Yeah. Don't get on the wrong side of his rage.",
  ];

  var currentBanner = 0;

  function rotate() {
    var bannerPlace = document.getElementById("rotateImages");
    var headingElement = document.getElementById("heading");
    var subheadingElement = document.getElementById("subheading");
    var descriptionElement = document.getElementById("description");

    bannerPlace.src = bannerArray[currentBanner];
    headingElement.textContent = headerArray[currentBanner];
    subheadingElement.textContent = subHeaderArray[currentBanner];
    descriptionElement.textContent = descriptionArray[currentBanner];

    currentBanner++;

    if (currentBanner === bannerArray.length) {
      currentBanner = 0;
    }

    setTimeout(rotate, 4000);
  }

  onMount(() => {
    rotate();
  });

  function fetchAdventureLog() {
    fetch("/adventureLog")
      .then((response) => response.text())
      .then((data) => {
        const parser = new DOMParser();
        const doc = parser.parseFromString(data, "text/html");
        const lastEntryContainer = document.getElementById(
          "last-entry-container"
        );
        const lastHeader = doc.getElementById("newest");

        // Find the paragraphs after the 'newest' header until the next major break
        let currentNode = lastHeader.nextElementSibling;
        const lastParagraphs = [];

        while (
          currentNode &&
          currentNode.tagName !== "HR" &&
          currentNode.tagName !== "H4"
        ) {
          if (currentNode.tagName === "P") {
            lastParagraphs.push(currentNode);
          }
          currentNode = currentNode.nextElementSibling;
        }

        // Select the last two paragraphs from collected paragraphs
        const lastTwoParagraphs = lastParagraphs.slice(-2);

        if (lastHeader) {
          const entryHeader = document.createElement("h4");
          entryHeader.innerHTML = lastHeader.innerHTML;
          lastEntryContainer.appendChild(entryHeader);
        }

        lastTwoParagraphs.forEach((paragraph, index) => {
          const entryParagraph = document.createElement("p");
          entryParagraph.innerHTML = paragraph.innerHTML;
          lastEntryContainer.appendChild(entryParagraph);

          // Add <br> except after the last paragraph
          if (index < lastTwoParagraphs.length - 1) {
            lastEntryContainer.appendChild(document.createElement("br"));
          }
        });
      })
      .catch((error) => {
        console.log("An error occurred:", error);
      });
  }

  onMount(() => {
    fetchAdventureLog();
  });
</script>

<svelte:head>
  <link rel="stylesheet" href="/css/jr_styles.css" />
</svelte:head>

<body>
  <header class="header1">
    <div class="head">
      <img
        src="jaderegentImages/PathSixLogo2.png"
        alt="The Pathfinder 6"
        id="mainLogo"
      />
    </div>
    <nav class="navFirst">
      <a href="#" id="navicon"
        ><img src="jaderegentImages/navicon.png" alt="" /></a
      >
      <ul>
        <li><a href="/">Home Page</a></li>
        <li><a href="/JadeRegent">Jade Regent Home</a></li>
        <li><a href="/adventureLog">Adventure Log</a></li>
        <li><a href="/characters">Characters</a></li>
        <li><a href="/about">About Us</a></li>
      </ul>
    </nav>

    <div class="hero">
      <img
        src="jaderegentImages/gateHero.webp"
        alt="Doors to Adventure"
        class="doors"
      />
      <div class="heroCenter">
        <h1>Welcome To Our Game Page!</h1>
        <h1>"The Jade Regent"</h1>
      </div>
      <div class="heroBottom">
        <h3>Our Adventures in Tian Xia Have Concluded!</h3>
        <p>
          Thank you for joining our party of adventures. They have finished
          their quest in the Lands of Minkai and have successfully restored the
          rightful ruler to the throne. The adventure is chronicled in the
          Adventure Log. Enjoy and we hope you join us in our new adventure,
          "Skull & Shackles."
        </p>

        <h3>Follow Our Party's Journey!</h3>
        <p>Warning! Spoilers for the "Jade Regent" Adventure Path.</p>
        <button onclick="window.location.href='adventureLog.html';"
          >Adventure Log</button
        >
      </div>
    </div>
  </header>

  <main class="containerIndex">
    <section class="container1">
      <article>
        <h3>The Adventure Path</h3>
        <a href="images/TianXia-min.png"
          ><img
            src="jaderegentImages/TianXia-min.png"
            alt="Tian Xia Map"
            id="tianMap"
          /></a
        >
        <p>
          We are playing the "Jade Regent" Adventure Path sold by Paizo, Inc.
        </p>
        <blockquote>
          When a decades-old secret is exposed, an unassuming local tavern-owner
          and a close friend of the PCs discovers her birthright is to rule one
          of the ancient Dragon Empires of Tian Xia—the empire of Minkai. Yet
          the current ruler of this empire, the mysterious and increasingly
          cruel Jade Regent, has no intention of giving up his hold over the
          throne. In order to save Minkai from a would-be tyrant, the PCs must
          not only escort their friend from Varisia to Tian Xia, braving the
          frozen horrors of the Crown of the World, but must aid her in gaining
          the trust and support of a nation on the edge of anarchy.
        </blockquote>
        <cite> &mdash; Paizo Adventure Path Teaser </cite>
      </article>
      <br />
      <article>
        <br /><br />
        <h3>Our Game</h3>
        <p>
          Our group currently consists of a storyteller and five players. Our
          house rules are all a result of group discussion and consensus. Not
          everyone would enjoy our game, but we have a ton of fun. For example,
          if you read the house rules, you might notice that we banned a lot of
          classes, including the basic fighter class. This was based on our
          group playstyle where min maxed fighters could dominate the game. It
          was not done to punish a single player or even as a negative rule, but
          an agreement among the group that by removing this class, we'd have
          more fun as a whole. It's not perfect, especially with the gestalt
          builds that we are playing with now, but it's what we want for our
          game.
        </p>
        <p>
          Speaking of Gestalt leveling rules, they derive from the D&D 3.5
          ruleset. If you have never heard of it, you can read about the rules
          here:
        </p>
        <figure id="gestalt">
          <a
            href="https://www.d20srd.org/srd/variant/classes/gestaltCharacters.htm"
            ><img
              src="jaderegentImages/gestaltLink.png"
              alt="gestaltLink"
              id="gestLink"
            /></a
          >
          <figcaption>
            For the full character sheets, see the <a href="characters.html"
              ><b>characters page</b></a
            >.
          </figcaption>
        </figure>
      </article>
    </section>
    <section>
      <h1 class="rotation">The Cast:</h1>
      <div id="charRotate">
        <div class="rotator">
          <img
            id="rotateImages"
            src="jaderegentImages/aelfread.png"
            alt="Characters"
          />
        </div>
        <div class="rotatorText">
          <h2 id="heading">Aelfread</h2>
          <h5 id="subheading">Gestalt Inquisitor-Ninja</h5>
          <p id="description">
            Aelfread is a ghost of the battlefield, stalking his prey invisible
            and bringing the inquistion of Serenrae upon our foes.
          </p>
        </div>
      </div>
      <br />
      <div>
        <h3>An excerpt from our last adventure entry:</h3>
      </div>
      <div id="last-entry-container"></div>
      <h3>
        <a href="adventureLog.html">Click here to see the full Adventure Log</a>
      </h3>
    </section>

    <div id="eventHeader"><h1>Event Pictures</h1></div>
    <section class="events">
      <div>
        <a target="_blank" rel="noopener" href="jaderegentImages/adlog4.jpg"
          ><img src="jaderegentImages/adlog4.jpg" alt="" class="eventPic" /></a
        >
        <p class="eventDesc"></p>
      </div>

      <div>
        <a target="_blank" rel="noopener" href="jaderegentImages/adlog5.jpg"
          ><img src="jaderegentImages/adlog5.jpg" alt="" class="eventPic" /></a
        >
        <p class="eventDesc"></p>
      </div>

      <div>
        <a target="_blank" rel="noopener" href="jaderegentImages/adlog6.jpg"
          ><img src="jaderegentImages/adlog6.jpg" alt="" class="eventPic" /></a
        >
        <p class="eventDesc"></p>
      </div>

      <div>
        <a target="_blank" rel="noopener" href="jaderegentImages/adlog3.jpg"
          ><img src="jaderegentImages/adlog3.jpg" alt="" class="eventPic" /></a
        >
        <p class="eventDesc"></p>
      </div>

      <div>
        <a target="_blank" rel="noopener" href="jaderegentImages/adlog2.jpg"
          ><img src="jaderegentImages/adlog2.jpg" alt="" class="eventPic" /></a
        >
        <p class="eventDesc"></p>
      </div>

      <div>
        <a target="_blank" rel="noopener" href="jaderegentImages/adlog1.jpg"
          ><img src="jaderegentImages/adlog1.jpg" alt="" class="eventPic" /></a
        >
        <p class="eventDesc"></p>
      </div>
    </section>
  </main>

  <footer>
    <p>All Rights Reserved</p>
  </footer>
</body>

<style>
  @charset "utf-8";
  /*
   date: 3/12/23
*/

  /* Global Variables */

  main {
    max-width: 70%;
  }

  /* Text Styles */
  h1 {
    color: var(--accentColor);
    font-size: 2.3em;
    line-height: 2.4em;
    font-family: Alkatra, Verdana, Geneva, Tahoma, sans-serif;
    text-align: center;
    margin-top: 10px;
  }

  h3 {
    color: rgb(63, 17, 11);
    font-size: 1.5em;
    line-height: 1.5em;
    font-family: Alkatra, Verdana, Geneva, Tahoma, sans-serif;
    margin-top: 10px;
  }

  p {
    font-size: 1.1em16px;
    line-height: 1.5em;
    font-family: Georgia, "Times New Roman", Times, serif;
  }

  /* Link Styles */
  a {
    text-decoration: none;
    color: var(--accentColor);
  }
  a:active,
  a:hover {
    font-size: 1.2em;
    color: grey;
  }

  /* Button Styles */
  button {
    margin: 20px 0 30px 25px;
    width: 200px;
    height: 30px;
    transition: transform 0.3s ease;
    border-radius: 10px;
    font-family: Alkatra, Georgia, "Times New Roman", Times, serif;
    font-size: 18px;
    color: var(--lightText);
    background-color: var(--accentColor);
  }

  button:active,
  button:hover {
    background-color: grey;
  }

  button:active {
    width: 170px;
    height: 30px;
    background-color: var(--background);
    color: var(--accentColor);
  }

  /* Header Styles */

  header {
    background-color: var(--background);
  }

  .header1 {
    background-color: var(--heroBackground);
  }

  .head img {
    width: 30%;
    padding: 10px 0 0 10px;
  }

  /* Navigation List Styles */

  nav ul {
    display: flex;
    flex-flow: row nowrap;
    flex: 1 1 auto;
    list-style-type: none;
  }

  nav ul li {
    line-height: 2em;
    width: 100%;
  }

  .navFirst ul li a {
    color: var(--accentColor);
    display: block;
    text-align: center;
    font-size: 1.1em;
    line-height: 2.5em;
    font-weight: bold;
  }

  .navFirst li a:visited,
  .navFirst li a:active {
    color: var(--accentColor);
    line-height: 2.3em;
  }

  .navFirst a {
    background-color: var(--heroBackground);
  }
  .navSecond ul li a {
    color: var(--lightText);
    background-color: var(--accentColor);
    display: block;
    text-align: center;
    font-size: 1.1em;
    line-height: 2.5em;
    font-weight: bold;
  }

  .navSecond li a:visited,
  .navSecond li a:active {
    color: var(--background);
    line-height: 2.3em;
  }
  /* Hero Styles */

  .hero {
    position: relative;
  }

  img.doors {
    width: 100%;
  }

  .heroCenter {
    position: absolute;
    top: 15%;
    left: 50%;
    transform: translate(-50%, -50%);
  }

  .heroBottom {
    position: absolute;
    top: 85%;
    left: 50%;
    transform: translate(-50%, -50%);
    text-align: center;
  }

  /* Quote Styles */
  blockquote {
    margin: 10px 10px 20px 20px;
  }

  blockquote::before {
    content: open-quote;
    font-family: "Times New Roman", Times, serif;
    font-size: 1.6em;
    font-weight: bold;
  }

  blockquote::after {
    content: close-quote;
    font-family: "Times New Roman", Times, serif;
    font-size: 1.6em;
    font-weight: bold;
  }

  /* Section Styles */

  main {
    margin: 10px auto;
  }

  .containerIndex {
    margin-top: 40px;
  }

  .container1 {
    flex-basis: 65%;
    margin: 10px;
  }

  .container1 p {
    margin: 15px 0;
  }

  img#tianMap {
    float: right;
    width: 40%;
    margin: -20px 0 0 20px;
  }

  #gestalt {
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
  }

  figcaption {
    text-align: center;
  }

  /* Javascript Cast Rotation Section */

  #charRotate {
    display: flex;
    margin: 0 auto;
    justify-content: center;
    border-top: 1px solid black;
    border-bottom: 1px solid black;
  }

  .rotation {
    margin-top: 8%;
    border-top: 1px solid black;
  }

  .rotator {
    margin: 0;
    padding: 0;
    width: 20%;
  }

  #rotateImages {
    width: 100%;
    padding: 0;
  }

  .rotatorText {
    width: 35%;
    padding: 65px 0 0 4%;
    text-align: center;
  }
  /* Event Section */

  div#eventHeader {
    width: 60%;
  }

  .events {
    width: 60%;
    display: flex;
    justify-content: space-around;
    flex-wrap: wrap;
  }

  .events img {
    max-width: 300px;
    border-radius: 5px;
  }

  .events p {
    max-width: 300px;
    margin-bottom: 10px;
  }

  figure {
    text-align: center;
  }

  figcaption {
    font-size: 14px;
  }

  /* footer styles */
  footer {
    display: flex;
    background-color: var(--accentColor);
    color: var(--lightText);
    width: 100%;
    padding: 10px 20px;
    justify-content: space-between;
  }

  /* =============================
	Mobile Styles: 0 - 900 pixels
   =============================
*/
  @media only screen and (max-width: 900px) {
    .head img {
      width: 100%;
      margin: 0;
      padding: 0;
    }

    img.doors {
      width: 100%;
      margin: 0;
    }

    nav ul {
      display: none;
    }

    a#navicon:hover + ul,
    nav ul:hover {
      display: block;
    }

    h1 {
      line-height: 1.1em;
    }

    button:active,
    button:hover {
      width: 200px;
      height: 30px;
    }

    .hero {
      position: static;
      padding: 0;
      margin: 0;
      transform: none;
    }

    .heroCenter {
      position: static;
      width: 100%;
      font-size: 0.9em;
      padding: 0;
      margin: 0;
      transform: none;
    }

    .heroBottom {
      position: static;
      width: 100%;
      padding: 0;
      margin: 0;
      transform: none;
    }

    .container1,
    .events {
      flex-basis: 100%;
      margin: 0;
      padding: 1px;
    }

    /* Home Page Styles */

    img#tianMap {
      float: none;
      width: 100%;
      margin: 1px;
    }

    #gestLink {
      width: 100%;
    }

    .rotator {
      width: 100%;
    }

    .rotatorText {
      width: 100%;
      padding: 0;
      text-align: center;
    }

    .events {
      width: 100%;
      display: block;
    }

    footer {
      flex-basis: 100%;
    }
  }

  /* ============================================
   Tablet and Desktop Styles: 781px and greater 
   ============================================
*/

  @media only screen and (min-width: 901px) {
    a#navicon {
      display: none;
    }
  }
</style>
