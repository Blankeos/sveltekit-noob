<script lang="ts">
	import { css } from 'styled-system/css';
	import { stack, vstack, flex, hstack } from 'styled-system/patterns';

	let counter = 0;

	type Message = {
		sender: string;
		aligned: 'left' | 'right';
		content: string;
	};

	let messages: Message[] = [];

	let inputBox = '';

	function sendMessage() {
		console.log(messages, 'pushing in', inputBox);
		messages = [
			...messages,
			{
				sender: 'Carlo',
				aligned: 'right',
				content: inputBox
			}
		];
		inputBox = '';
	}

	const buttonCSS = css({
		background: 'orange.500',
		paddingY: '2.5',
		paddingLeft: '3.5',
		paddingRight: '3.5',
		rounded: 'md',
		color: 'white',
		_hover: {
			background: 'orange.600'
		},
		transition: 'ease-in-out 0.2s',
		cursor: 'pointer',
		margin: 0
	});
</script>

<h1>Carlo's Counter</h1>

<div
	class={css({
		fontSize: '2xl',
		fontWeight: 'bold'
	})}
/>
<div
	class={css({
		display: 'flex',
		fontSize: '3.5rem',
		justifyContent: 'center'
	})}
>
	{counter}
</div>
<div
	class={css({
		display: 'flex',
		justifyContent: 'center',
		columnGap: '10'
	})}
>
	<button class={buttonCSS} on:click={() => counter++}>Increase</button>
	<button class={buttonCSS} on:click={() => counter--}>Decrease</button>
</div>

<form
	on:submit={(e) => {
		e.preventDefault();
		sendMessage();
	}}
	class={css({
		maxWidth: 1280,
		width: 'full',
		background: 'green'
	})}
>
	<div
		class={vstack({
			background: 'white',
			height: '450px',
			gap: 0
		})}
	>
		<!-- Text Area -->
		<div
			class={css({
				width: 'full',
				height: '100%',
				borderBottom: '1px solid',
				borderColor: 'gray.200'
			})}
		>
			{#each messages as message (message.sender + message.content)}
				<div>{message.sender}: {message.content}</div>
			{/each}
		</div>
		<div
			class={hstack({
				gap: 0,
				width: 'full'
			})}
		>
			<input
				type="text"
				bind:value={inputBox}
				class={css({
					margin: 0,
					padding: 2,
					width: 'full',
					border: '1px solid',
					borderColor: 'orange.400',
					rounded: 'md',
					outline: 'none'
				})}
			/>
			<button type="submit" class={buttonCSS}>Send</button>
		</div>
	</div>
</form>
