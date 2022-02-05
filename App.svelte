<script>
  import Auth from "./Auth.svelte";
  import Calendar from "./Calendar.svelte";
  import { supabase } from "./dbClient.js";
  import { user } from "./sessionStore";

  user.set(supabase.auth.user());

  supabase.auth.onAuthStateChange((_, session) => {
    user.set(session.user);
    console.log("User from session", $user);
  });
</script>

<style>
  main {
    font-family: Tahoma, sans-serif;
    text-align: center;
    height: 100vh;
    width: 100vw;
  }
  h1 {
    margin: 0px;
    padding: 20px 15px;
  }
  div {
    font-size: 1.2rem;
  }

  .glow {
    color: black;
    text-align: center;
    -webkit-animation: glow 1s ease-in-out infinite alternate;
    -moz-animation: glow 1s ease-in-out infinite alternate;
    animation: glow 1s ease-in-out infinite alternate;
  }

  @-webkit-keyframes glow {
    from {
      text-shadow: 0 0 10px #fff, 0 0 20px #fff, 0 0 30px #e60073,
        0 0 40px #e60073, 0 0 50px #e60073, 0 0 60px #e60073, 0 0 70px #e60073;
    }
    to {
      text-shadow: 0 0 20px #fff, 0 0 30px #ff4da6, 0 0 40px #ff4da6,
        0 0 50px #ff4da6, 0 0 60px #ff4da6, 0 0 70px #ff4da6, 0 0 80px #ff4da6;
    }
  }
</style>

<main >
	<h1 class="glow">Biggis Burning Wheelz</h1>
  <p/>
  { #if $user }
	  <div class="glow">
      Hallo { $user.user_metadata?.name }, lass uns wissen wann du kommst!
    </div>
    <p/>
         <Calendar />
  {:else}
        <Auth />
  {/if}
</main>