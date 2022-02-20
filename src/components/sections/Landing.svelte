<script>
  // your script goes here
  const sentences = [
    "Jason Wandrag",
    "a frontend developer",
    "an authentic nerd",
    "creative and logical",
    "a JavaScript framework polyglot",
    "passionate about JavaScript",
  ];

  function waitForMs(ms) {
    return new Promise((resolve) => setTimeout(resolve, ms));
  }

  async function typeSentence(sentence, element, delay = 100) {
    const letters = sentence.split("");
    let i = 0;
    while (i < letters.length) {
      await waitForMs(delay);
      document.querySelector(element).append(letters[i]);
      i++;
    }
  }

  async function deleteSentence(element) {
    const sentence = document.querySelector(element).innerHTML;
    const letters = sentence.split("");
    while (letters.length > 0) {
      await waitForMs(100);
      letters.pop();
      document.querySelector(element).innerHTML = letters.join("");
    }
  }

  async function sentenceLoop(sentenceList, element) {
    let i = 0;
    while (true) {
      await typeSentence(sentenceList[i], element);
      await waitForMs(1500);
      await deleteSentence(element);
      await waitForMs(500);
      i++;
      if (i >= sentenceList.length) {
        i = 0;
      }
    }
  }

  sentenceLoop(sentences, "#text");
</script>

<!-- markup (zero or more items) goes here -->
<header id="landing">
  <h1>I am <span id="text"></span></h1>
</header>

<style>
  /* your styles go here */
  header {
    min-height: 100vh;
    background-size: cover;
    display: grid;
    place-items: center;
    padding: 50px;
  }
  h1 {
    width: 100%;
  }
  #text {
    position: relative;
    display: block;
    color: var(--blueGray1);
  }

  #text:after {
    content: "";
    width: 3px;
    height: 44px;
    background: var(--blue1);
    position: absolute;
    animation: blink 1.2s infinite;
  }

  @keyframes blink {
    0%,
    49% {
      background: var(--blue1);
    }
    50%,
    100% {
      background: var(--blue7);
    }
  }
</style>
