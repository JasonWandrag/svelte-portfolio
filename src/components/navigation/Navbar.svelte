<script>
  import Icon from "svelte-awesome/components/Icon.svelte";
  import {
    faHouse,
    faUser,
    faBriefcase,
    faCode,
    faLaptopCode,
    faCommentDots,
    faEnvelope,
    faGears,
    faBars,
  } from "@fortawesome/free-solid-svg-icons";

  // your script goes here
  export let menuVisible;

  const waitForMs = (ms) => {
    return new Promise((resolve) => setTimeout(resolve, ms));
  };
  const toggleNav = async (e) => {
    const x = e.clientX;
    const y = e.clientY;
    const nav = document.querySelector("#navbar");

    menuVisible = !menuVisible;

    if (!menuVisible) await waitForMs(250);
    nav.style.left = `${menuVisible ? x : "-300"}px`;
    nav.style.top = `${y}px`;
  };

  // For PC events
  window.oncontextmenu = (e) => {
    toggleNav(e);
    return false; // cancel default menu
  };

  // For mobile events
  const toggleNavMobile = async (e) => {
    const x = e.touches[0].pageX;
    const y = e.touches[0].pageY;
    const nav = document.querySelector("#navbar");

    menuVisible = !menuVisible;

    if (!menuVisible) await waitForMs(250);
    nav.style.left = `${menuVisible ? x : "-300"}px`;
    nav.style.top = `${y}px`;
  };
  document.querySelectorAll(".nav-button").forEach((btn) => {
    btn.addEventListener("click", (e) => {
      console.log("hello");
      toggleNavMobile(e);
    });
  });
  const touchduration = 200; //length of time we want the user to touch before we do something
  let timer;
  const onlongtouch = (e) => {
    console.log(e);
    toggleNavMobile(e);
    if (!menuVisible) clearTimeout(timer);
  };

  document.querySelector("body").addEventListener("touchstart", (e) => {
    // e.preventDefault();
    if (!timer) {
      timer = setTimeout(onlongtouch(e), touchduration);
    }
  });
  document.querySelector("body").addEventListener("touchend", (e) => {
    // e.preventDefault();
    if (timer) {
      clearTimeout(timer);
    }
  });

  const animationObserver = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        entry.target.classList.toggle("show", entry.isIntersecting);
      });
    },
    {
      threshold: 1,
    }
  );
  document.querySelectorAll("section").forEach((item) => {
    animationObserver.observe(item);
  });
</script>

<nav id="navbar" class:show="{menuVisible}">
  <a
    href="#landing"
    class:show="{menuVisible}"
    class="nav-button"
    on:click="{toggleNav}"><Icon data="{faHouse}" /></a
  >
  <a
    href="#about"
    class:show="{menuVisible}"
    class="nav-button"
    on:click="{toggleNav}"><Icon data="{faUser}" /></a
  >
  <a
    href="#resume"
    class:show="{menuVisible}"
    class="nav-button"
    on:click="{toggleNav}"><Icon data="{faBriefcase}" /></a
  >
  <a
    href="#skills"
    class:show="{menuVisible}"
    class="nav-button"
    on:click="{toggleNav}"><Icon data="{faCode}" /></a
  >
  <a
    href="#projects"
    class:show="{menuVisible}"
    class="nav-button"
    on:click="{toggleNav}"><Icon data="{faLaptopCode}" /></a
  >
  <a
    href="#testimonials"
    class:show="{menuVisible}"
    class="nav-button"
    on:click="{toggleNav}"><Icon data="{faCommentDots}" /></a
  >
  <a
    href="#contact"
    class:show="{menuVisible}"
    class="nav-button"
    on:click="{toggleNav}"><Icon data="{faEnvelope}" /></a
  >
  <button class:show="{menuVisible}" class="nav-button"
    ><Icon data="{faGears}" />
  </button>
  <button class:show="{menuVisible}" class="nav-button" on:click="{toggleNav}"
    ><Icon data="{faBars}" scale="2" /></button
  >
</nav>

<style>
  #navbar {
    position: fixed;
    transform: translate(-50%, -50%);
    transition: opacity 0.3s linear;
    opacity: 0;
    width: 0;
    height: 0;
    display: grid;
    place-items: center;
    left: -100%;
    color: white;
    border-radius: 50%;
    transition: all 300ms ease;
    transition-property: height, width, opacity;
  }
  #navbar.show {
    transition-delay: 300ms;
    opacity: 1;
    width: 120px;
    height: 120px;
    z-index: 100;
  }
  .nav-button {
    color: var(--blue6);
    background-color: var(--blueGray1);
    /* border: 2px solid var(--blue6); */
    border: none;
    text-align: center;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    border-radius: 50%;
    box-shadow: 0 3px 8px 0 rgb(15 15 20 / 20%);
    outline: none;
    height: 45px;
    width: 45px;
    transition: all 0.3s ease;
    transition-property: top, left, background-color, color;
    z-index: -1;
    cursor: pointer;
    display: grid;
    place-items: center;
  }

  .show .nav-button:last-child {
    transition: z-index 0.1s linear;
  }
  .nav-button:hover {
    color: var(--blueGray1);
    background-color: var(--blue6);
  }
  .nav-button.show {
    left: 50%;
    top: 0;
    z-index: 50;
    transition: all 0.3s cubic-bezier(0, 0, 0, 2.83);
    transition-property: top, left, color, background-color;
    /* transition-delay: 100ms; */
  }
  .nav-button.show:nth-child(2) {
    left: 85%;
    top: 15%;
    /* transition-delay: 200ms; */
  }
  .nav-button.show:nth-child(3) {
    left: 100%;
    top: 50%;
    /* transition-delay: 300ms; */
  }
  .nav-button.show:nth-child(4) {
    left: 85%;
    top: 85%;
    /* transition-delay: 400ms; */
  }
  .nav-button.show:nth-child(5) {
    left: 50%;
    top: 100%;
    /* transition-delay: 500ms; */
  }
  .nav-button.show:nth-child(6) {
    left: 15%;
    top: 85%;
    /* transition-delay: 600ms; */
  }
  .nav-button.show:nth-child(7) {
    left: 0;
    top: 50%;
    /* transition-delay: 700ms; */
  }
  .nav-button.show:nth-child(8) {
    left: 15%;
    top: 15%;
    /* transition-delay: 800ms; */
  }

  .nav-button.show:nth-child(9) {
    left: 50%;
    top: 50%;
    display: grid;
    place-items: center;
    transition: all 0.3s cubic-bezier(0, 0, 0, 2.83);
    width: 70px;
    height: 70px;
    font-size: 600px;
    transition-delay: 700ms;
    transition-property: width, height;
  }

  .nav-button.show:hover,
  .nav-button:hover {
    transition-delay: 0ms !important;
  }

  @media screen and (max-width: 720px) {
    #navbar {
      transform: scale(1.2);
    }
  }
</style>
