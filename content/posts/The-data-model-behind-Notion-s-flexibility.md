---
                title: The-data-model-behind-Notion-s-flexibility
                date: 2021-01-01    
                draft: true
                tags: []
               ---


            # The-data-model-behind-Notion-s-flexibility

Notion supports many types of blocks, most of which you can see in the “new block” menu that appears when you press the `+` button or in the `/` menu:
In addition to the attributes that describe the block itself, every block has attributes that define their relationship with other blocks:
- **Content** — an array (or ordered set) of block IDs representing the content inside this block, like nested bullet items in a bulleted list or the text inside a toggle.The block type is what specifies how the block is rendered in Notion’s UI — and depending on that type, we interpret the block’s properties and content differently.The “checked” property of the `To-do list` block is ignored when the block is transformed into `Heading` and `Callout` block types — but by the time we come full circle to turn the block back into a `To-do list` block, it is still checked.In the to-do list example, we have a `To-do list` block (“Write a blog post about blocks”) with three block IDs in its content array.We think of these IDs as “downward pointers,” and call the blocks that they refer to “content” or “render children.”
Each block defines the position and order in which its content blocks are rendered.For example, pressing indent in a content block tries to add that block to the content of the nearest sibling block in the content tree.The API method for loading the data for a page is called `loadPageChunk` — it descends from a starting point (likely the block ID of a page block) down the content tree, and returns the blocks in the content tree plus any dependent records needed to properly render those blocks.