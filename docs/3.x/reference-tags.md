# Reference Tags

Reference tags can be used to create references to various elements in your site. They can be used in any textual fields, including Text cells within a Table field.

The syntax for reference tags looks like this:

```twig
{<Type>:<Identifier>:<Property>}
```

As you can see, they are made up three segments:

1.  `<Type>` – The type of element you’re creating a reference to. This can be a fully-qualified element class name (e.g. `craft\elements\Entry`) or the element type’s “reference handle”.

    Core element types have the following reference handles:

    - `entry`
    - `asset`
    - `tag`
    - `user`
    - `globalset`

2.  `<Identifier>` – Either the element’s ID or a custom identifier supported by the element type.

    Entries support the following custom identifier:

    - `sectionHandle/entry-slug`

    Identifiers can also include the site ID, UUID, or handle that the element should be loaded from, using an `@<Site>` syntax.

3.  `<Property>` _(optional)_ – The element property that the reference tag should return. If omitted, the element’s URL will be returned.

    You can refer to the element types’ class references for a list of available properties:

    - [craft\elements\Entry](craft3:craft\elements\Entry#public-properties)
    - [craft\elements\Asset](craft3:craft\elements\Asset#public-properties)
    - [craft\elements\Tag](craft3:craft\elements\Tag#public-properties)
    - [craft\elements\User](craft3:craft\elements\User#public-properties)
    - [craft\elements\GlobalSet](craft3:craft\elements\GlobalSet#public-properties)

    Custom field handles are also supported, for field types with values that can be represented as strings.

### Examples

The following are valid reference tags:

- `{asset:123:filename}` – returns the filename of an asset with the ID of `123` (via <craft3:craft\elements\Asset::getFilename()>).
- `{entry:blog/whats-on-tap}` – returns the URL of an entry in a `blog` section with the slug `whats-on-tap`.
- `{entry:blog/whats-on-tap@en:intro}` – returns the value of an `intro` custom field on a `blog` section entry with the slug `whats-on-tap`, loaded from the site with the handle `en`.
- `{craft\commerce\Variant:123:price}` – returns the price of a Commerce Variant object with the id of `123`.
- `{globalset:aGlobalSet:uid}` – returns the UID of a global set with the handle `aGlobalSet`.

## Parsing Reference Tags

You can parse any string for reference tags in your templates using the [parseRefs](dev/filters.md#parserefs) filter:

```twig
{{ entry.body|parseRefs|raw }}
```
