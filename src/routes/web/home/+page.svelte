<script lang="ts">
	import { browser } from '$app/environment';
	import data from '$lib/assets/data.json';
	import layout from '$lib/assets/Layouts.png';
	import { quintOut } from 'svelte/easing';
	import { fade, fly, type FlyParams } from 'svelte/transition';

	$: number = browser ? localStorage.getItem('control-number')?.replace('-', '&#8209;') : '';

	let name = '';
	let text = '';
	let datePosted = '';
	let imagePackage = '';

	let toastMessage = '';
	let timeout: number;

	const flyParams: FlyParams = {
		y: 100,
		duration: 600,
		easing: quintOut
	};

	$: if (toastMessage) {
		if (timeout) clearTimeout(timeout);
		timeout = setTimeout(() => (toastMessage = ''), 3000);
	}

	$: if (browser) document.body.style.overflow = text ? 'hidden' : '';

	function set(__name: string, __text: string, __datePosted: string, __images: string) {
		name = __name;
		text = __text;
		datePosted = __datePosted;
		imagePackage = __images;
	}

	function transformText(): string {
		const paragraphs = text.split('\n');
		const formattedParagraphs = paragraphs.map((p) => {
			if (p.length === 0) return '';

			p = p.replace(
				/[𝗔𝗕𝗖𝗗𝗘𝗙𝗚𝗛𝗜𝗝𝗞𝗟𝗠𝗡𝗢𝗣𝗤𝗥𝗦𝗧𝗨𝗩𝗪𝗫𝗬𝗭𝗮𝗯𝗰𝗱𝗲𝗳𝗴𝗵𝗶𝗷𝗸𝗹𝗺𝗻𝗼𝗽𝗾𝗿𝘀𝘁𝘂𝘃𝘄𝘅𝘆𝘇𝟬𝟭𝟮𝟯𝟰𝟱𝟲𝟳𝟴𝟵].+[𝗔𝗕𝗖𝗗𝗘𝗙𝗚𝗛𝗜𝗝𝗞𝗟𝗠𝗡𝗢𝗣𝗤𝗥𝗦𝗧𝗨𝗩𝗪𝗫𝗬𝗭𝗮𝗯𝗰𝗱𝗲𝗳𝗴𝗵𝗶𝗷𝗸𝗹𝗺𝗻𝗼𝗽𝗾𝗿𝘀𝘁𝘂𝘃𝘄𝘅𝘆𝘇𝟬𝟭𝟮𝟯𝟰𝟱𝟲𝟳𝟴𝟵]/g,
				(a) => '<strong>' + a.normalize('NFKD') + '</strong>'
			);
			p = p.replace(
				/[𝘼𝘽𝘾𝘿𝙀𝙁𝙂𝙃𝙄𝙅𝙆𝙇𝙈𝙉𝙊𝙋𝙌𝙍𝙎𝙏𝙐𝙑𝙒𝙓𝙔𝙕𝙖𝙗𝙘𝙙𝙚𝙛𝙜𝙝𝙞𝙟𝙠𝙡𝙢𝙣𝙤𝙥𝙦𝙧𝙨𝙩𝙪𝙫𝙬𝙭𝙮𝙯].+[𝘼𝘽𝘾𝘿𝙀𝙁𝙂𝙃𝙄𝙅𝙆𝙇𝙈𝙉𝙊𝙋𝙌𝙍𝙎𝙏𝙐𝙑𝙒𝙓𝙔𝙕𝙖𝙗𝙘𝙙𝙚𝙛𝙜𝙝𝙞𝙟𝙠𝙡𝙢𝙣𝙤𝙥𝙦𝙧𝙨𝙩𝙪𝙫𝙬𝙭𝙮𝙯]/g,
				(a) => '<strong><em>' + a.normalize('NFKD') + '</em></strong>'
			);
			p = p.replace(
				/[𝐀𝐁𝐂𝐃𝐄𝐅𝐆𝐇𝐈𝐉𝐊𝐋𝐌𝐍𝐎𝐏𝐐𝐑𝐒𝐓𝐔𝐕𝐖𝐗𝐘𝐙𝐚𝐛𝐜𝐝𝐞𝐟𝐠𝐡𝐢𝐣𝐤𝐥𝐦𝐧𝐨𝐩𝐪𝐫𝐬𝐭𝐮𝐯𝐰𝐱𝐲𝐳𝟎𝟏𝟐𝟑𝟒𝟓𝟔𝟕𝟖𝟗].+[𝐀𝐁𝐂𝐃𝐄𝐅𝐆𝐇𝐈𝐉𝐊𝐋𝐌𝐍𝐎𝐏𝐐𝐑𝐒𝐓𝐔𝐕𝐖𝐗𝐘𝐙𝐚𝐛𝐜𝐝𝐞𝐟𝐠𝐡𝐢𝐣𝐤𝐥𝐦𝐧𝐨𝐩𝐪𝐫𝐬𝐭𝐮𝐯𝐰𝐱𝐲𝐳𝟎𝟏𝟐𝟑𝟒𝟓𝟔𝟕𝟖𝟗]/g,
				(a) => "<strong class='serif'>" + a.normalize('NFKD') + '</strong>'
			);
			p = p.replace(
				/[𝑨𝑩𝑪𝑫𝑬𝑭𝑮𝑯𝑰𝑱𝑲𝑳𝑴𝑵𝑶𝑷𝑸𝑹𝑺𝑻𝑼𝑽𝑾𝑿𝒀𝒁𝒂𝒃𝒄𝒅𝒆𝒇𝒈𝒉𝒊𝒋𝒌𝒍𝒎𝒏𝒐𝒑𝒒𝒓𝒔𝒕𝒖𝒗𝒘𝒙𝒚𝒛].+[𝑨𝑩𝑪𝑫𝑬𝑭𝑮𝑯𝑰𝑱𝑲𝑳𝑴𝑵𝑶𝑷𝑸𝑹𝑺𝑻𝑼𝑽𝑾𝑿𝒀𝒁𝒂𝒃𝒄𝒅𝒆𝒇𝒈𝒉𝒊𝒋𝒌𝒍𝒎𝒏𝒐𝒑𝒒𝒓𝒔𝒕𝒖𝒗𝒘𝒙𝒚𝒛]/g,
				(a) => "<strong class='serif'><em>" + a.normalize('NFKD') + '</em></strong>'
			);
			p = p.replace(/\#(\w+)/g, (a, p1) => `<a href="facebook.com/hashtag/${p1}">${a}</a>`);
			p = p.replace(
				/(http(s)?:\/\/.)?(www\.)?[-a-zA-Z0-9@:%._\+~#=]{2,256}\.[a-z]{2,6}\b([-a-zA-Z0-9@:%_\+.~#?&//=]*)/g,
				(a) => `<a href="${a}">${a}</a>`
			);
			return `<p>${p.trim()}</p>`;
		});

		return formattedParagraphs.filter(p => p !== "<p></p>").join('\n');
	}

	function clickOutside(node: HTMLElement) {
		node.addEventListener('click', (e) => {
			if ((e.target as HTMLElement).closest('.content-window') === null) {
				text = '';
			}
		});
	}

	function copyHtml() {
		navigator.clipboard
			.writeText(transformText())
			.then(() => (toastMessage = 'Copied raw HTML to clipboard'));
	}

	function copyText() {
		navigator.clipboard.writeText(text).then(() => (toastMessage = 'Copied raw text to clipboard'));
	}
</script>

<div class="container" in:fly={{ ...flyParams, delay: 300 }}>
	{#if number}
		{#key toastMessage}
			<div class="toast" transition:fly={{ y: '-10vh' }} class:hidden={toastMessage === ''}>
				{toastMessage}
			</div>
		{/key}

		<div class="content">
			<div class="dl-links">
				<h1>Welcome, {@html number?.toUpperCase()}!</h1>
				<p>Download the articles and photos below to get started.</p>

				<div class="table">
					<section>
						<strong>Section Name</strong>
						<strong>Type</strong>
					</section>

					{#each data as { name, type, link, content }}
						<section>
							<span>{name}</span>
							<span>{type}</span>

							{#if link}
								<a href="/links/{link}" class="button" download={name} title="Download {name}">
									<i class="ph-bold ph-download-simple"></i>
								</a>
							{:else if content}
								<button
									title="Open {name}"
									on:click={() => set(name, content.text, content['date-posted'], content.images)}
								>
									<i class="ph-bold ph-download-simple"></i>
								</button>
							{/if}
						</section>
					{/each}
				</div>

				{#if text}
					<div class="dialog" transition:fade use:clickOutside>
						<div class="content-window" transition:fly={flyParams}>
							<button class="close" on:click={() => (text = '')}
								><i class="ph-bold ph-x"></i></button
							>
							<h1>{name}</h1>

							<div class="head">
								<small>CONTENT</small>
								<button title="Copy Raw HTML" on:click={copyHtml}
									><i class="ph-bold ph-file-html"></i></button
								>
								<button title="Copy Raw Text (Formatted)" on:click={copyText}
									><i class="ph-bold ph-file-txt"></i></button
								>
							</div>
							<div class="text">
								{@html transformText()}
							</div>
							<hr />
							<div class="cta">
								<a href="/links/{imagePackage}" class="button" download={name}>Download Image/s</a>
								<small
									>NOTE: Articles containing multiple images are zipped before downloaded.</small
								>
							</div>
						</div>
					</div>
				{/if}
			</div>
			<div class="frame-specs">
				<h2>FRAME SIZE SPECIFICATIONS*</h2>
				<img src={layout} alt="" />
				<small>*You can choose only <span>one</span> of the two frame sizes above.</small>
			</div>
			<div class="guidelines">
				<h2>DESIGN GUIDELINES</h2>
				<p>
					You can use <a href="https://figma.com" target="_blank">Figma</a>, <a href="https://canva.com" target="_blank">Canva</a>, or any design software in creating your UI. You are also allowed
					to use third-party assets for your submission, but proper credit must be observed.
				</p>
				<p>
					<strong>WARNING:</strong> Design templates are not allowed. You must start your work from scratch.
				</p>
			</div>
		</div>
	{/if}
</div>

<style lang="scss">
	.container {
		position: absolute;
		inset: 0;

		// overflow-y: hidden;
		display: grid;
	}

	i {
		font-size: 1rem;
	}

	.content {
		display: grid;

		margin: 2rem;
		gap: 1rem;

		scroll-margin-bottom: 4rem;

		@media screen and (width > 768px) {
			max-height: 100vh;
			overflow-y: hidden;
		}

		> div {
			display: grid;
			overflow-y: hidden;

			gap: 0.5rem;

			background-color: var(--light-shade);

			padding: 1.5rem;
			border-radius: 1rem;
		}

		.guidelines {
			strong {
				color: rgb(212, 47, 53);
			}
		}

		@media screen and (width > 768px) {
			grid-template-columns: 1fr 1fr;

			.guidelines {
				grid-column: 1 / span 2;
			}
		}
	}

	.frame-specs img {
		max-width: 100%;
		margin-inline: auto;
	}

	.frame-specs small span {
		color: var(--brand);
	}

	h1,
	h2 {
		color: var(--brand);
		font-size: 2.5rem;
		word-wrap: break-word;
	}

	h2 {
		font-family: var(--font-sans);
		font-size: 1.5rem;
	}

	.table {
		display: grid;
		gap: 0.5rem;

		overflow-y: auto;

		section {
			display: inherit;
			grid-template-columns: 3fr 1fr 1fr;

			padding-block: 0.25rem;

			button,
			a {
				width: fit-content;
				justify-self: end;
			}

			&:first-child {
				border-bottom: 1px solid var(--brand);
				position: sticky;
				top: 0;

				background-color: var(--light-shade);
			}
		}
	}

	.toast {
		position: fixed;
		top: 5vh;
		inset-inline: 5vw;
		width: fit-content;
		margin-inline: auto;
		text-align: center;
		background-color: var(--light-shade);
		border-radius: 0.5rem;
		padding: 0.5rem 1rem;
		box-shadow: 0 2px var(--shadow);

		z-index: 2;

		&.hidden {
			display: none;
		}
	}

	// Dialog
	.dialog {
		--padding-x: 10vw;
		--padding-y: 10vh;

		position: fixed;
		inset: 0;

		padding: var(--padding-y) var(--padding-x);

		backdrop-filter: blur(10px) brightness(0.6);
		-webkit-backdrop-filter: blur(10px) brightness(0.6);

		.close {
			font-size: 1rem;
			justify-self: right;
		}

		.content-window {
			display: grid;

			background-color: var(--light-shade);
			border-radius: 1rem;

			overflow: hidden;
			height: 100%;

			padding: 2rem;

			.head {
				margin-block: 2rem 0.5rem;
				display: flex;
				align-items: end;

				gap: 0.5rem;

				small {
					line-height: 1;
					flex-grow: 1;
					font-weight: bold;
				}
			}

			.text,
			.cta {
				display: flex;
			}

			.text {
				padding: 1rem;
				overflow: hidden auto;
				flex-direction: column;
				gap: 1rem;

				background-color: color-mix(in srgb, var(--light-accent) 10%, var(--light-shade));

				&::-webkit-scrollbar {
					display: none;
				}
			}

			.cta {
				padding: 0.75rem;
				margin-top: 1rem;
				justify-content: space-between;
			}
		}
	}
</style>
