<script>
  import { onMount } from "svelte";

  onMount(() => {
    // Fetch blog data and populate the container
    fetch("/adventure")
      .then((response) => response.text())
      .then((data) => {
        const parser = new DOMParser();
        const doc = parser.parseFromString(data, "text/html");
        const blogContainer = document.getElementById("blog-container");
        const newSection = doc.getElementById("new");

        // Find the h2 title, h3 date, img and first paragraph in the 'new' section
        const title = newSection.querySelector("h2");
        const date = newSection.querySelector("h3");
        const image = newSection.querySelector("img");
        const firstParagraph = newSection.querySelector("p");

        // Create and append the elements to the blog container
        if (title) {
          const entryTitle = document.createElement("h2");
          entryTitle.innerHTML = title.innerHTML;
          blogContainer.appendChild(entryTitle);
        }

        if (date) {
          const entryDate = document.createElement("h3");
          entryDate.innerHTML = date.innerHTML;
          blogContainer.appendChild(entryDate);
        }

        if (firstParagraph) {
          const entryParagraph = document.createElement("p");
          entryParagraph.innerHTML = firstParagraph.innerHTML;
          blogContainer.appendChild(entryParagraph);
        }
      })
      .catch((error) => {
        console.log("An error occurred:", error);
      });

    // Initialize scroll effect after fetching data
    const images = document.querySelectorAll(".container4 img");

    // Define the Intersection Observer
    const observer = new IntersectionObserver(
      (entries, observer) => {
        entries.forEach((entry, index) => {
          if (entry.isIntersecting) {
            setTimeout(() => {
              entry.target.classList.add("pop");
              observer.unobserve(entry.target);
            }, 500 * index); // Delay the animation here!
          }
        });
      },
      {
        threshold: 0.1,
        rootMargin: "-150px 0px 0px 0px",
      }
    );

    // Observe each image
    images.forEach((image) => {
      observer.observe(image);
    });
  });
</script>

