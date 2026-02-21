<script lang="ts">
	import { authClient } from '$lib/auth-clients';
	import { goto } from '$app/navigation'
	let error = $state('');
	async function signup(e: Event) {
		e.preventDefault();
		const form = e.target as HTMLFormElement;
		const username = form.username.value;
		const email = form.email.value;
		const password = form.password.value;
		const password_confirm = form.password_confirm.value;
		if (password !== password_confirm) {
			error = 'Password ist not matching';
			return;
		}
		if (!username || !email || !password || !password_confirm) {
			error = 'All fields are required';
			return;
		}
		await authClient.signUp.email({
			email,
			password,
			name: username
		},
		{
  		onSucces: async () => {
  		//what you want to do after it
  		// got to homepage
      goto('/')
      }
		}
		}):
	}
</script>

<h1>Sign Up</h1>
<form>
	<div class="row">
		<label>
			Username:
			<input required type="text" id="username" />
		</label>
	</div>
	<div class="row">
		<label>
			E-Mail:
			<input required type="email" id="email" />
		</label>
	</div>
	<div class="row">
		<label>
			Password:
			<input required type="password" id="password" />
		</label>
	</div>
	<div class="row">
		<label>
			Confirm Password:
			<input required type="password" id="password_confirm" />
		</label>
	</div>
	<button type="submit"> Sign Up</button>
</form>
