---
title: GroupByLastmod
description: Returns the given page collection grouped by last modification date in descending order.
categories: []
keywords: []
params:
  functions_and_methods:
    returnType: page.PagesGroup
    signatures: ['PAGES.GroupByLastmod LAYOUT [SORT]']
---

When grouping by last modification date, the value is determined by your [site configuration], defaulting to the `lastmod` field in front matter.

The [layout string] has the same format as the layout string for the [`time.Format`] function. The resulting group key is [localized](g) for language and region.

[`time.Format`]: /functions/time/format/
[layout string]: #layout-string
[site configuration]: /configuration/front-matter/#dates

{{% include "/_common/methods/pages/group-sort-order.md" %}}

To group content by year and month:

```go-html-template
{{ range .Pages.GroupByLastmod "January 2006" }}
  <p>{{ .Key }}</p>
  <ul>
    {{ range .Pages }}
      <li><a href="{{ .RelPermalink }}">{{ .LinkTitle }}</a></li>
    {{ end }}
  </ul>
{{ end }}
```

To sort the groups in ascending order:

```go-html-template
{{ range .Pages.GroupByLastmod "January 2006" "asc" }}
  <p>{{ .Key }}</p>
  <ul>
    {{ range .Pages }}
      <li><a href="{{ .RelPermalink }}">{{ .LinkTitle }}</a></li>
    {{ end }}
  </ul>
{{ end }}
```

The pages within each group will also be sorted by last modification date, either ascending or descending depending on your grouping option. To sort the pages within each group, use one of the sorting methods. For example, to sort the pages within each group by title:

```go-html-template
{{ range .Pages.GroupByLastmod "January 2006" }}
  <p>{{ .Key }}</p>
  <ul>
    {{ range .Pages.ByTitle }}
      <li><a href="{{ .RelPermalink }}">{{ .Title }}</a></li>
    {{ end }}
  </ul>
{{ end }}
```

## Layout string

{{% include "/_common/time-layout-string.md" %}}
