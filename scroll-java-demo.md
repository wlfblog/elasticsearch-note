
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
