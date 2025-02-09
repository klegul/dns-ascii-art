<script lang="ts">
	let inputText = '';
	let formattedText = '';
	let domain = 'ascii.example.com';

	function formatText(text: string): string {
		if (!domain.endsWith('.')) {
			domain += '.';
		}

		let lines = text.split('\n');
		for (let i = 0; i < lines.length; i++) {
			lines[i] = `${domain} 1 IN NAPTR ${(i + 1) * 10} 10 "" "${lines[i]}" "" . ; DNS ASCII Art`
		}
		return lines.join('\n');
	}

	function handleFormat() {
		formattedText = formatText(inputText);
	}
</script>

<style>
	.box {
		width: 100%;
		height: calc(100vh - 100px);
		margin: 20px;
	}

	.container {
		display: flex;
		gap: 10px;
		height: 100%;
	}

	textarea {
		width: 100%;
		height: 100%;
	}

	.button-container {
		margin-top: 20px;
	}
</style>

<svelte:head>
	<title>DNS ASCII Art</title>
</svelte:head>

<div class="box">
	<div class="container">
		<textarea bind:value={inputText} placeholder="Enter text here..."></textarea>
		<textarea bind:value={formattedText} readonly placeholder="Formatted text..."></textarea>
	</div>
	<div class="button-container">
		<input type="text" bind:value={domain} placeholder="Domain"/>
		<button on:click={handleFormat}>Format Text</button>
	</div>
</div>

