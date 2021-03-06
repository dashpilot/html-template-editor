# html-template-editor
Make any HTML template editable!

Simple on-page editor that features inline-editing, image upload and resize, adding/sorting/removing template blocks. Easy to integrate into any HTML template and independant of CSS frameworks (Can be used with Bootstrap/Tailwind/Uikit/Bulma/Custom CSS/etc).

## Howto

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
