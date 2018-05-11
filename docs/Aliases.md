# Aliases

**e621 Has Marked this section of the API as incomplete**

General notes here

## GET Endpoints
</br>

### List

URL is `https://e621.net/tag_alias/index.json`

Parameters are:

- **page** - The page number to return
- **order** - Can be `tag`, `aliasedtag`, `reason`, `user`, `date` or `forum_post`
- **query** - Search for aliases with the given `query` in their name
- **user** - Username of the user who submitted the tag alias
- **approved** - Can be `all`, `true` or `false`
- **forum_post** - The accompanying forum post to the tag alias. Can be `all` or `false` (`true` option is the same as all)
</br>

Below is the basic response schema that you can expect to be returned:

```typescript
[
    {
    id: number,
    name: string,
    alias_id: number,
    pending: boolean
    }
    //...
]
```

[Example JSON Request](https://e621.net/tag_alias/index.json?aliased_to=digitigrade&approved=true)    [Example XML Request](https://e621.net/tag_alias/index.xml?aliased_to=digitigrade&approved=true)


</br>
</br>
## POST Endpoints
</br>

**NONE**