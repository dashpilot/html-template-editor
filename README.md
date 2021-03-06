# html-template-editor
Make any HTML template editable!

Simple on-page editor that features inline-editing, image upload and resize, adding/sorting/removing template blocks. Easy to integrate into any HTML template and independant of CSS frameworks (Can be used with Bootstrap/Tailwind/Uikit/Bulma/Custom CSS/etc).

## Demo
https://html-template-editor.vercel.app/

## How to

Integrate the editor with any existing HTML template by adding the following to the head of each page:

```
<script>
  const inline_editor = 'h1,h2,h3,h4,h5,p'; // which element should be inline-editable
  const img_width = 800; // resize images to this width
  const page_id = 'page'; // id of the div that contains the page's contents, see below
</script>

<link rel='stylesheet' href='/global.css'>
<script defer src='/build/bundle.js'></script>
```

Wrap the part of the page that you want to save in a div with an id of `page`:

```
<div id="page">
  <!-- This part will be saved -->
</div>
```

That's all! No further changes required!

## Creating content blocks that users can add to the page

To create your own content blocks, just wrap your custom HTML in a 'template'-tag, add a unique id and the following data-attributes:

`data-name`: The name of the content block as it should appear in the interface
`data-insert`: the wrapper element the content block should be inserted into

```
<template id="post" data-name="Post" data-insert="main">

    <!-- Your custom content-block -->
		<section class="layout-post">
			<div id="item-4" class="container editable">
				<h2>Mauris eleifend ligula</h2>
				Vivamus in nisi commodo, auctor magna vel, viverra turpis.
			</div>
		</section>
    
</template>
```

Check out the example on: https://html-template-editor.vercel.app/ to see how it all works together
