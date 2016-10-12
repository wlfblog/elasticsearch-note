
```
public void testScroll() throws Exception {
        SearchResponse scrollResp = this.client
                .prepareSearch("index")
                .setScroll(new TimeValue(60000))
                //.setSearchType(SearchType.SCAN)
                .addSort(SortParseElement.DOC_FIELD_NAME, SortOrder.ASC)
                .setQuery(QueryBuilders.matchAllQuery())
                .get();

        while(true){
            System.out.println(scrollResp.getHits().hits().length);
            System.out.println(scrollResp.getScrollId());
            scrollResp = client.prepareSearchScroll(scrollResp.getScrollId()).setScroll(new TimeValue(60000)).get();
            if (scrollResp.getHits().hits().length == 0) {
                break;
            }
        }
    }
```

- hadoop mr inputformat rest scroll 用法 源码如下

```
private String assemble() {
        if (limit > 0) {
            if (size > limit) {
                size = limit;
            }
        }

        StringBuilder sb = new StringBuilder();
        sb.append(StringUtils.encodePath(resource.index()));
        sb.append("/");
        sb.append(StringUtils.encodePath(resource.type()));
        sb.append("/_search?");

        // override infrastructure params
        uriParams.put("search_type", "scan");
        uriParams.put("scroll", String.valueOf(time.toString()));
        uriParams.put("size", String.valueOf(size));
        if (INCLUDE_VERSION) {
            uriParams.put("version", "");
        }

        // override fields
        if (StringUtils.hasText(fields)) {
            // ES 1.0
            uriParams.put("_source", StringUtils.concatenateAndUriEncode(StringUtils.tokenize(fields), StringUtils.DEFAULT_DELIMITER));
            uriParams.remove("fields");
        }
        else {
            uriParams.remove("fields");
        }

        StringBuilder pref = new StringBuilder();
        if (StringUtils.hasText(shard)) {
            pref.append("_shards:");
            pref.append(shard);
        }
        if (StringUtils.hasText(node)) {
            if (pref.length() > 0) {
                pref.append(";");
            }
            pref.append(onlyNode ? "_only_node:" : "_prefer_node:");
            pref.append(node);
        }

        if (pref.length() > 0) {
            uriParams.put("preference", pref.toString());
        }

        // append params
        for (Iterator<Entry<String, String>> it = uriParams.entrySet().iterator(); it.hasNext();) {
            Entry<String, String> entry = it.next();
            sb.append(entry.getKey());
            if (StringUtils.hasText(entry.getValue())) {
                sb.append("=");
                sb.append(entry.getValue());
            }
            if (it.hasNext()) {
                sb.append("&");
            }
        }

        return sb.toString();
    }
```


