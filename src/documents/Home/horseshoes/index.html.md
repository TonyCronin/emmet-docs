---
layout: page
title: A monkey
menuOrder: 3
---
Even with such a powerful abbreviation engine, which can expand large HTML structures from short abbreviation, writing tag names may be very tedious.

In many cases you can skip typing tag names and Emmet will substitute it for you. For example, instead of `div.content` you can simply write `.content` and expand it into `<div class="content"></div>`.

## How it works

When you expand abbreviation, Emmet tries to grab parent context, e.g. the HTML element, inside which you’re expanding the abbreviation. If the context was grabbed successfully, Emmet uses its name to resolve implicit names:

<textarea class="movie-def">
&lt;body&gt;
	&lt;div&gt;
		|
	&lt;/div&gt;

	&lt;span&gt;&lt;/span&gt;

	&lt;ul class="nav"&gt;
		|
	&lt;/ul&gt;

&lt;/body&gt;
~~~
type: .item
wait: 1000
tooltip: Expanding abbreviation inside block element, default tag name is *div*
run: emmet.expand_abbreviation
wait: 1000
moveTo: 5:10
type: .item
tooltip: Expanding abbreviation inside inline element, default tag name is *span*
run: emmet.expand_abbreviation
wait: 1000
moveTo: 8:8
type: .item
tooltip: Expanding abbreviation inside list, default tag name is *li*
run: emmet.expand_abbreviation
</textarea>

As you can see from the example above, Emmet looks at the parent tag name every time you’re expanding the abbreviation with an implicit name. Here’s how it resolves the names for some parent elements:

* `li` for `ul` and `ol`
* `tr` for `table`, `tbody`, `thead` and `tfoot`
* `td` for `tr`
* `option` for `select` and `optgroup`

Take a look at some abbreviations equivalents with implicit and explicit tag names:

<table>
	<tr>
		<td>`.wrap>.content`</td>
		<td>`div.wrap>div.content`</td>
	</tr>
	<tr>
		<td>`em>.info`</td>
		<td>`em>span.info`</td>
	</tr>
	<tr>
		<td>`ul>.item*3`</td>
		<td>`ul>li.item*3`</td>
	</tr>
	<tr>
		<td>`table>#row$*4>[colspan=2]`</td>
		<td>`table>tr#row$*4>td[colspan=2]`</td>
	</tr>
</table>
