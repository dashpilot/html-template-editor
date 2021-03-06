<svelte:head>
<script type="module" src="https://unpkg.com/@deckdeckgo/inline-editor@latest/dist/deckdeckgo-inline-editor/deckdeckgo-inline-editor.esm.js"></script>
</svelte:head>

<script>
import { onMount } from 'svelte';
import { fade, fly } from 'svelte/transition';
import Image from './components/Image.svelte';

let showAdd = false;
let showSet = false;
let templates = [];

onMount(async () => {
document.body.setAttribute('spellCheck', false);
enableEditing();
loadTemplates();
});

function enableEditing() {
  document.querySelectorAll(inline_editor).forEach(function(e) {
    e.setAttribute('contenteditable', true);
  })
}

function disableEditing() {
  document.querySelectorAll(inline_editor).forEach(function(e) {
    e.removeAttribute("contenteditable")
  })
}

function loadTemplates(){
	document.querySelectorAll('template').forEach(function(e) {
	  let id = e.id;
	  let name = e.getAttribute('data-name');
	  templates.push({id: id, name: name});
	})
}

function addItem(id){
	let insert = document.getElementById(id).getAttribute('data-insert');
	let html = document.getElementById(id).innerHTML;
	document.getElementById(insert).innerHTML = html + document.getElementById(insert).innerHTML;
	enableEditing();
	showAdd = false;
}

function save(){
	disableEditing();
	let html = document.getElementById(page_id).innerHTML.replace(/\s{2,}/g, '');
	alert(html);
	enableEditing();
}
</script>

<div id="dock">
	<img src="/img/add.png" data-open="wdgt-add" class="exclude" alt="add" on:click="{() => showAdd = true}" />
	<img src="/img/save.png" id="save" class="exclude" alt="save" on:click="{save}" />
	<img src="/img/settings.png" data-open-right="wdgt-settings" class="exclude" alt="settings" on:click="{() => showSet = true}" />
</div>

{#if showAdd}
	<div class="pane pane-left" transition:fly={{x: -320}}>
		<span class="wdgt-title">Add Content Blocks</span>
		<a class="close-it" data-close="wdgt-add" id="close-add" on:click="{() => showAdd = false}">&times;</a>
		<div class="wdgt-content" id="add-content">
		{#each templates as item}
		<a class="box" on:click="{() => addItem(item.id)}">{item.name}</a>
		{/each}
		</div>
	</div>
{/if}

{#if showSet}
<div class="pane pane-right" transition:fly={{x: 320}}>
	<span class="wdgt-title">Settings</span>
	<a class="close-it" data-close-right="wdgt-settings" id="close-settings" on:click="{() => showSet = false}">&times;</a>
	<div class="wdgt-content" id="settings-content">Coming soon</div>
</div>
{/if}


<Image />
<deckgo-inline-editor containers="{inline_editor}" background-color="false" align="false" />
