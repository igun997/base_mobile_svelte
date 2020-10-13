<script>
	import {onMount} from "svelte";

	export let name = ""
	import TopAppBar, {Row, Section, Title, FixedAdjust, DenseFixedAdjust, ProminentFixedAdjust, ShortFixedAdjust} from '@smui/top-app-bar';
	import Drawer, {AppContent, Content, Header, Subtitle, Scrim} from '@smui/drawer';
	import List, {Item, Text, Graphic, Separator, Subheader} from '@smui/list';
	import H6 from '@smui/common/H6.svelte';
	import IconButton from '@smui/icon-button';
	import Landing from "./pages/Landing.svelte"
	let dense = false;
	let prominent = false;
	let Adjust = FixedAdjust;
	let title = "SMK"
	let fromChild;
	let myDrawer2;
	let menuOpen = false;
	let active_menu = 'Inbox';
	let variant = 'fixed';
	Adjust = ShortFixedAdjust;
	function setActive2(value) {
		active_menu = value
		menuOpen = false;
	}
	const bindData = async (n) => {
		fromChild = n;
		console.log(fromChild)
	};
	onMount(()=>{
		title = fromChild.title;
	});
</script>

<style>

</style>
<svelte:head>
	<title>{name}</title>
	<link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">
	<link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Roboto:300,400,500,600,700">
	<link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Roboto+Mono">
</svelte:head>
<Drawer variant="dismissible"  bind:this={myDrawer2} bind:open={menuOpen}>
	<Header>
		<IconButton on:click={() => menuOpen = !menuOpen} class="material-icons">menu</IconButton>
	</Header>
	<Content>
		<List>
			<Item href="javascript:void(0)" on:click={() => setActive2('Inbox')} >
				<Graphic class="material-icons" aria-hidden="true">inbox</Graphic>
				<Text>Inbox</Text>
			</Item>
			<Item href="javascript:void(0)" on:click={() => setActive2('Star')} activated={active_menu === 'Star'}>
				<Graphic class="material-icons" aria-hidden="true">star</Graphic>
				<Text>Star</Text>
			</Item>
			<Item href="javascript:void(0)" on:click={() => setActive2('Sent Mail')} activated={active_menu === 'Sent Mail'}>
				<Graphic class="material-icons" aria-hidden="true">send</Graphic>
				<Text>Sent Mail</Text>
			</Item>
			<Item href="javascript:void(0)" on:click={() => setActive2('Drafts')} activated={active_menu === 'Drafts'}>
				<Graphic class="material-icons" aria-hidden="true">drafts</Graphic>
				<Text>Drafts</Text>
			</Item>

			<Separator nav />
			<Subheader component={H6}>Labels</Subheader>
			<Item href="javascript:void(0)" on:click={() => setActive2('Family')} activated={active_menu === 'Family'}>
				<Graphic class="material-icons" aria-hidden="true">bookmark</Graphic>
				<Text>Family</Text>
			</Item>
			<Item href="javascript:void(0)" on:click={() => setActive2('Friends')} activated={active_menu === 'Friends'}>
				<Graphic class="material-icons" aria-hidden="true">bookmark</Graphic>
				<Text>Friends</Text>
			</Item>
			<Item href="javascript:void(0)" on:click={() => setActive2('Work')} activated={active_menu === 'Work'}>
				<Graphic class="material-icons" aria-hidden="true">bookmark</Graphic>
				<Text>Work</Text>
			</Item>
		</List>
	</Content>
</Drawer>
<div class="top-app-bar-container flexor">
	<TopAppBar {variant} {prominent} {dense} color='primary'>
		<Row>
			<Section>
				<IconButton on:click={() => menuOpen = !menuOpen} class="material-icons">menu</IconButton>
				<Title>{title}</Title>
			</Section>
			<Section align="end" toolbar>
				<IconButton class="material-icons" aria-label="Download">file_download</IconButton>
				<IconButton class="material-icons" aria-label="Print this page">print</IconButton>
				<IconButton class="material-icons" aria-label="Bookmark this page">bookmark</IconButton>
			</Section>
		</Row>
	</TopAppBar>
	<div use:Adjust>
		<Landing bindData={bindData} />
	</div>
</div>
