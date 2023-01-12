# Website for Zimera Corporation

Tools:

1.  [Hugo](https://gohugo.io).
2.  [Hugo Serif theme](https://github.com/zerostaticthemes/hugo-serif-theme).

## Some Notes

### Checking

After pushing new contents, check [Actions](https://github.com/zimera-corp/zimera-corp.github.io/actions) to see whether something wrong has happened.

### Featured Services

By default, `services/*.md` will be checked for `featured = `. If `true` then the content of .md file will be displayed at `Home`.

### Contact at Home page

See `[params.homepage].show_contact_box` to choose whether to display Contact or not (will be the same with `data/contact.yaml`.

### Embed HTML Codes

See [layouts/shortcodes/rawhtml.html](layouts/shortcodes/rawhtml.html) on how to provide function which will enable us to embed HTML codes. Also see [content/news/_index.md](content/news/_index.md) for an example:

```
{{< rawhtml >}}
<a class="twitter-timeline" data-width="500" data-height="300" href="https://twitter.com/ZimeraCorp?ref_src=twsrc%5Etfw">Tweets by ZimeraCorp</a> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
{{< /rawhtml >}}
```
