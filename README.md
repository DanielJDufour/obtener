# obtener
Safely and Easily Access Nested Object Property Values

# why obtener
```js
"obtener" is Spanish for "to obtain".
```

# install
```html
<script src="https://unpkg.com/obtener"></script>
```
or
```js
import { get } from "obtener";
```

# basic usage
```html
data = {
  "agency": "GSA",
  "measurementType": {
    "method": "modules"
  },
  "version": "2.0.0",
  "releases": [
    {
      "name": "usasearch",
      "description": "System now maintained in open repo https://github.com/GSA/search-gov.",
      "permissions": {
        "licenses": null,
        "usageType": "governmentWideReuse"
      },
      "tags": [
        "GSA"
      ],
      "repositoryURL": "https://github.com/GSA/usasearch",
      "homepageURL": "https://search.gov",
      "contact": {
        "email": "gsa-github.support@gsa.gov"
      },
      "laborHours": 0,
      "vcs": "git",
      "organization": "GSA"
    },
    // ...
  }
}
```

```js
get(data, 'agency');
["GSA"]

// get nested properties using dot syntax
get(data, 'releases.permissions.licenses.name');
["CC0 1.0 Universal", "PD", "agpl-3.0", ... ]

// get nested properties using double underscore syntax
get(data, 'releases__permissions__licenses__name');
["CC0 1.0 Universal", "PD", "agpl-3.0", ... ]
```

# advanced usage
## unique
If you only want unique results returned:
```js
// default
get(data, 'releases.tags');
["GSA", "GSA", "GSA", ...]

// uniques only
get(data, 'releases.tags', { unique: true });
["GSA","gsa","socialmedia", "mobileapps", ...]
```

## sort
If you want your results sorted
```js
get(data, 'releases.tags', { sort: true });
["508", "API", "Bing", "DigitalGovSearch", ...]
```

## seperator
By default, obtener tries syntax where the steps are separted by 
`"."` or `"__"`.  If you'd like to restrict the syntax or use a custom separator:
```js
get(data, 'releases--tags', { sep: '--' });

// accepts releases--tags and releases__tags
get(data, 'releases--tags', { sep: ['--', '__'] });
```