<main>
  <div class="hero">
    <img src="/images/heroAlt.jpg" alt="Ship on the sea" class="ship" />
    <div class="heroWelcome">
      <h1>Welcome To Our Game Page!</h1>
      <h2>"Skull & Shackles"</h2>
    </div>
    <div class="heroBottom">
      <h3>The high seas adventure has begun!</h3>
      <p>
        Welcome to our thrilling journey through the lawless Shackles, where
        danger and discovery intertwine! Follow our intrepid adventurers as they
        navigate uncharted territories in search of adventure. What secrets do
        the Shackles hold? What challenges will our adventurers face? Dive into
        our adventure log and join us to uncover what lies ahead for the
        intrepid crew of the pirate ship, <i>Scourge's Bane</i>!
      </p>
      <h2>Follow Our Party's Journey!</h2>
      <p>Warning! Spoilers for the "Skull & Shackles" Adventure Path.</p>
      <button onclick="window.location.href='/adventure';">Adventure Log</button
      >
    </div>
  </div>

  <section class="container1">
    <div id="shackles">
      <h3>The Adventure Path</h3>
      <p>
        We are playing the "Skull & Shackles" Adventure Path sold by Paizo, Inc.
      </p>
      <blockquote>
        There's adventure to be had on the high seas when a group of
        press-ganged strangers seizes a ship and becomes embroiled in the plots
        and politics of the Shackles—an infamous island chain dominated by
        pirate warlords. But as these new swashbucklers make names for
        themselves, rival scalawags, enemy navies, legendary sea monsters, and
        the infamous Hurricane King himself seek to see them walk the plank. Who
        will survive when there's glory to plunder?
      </blockquote>
      <cite> &mdash; Paizo Adventure Path Teaser </cite>
    </div>
    <a href="/images/shacklesMap.jpg"
      ><img
        src="images/shacklesMap.jpg"
        alt="Shackes Map"
        id="shacklesMap"
      /></a
    >
  </section>

  <aside class="container2">
    <a href="https://www.d20srd.org/srd/variant/classes/gestaltCharacters.htm"
      ><img
        src="images/gestalt-link.jpg"
        alt="Link to Gestalt characters rules"
      /></a
    >
    <a
      href="https://www.aonprd.com/Rules.aspx?Name=Fast-Play%20Ship%20Combat&Category=Water"
      ><img src="images/ship-combat-link.jpg" alt="Ship Combat rules" /></a
    >
    <a href="/JadeRegent/index.html"
      ><img src="images/jade-regent-link.jpg" alt="Our last adventure" /></a
    >
  </aside>

  <div class="container3">
    <img
      src="/images/ship-side.png"
      alt="The side of a ship and the nearby coast"
    />
  </div>

  <div class="container4 pop">
    <h1>The Crew</h1>
    <div class="subCon1">
      <figure>
        <img src="/images/Kasmira.jpg" alt="Kasmira" />
        <figcaption>
          <p>Kasmira de la Torre</p>
          <p>Human Gunslinger/Rogue</p>
          <a href="/images/Kasmira.pdf"><u>Character Sheet</u></a>
        </figcaption>
      </figure>
      <img src="/images/Kasmira.jpg" alt="Kasmira" class="kasmira" />

      <figure id="finn">
        <figcaption>
          <p>Finn</p>
          <p>Undine Kineticist/Rogue</p>
          <a href="/images/Finn.pdf"><u>Character Sheet</u></a>
        </figcaption>
        <img src="/images/Finn.jpg" alt="Finn" />
      </figure>
      <img src="/images/Finn.jpg" alt="Finn" class="finn" />
    </div>
    <div class="empty"></div>
    <div class="subCon2">
      <figure id="red">
        <figcaption>
          <p>Red</p>
          <p>Dwarven Inquisitor/War Priest</p>
          <a href="/images/Red.pdf"><u>Character Sheet</u></a>
        </figcaption>
        <img src="/images/red.jpg" alt="Red" />
      </figure>
      <img src="/images/red.jpg" alt="Red" class="red" />

      <figure>
        <img src="/images/Varen.jpg" alt="Varen" />
        <figcaption>
          <p>Varen Galashantar</p>
          <p>Aquatic Elf Gunslinger/Magus</p>
          <a href="/images/Varen.pdf"><u>Character Sheet</u></a>
        </figcaption>
      </figure>
      <img src="/images/Varen.jpg" alt="Varen" class="varen" />
    </div>
  </div>
  <hr />
  <section class="container5">
    <div>
      <div class="blog2">
        <h3>An excerpt from our last adventure entry:</h3>
      </div>
      <div class="blog2" id="blog-container"></div>
      <div class="blog2">
        <p>
          You can find our entire story in the <a href="/adventure"
            >Adventure Log</a
          >
        </p>
      </div>
      <div class="blog3">
        <a href="images/gallery-image10.jpg"
          ><img src="images/gallery-image10.jpg" alt="Mini Gallery Images" /></a
        >
        <a href="images/gallery-image11.jpg"
          ><img src="images/gallery-image11.jpg" alt="Mini Gallery Images" /></a
        >
      </div>
    </div>

    <div class="blog3">
      <h3>Miniatures Gallery</h3>
      <a href="images/gallery-image13.jpg"
        ><img src="images/gallery-image13.jpg" alt="Mini Gallery Images" /></a
      >
      <a href="images/gallery_image9.jpg"
        ><img src="images/gallery_image9.jpg" alt="Mini Gallery Images" /></a
      >
      <a href="images/gallery_image3.jpg"
        ><img src="images/gallery_image3.jpg" alt="Mini Gallery Images" /></a
      >
      <a href="images/gallery_image5.jpg"
        ><img src="images/gallery_image5.jpg" alt="Mini Gallery Images" /></a
      >
      <a href="images/gallery_image6.jpg"
        ><img src="images/gallery_image6.jpg" alt="Mini Gallery Images" /></a
      >
      <a href="images/gallery_image7.jpg"
        ><img src="images/gallery_image7.jpg" alt="Mini Gallery Images" /></a
      >
    </div>
  </section>
</main>

