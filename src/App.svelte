<script>
  import { timer } from "rxjs";

  var message = "-";

  timer(0, 1000).subscribe(value => (message = Date()));
</script>

<style>
  main {
    /* text-align: center; */
    padding: 1em;
    max-width: 240px;
    /* margin: 0 auto; */
  }

  h1 {
    color: #ff3e00;
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

<main>
  <h1>{message}</h1>
</main>
