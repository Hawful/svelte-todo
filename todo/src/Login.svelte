<script>
  import Profile from './Profile.svelte';

  import { authState } from 'rxfire/auth';
  import { signOut } from 'firebase/auth';
  import firebase from 'firebase/compat/app';

  let user;

  async function loginWithGoogle() {
    try {
      const provider = new firebase.auth.GoogleAuthProvider();

      user = await firebase.auth().signInWithPopup(provider);
    } catch (e) {
      console.log(e);
    }
  }
</script>

<section>
  {#if user}
    <Profile {...user} />
    <button on:click={() => signOut()}>Logout</button>
  {:else}
    <button on:click={loginWithGoogle}>Sign In with Google</button>
  {/if}
</section>