<style>
  /* Hero Section */
  .ship {
    width: 100%;
    margin: 0;
    padding: 0;
  }

  /* Body Styles */
  #shacklesMap {
    width: 100%;
    margin: 0;
  }

  .container2 {
    display: flex;
    justify-content: space-around;
    align-items: center;
    box-shadow: inset 0 -4px 8px #ffff(0, 0, 0, 0.2);
    padding: 20px;
  }

  .container2 img {
    width: 100%;
    border-radius: 10px;
  }

  .container3 {
    display: flex;
    justify-content: space-around;
    align-items: center;
    background: linear-gradient(to bottom, #30393e 0%, black 100%);
  }

  .container3 img {
    width: 100%;
  }

  .container4 {
    background: black;
    background-image: url(/images/skull-background.png);
    background-repeat: no-repeat;
    background-position: center;
    background-size: 40%;
    justify-content: space-between;
  }

  .container4 img {
    width: 100%;
  }

  .container5 > div {
    flex: 1;
    width: 100%;
  }

  .finn,
  .kasmira,
  .red,
  .varen {
    display: none; /* Hidden by default */
    position: absolute; /* Positioned absolutely */
    max-width: 450px;
    top: 10%; /* Centered vertically */
    left: 35%; /* Centered horizontally */
    transform: translate(-50%, -50%); /* Offset the centering */
    z-index: 10; /* Higher z-index to ensure they appear above other content */
  }

  #red,
  #finn {
    display: flex;
    flex-direction: column-reverse;
  }

  .empty {
    height: 200px;
  }

  /* Quote Styles */
  blockquote {
    margin: 10px 10px 20px 30px;
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

  /* Adventure Log on Main Page */

  .blog2,
  .blog3 {
    width: 100%;
    padding: 10px;
    margin: 20px 0;
  }

  .blog3 img {
    width: 48%;
  }

  @media screen and (min-width: 1000px) {
    /* Hero Styles */

    .heroWelcome {
      color: var(--text);
      position: absolute;
      top: 45%;
      left: 35%;
      transform: translate(-50%, -50%);
    }

    .heroBottom {
      width: 40%;
      position: absolute;
      top: 75%;
      left: 35%;
      transform: translate(-50%, -50%);
      text-align: center;
    }

    /* Button Styles */
    button {
      margin: 20px 0 30px 25px;
      width: 250px;
      height: 40px;
      transition: transform 0.3s ease;
      border-radius: 10px;
      font-family: Alkatra, Georgia, "Times New Roman", Times, serif;
      font-size: 18px;
      color: var(--text);
      background-color: var(--background);
    }

    /* Body Styles */

    .container1 {
      display: flex;
      justify-content: space-around;
      align-items: center;
      box-shadow: inset 0 -4px 8px #ffff(0, 0, 0, 0.2);
      border: 0.25px solid #dcdcdc;
      background: linear-gradient(to bottom, black 0%, #30393e 100%);
      padding: 20px;
    }

    #shackles {
      width: 50%;
      padding: 0 30px;
    }

    #shacklesMap {
      width: 100%;
    }

    .container4 {
      display: flex;
      background: black;
      background-image: url(/images/skull-background.png);
      background-repeat: no-repeat;
      background-position: center;
      background-size: 40%;
      justify-content: space-between;
      flex-direction: column;
    }

    .container4 img {
      width: 40%;
      opacity: 0;
      cursor: pointer;
      min-height: 330px;
    }

    .subCon1 figure {
      display: flex;
      width: 30%;
      margin: 25px;
      align-items: center;
    }

    .subCon2 figure {
      display: flex;
      width: 30%;
      margin: 25px 0;
      align-items: center;
    }

    .subCon1 img,
    .subCon2 img {
      box-shadow: 10px 25px 30px 0px rgba(128, 128, 128, 0.6);
      margin: 10px;
    }

    .subCon1 {
      display: flex;
      justify-content: space-between;
      width: 100%;
      padding-left: 30px;
    }

    .subCon2 {
      display: flex;
      justify-content: space-around;
      width: 100%;
    }

    #red,
    #finn {
      display: flex;
      flex-direction: row; /* Align items in a row to fix column-reverse from mobile */
    }

    #red figcaption,
    #finn figcaption {
      text-align: right;
    }

    figcaption {
      font-size: 1.3em;
      font-family: Alkatra, Verdana, Geneva, Tahoma, sans-serif;
    }

    @keyframes pop {
      from {
        transform: scale(0.8) translateY(50px);
        opacity: 0;
      }
      to {
        transform: scale(1) translateY(0px);
        opacity: 1;
      }
    }

    .pop {
      animation: pop 0.5s ease-in-out forwards;
    }

    figure:hover + img {
      display: block;
    }

    .empty {
      height: 0;
    }

    .container5 {
      display: flex;
    }

    /* Adventure Log on Main Page */

    .blog3 img {
      width: 30%;
    }
  }
</style>
