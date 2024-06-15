<script>
  import { onMount } from "svelte";

  onMount(() => {
    if (typeof window !== "undefined") {
      const navicon = document.getElementById("navicon");
      const navMenu = document.getElementById("navMenu");

      if (navicon && navMenu) {
        navicon.addEventListener("click", () => {
          navMenu.style.display =
            navMenu.style.display === "block" ? "none" : "block";
        });
      } else {
        console.error("Navicon or NavMenu element not found");
      }
    }
  });
</script>

<header>
  <img src="images/PathSixLogowhite.png" alt="The Pathfinder 6" id="mainLogo" />
  <nav class="navFirst">
    <button id="navicon"><img src="images/navicon.png" alt="Menu" /></button>
    <ul id="navMenu">
      <img src="images/flagfill.png" alt="pirate flag" id="headerFlag" />
      <li><a href="/">Home Page</a></li>
      <li><a href="/adventure">Adventure Log</a></li>
      <li><a href="/dice">Dice Roller</a></li>
      <li><a href="/JadeRegent">Jade Regent</a></li>
      <li><a href="/rules">Rules Page</a></li>
      <img src="images/flagfill.png" alt="pirate flag" id="headerFlag" />
    </ul>
  </nav>
</header>

<slot />

<hr />
<footer>
  <div id="foot">
    <ul>
      <li><a href="/">Home Page</a></li>
      <li><a href="/adventure">Adventure Log</a></li>
      <li><a href="/dice">Dice Roller</a></li>
      <li><a href="/JadeRegent">Jade Regent</a></li>
      <li><a href="/rules">Rules Page</a></li>
    </ul>
    <img src="/images/flagfill.png" alt="pirate flag" id="footerFlag" />
    <p>All Rights Reserved</p>
  </div>
  <a href="https://www.pathsixdesigns.com" id="foot2">PathSix Web Design</a>
</footer>

<style>
  /* Navigation Styles */
  nav ul {
    display: none;
    list-style: none;
    list-style-image: none;
    list-style-type: none;
  }

  a {
    text-decoration: none;
    font-size: 1.3em;
    line-height: 1.6em;
    color: var(--text);
  }

  footer ul {
    list-style: none;
  }

  footer a {
    color: var(--background);
    font-size: 0.9em;
  }

  #navicon {
    background: var(--background);
    border: none;
  }

  #mainLogo {
    width: 100%;
  }

  #headerFlag {
    width: 15%;
  }

  /* footer styles */
  #foot {
    display: flex;
    background-color: var(--tertiary);
    color: var(--background);
    justify-content: center;
    align-items: center;
    clear: both;
  }

  #footerFlag {
    width: 20%;
    margin: 5px;
  }

  #foot2 {
    display: flex;
    background-color: var(--tertiary);
    color: var(--background);
    justify-content: center;
  }

  @media screen and (min-width: 1000px) {
    #mainLogo {
      width: 28%;
    }

    /* Navigation Styles */
    button#navicon {
      display: none;
    }

    nav ul {
      display: flex;
      flex-flow: row nowrap;
      flex: 1 1 auto;
    }

    nav ul li {
      line-height: 1.5em;
      width: 100%;
      margin-left: -2.5%;
    }

    .navFirst ul li a {
      color: var(--text);
      display: block;
      text-align: center;
      font-size: 1.1em;
      line-height: 1.8em;
      font-weight: bold;
    }

    .navFirst li a:active,
    .navFirst li a:hover {
      background-color: var(--tertiary);
      color: black;
    }

    #headerFlag {
      width: 5%;
      margin-left: -2%;
      z-index: 100;
    }

    /* Footer Styles */
    #footerFlag {
      margin: 20px 40px;
    }
  }
</style>
