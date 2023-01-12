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

