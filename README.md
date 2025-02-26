# Website for Zimera Corporation

Tools:

1.  [Hugo](https://gohugo.io).
2.  [Hugo Serif theme](https://github.com/zerostaticthemes/hugo-serif-theme).

## Modify Contents

1.  Modify contents using `hugo new`, for example: `hugo new posts/10.md`. 
2.  Test: `hugo serve`.
3.  Deploy: `hugo`, then push to Github. See **Checking** below.

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
Since raw HTML is considerd unsage, Hugo should be configured to read and embed HTML codes together with markdown using this configuration in [config.toml fle](config.toml):

```
[markup]
  defaultMarkdownHandler = 'goldmark'
  [markup.goldmark.renderer]
    unsafe = true
```

### Pagination and Read more ...

See [layouts/_default/list.html](layouts/_default/list.html) for definition. The template at `layouts/_default/list.html` is used by default for pagination. Configuration can be seen at [config.toml](config.toml) - see `paginate = ...`. There's no need to setup pagination at `posts` for example, since it will automatically calls `list.html` template if more than `paginate = ...` files exist.

### Summary -> Number of Words Truncated

See [layouts/_default/summary.html](layouts/_default/summary.html), it uses `truncate` function.

### Tags and Categories

1. Activate tags and categories inside `config.toml`:

```toml
[taxonomies]
    category = "categories"
    tag = "tags"
```

2. Prepare template. We just want to pust tags and categories in `/posts/`, so prepare these layouts:

`layout/_default/taxonomy.html`

```
{{ define "main" }}
  <div class="container">
    <h1>All {{ .Type }}</h1>
    <ul>
      {{ range .Data.Pages }}
        <li>
          <a href="{{ .Permalink }}">{{ .Title }}</a>
        </li>
      {{ end }}
    </ul>
  </div>
{{ end }}
```

`layout/_default/term.html`

```
{{ define "main" }}
  <div class="container">
    <h1>All posts for {{ .Type | singularize }} "{{ .Title }}"</h1>
    <ul>
      {{ range .Data.Pages }}
        <li>
          <a href="{{ .Permalink }}">{{ .Title }}</a>
        </li>
      {{ end }}
    </ul>
  </div>
{{ end}}
```

`layout/posts/summary.html`

```
<div class="summary">
    <h2>
      <a href="{{ .RelPermalink }}">{{ .Title }}</a>
    </h2>

    <p>Posted in: 
    {{ with .Params.categories }}
        {{range .}}
        <a href="/categories/{{ . | urlize }}">{{ . }}</a>&nbsp;&nbsp;
        {{end}}
    {{ end }}
    <br />
    Tags: 
    {{ with .Params.tags }}
        {{range .}}
        <a href="/tags/{{ . | urlize }}">{{ . }}</a>&nbsp;&nbsp;
        {{end}}
    {{ end }}
    <br />
    Author: {{ range .Param "authors" }}
          {{ . }}
	      {{ end }} | <time>{{ .PublishDate.Format "January 2, 2006" }}</time> | 
        {{ .ReadingTime }} {{ if eq .ReadingTime 1 }} minute {{ else }} minutes reading time{{ end }}
       </p>

    {{ .Content | truncate 200 "…" }}
</div>
```

We may also adjust `layout/posts/single.html` (the template which will be used to display the whole post) just like the above. Here's an example:

```
{{ define "body_classes" }}page-default-single{{ end }}

{{ define "main" }}
<div class="container pb-6 pt-6 pt-md-10 pb-md-10">
  <div class="row justify-content-start">
    <div class="col-12 col-md-8">
      <h1 class="title">{{.Title}}</h1>

    <p>Posted in: 
    {{ with .Params.categories }}
        {{range .}}
        <a href="/categories/{{ . | urlize }}">{{ . }}</a>&nbsp;&nbsp;
        {{end}}
    {{ end }}
    <br />
    Tags: 
    {{ with .Params.tags }}
        {{range .}}
        <a href="/tags/{{ . | urlize }}">{{ . }}</a>&nbsp;&nbsp;
        {{end}}
    {{ end }}
    <br />
    Author: {{ range .Param "authors" }}
          {{ . }}
	      {{ end }} | <time>{{ .PublishDate.Format "January 2, 2006" }}</time> | 
        {{ .ReadingTime }} {{ if eq .ReadingTime 1 }} minute {{ else }} minutes reading time{{ end }}
       </p>

      <div class="content">{{.Content}}</div>
    </div>
  </div>
</div>
{{ end }}
```

