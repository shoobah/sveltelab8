<script>
  import { timer } from "rxjs";
  import { scan } from "rxjs/operators";
  import Clock from "./components/clock.svelte";

  function getRandomRGB() {
    return Math.floor(Math.random() * 128);
  }

  function getRandomColor() {
    return `RGB(${getRandomRGB()},${getRandomRGB()},${getRandomRGB()})`;
  }

  var message = new Date();
  var color = getRandomColor();

  timer(0, 1000)
    .pipe(
      scan((acc, curr) => {
        var d = new Date();
        if (d.getSeconds() % 10 === 0) {
          color = getRandomColor();
        }
        return {
          date: d,
          color
        };
      })
    )
    .subscribe(value => {
      message = value.date;
    });
</script>

<style>
  main {
    padding: 1em;
    max-width: 240px;
  }

  h1 {
    color: var(--color);
    text-transform: uppercase;
    font-size: 2em;
    font-weight: 100;
    user-select: none;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>

<main style="--color:{color}">
  <h1>{message}</h1>
  <Clock time={message} />
</main>
