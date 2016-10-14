- template query java demo

```
public void createTemplate(){
        /*client.preparePutIndexedScript("mustache","first_template",
                "{\n" +
                "  \"template\":{\n" +
                "    \"query\": {\n" +
                "      \"term\": {\n" +
                "        \"event_type\": {\n" +
                "          \"value\": \"{{event_type}}\"\n" +
                "        }\n" +
                "      }\n" +
                "    }\n" +
                "  }\n" +
                "}").get();*/

        client.preparePutIndexedScript("mustache","first_template_aggs",
                "{\n" +
                        "  \"template\":{\n" +
                        "  \"size\" : 1,\n" +
                        "  \"query\": {\n" +
                        "    \"match_all\": {}\n" +
                        "  }, \n" +
                        "  \"aggs\": {\n" +
                        "    \"test\": {\n" +
                        "      \"terms\": {\n" +
                        "        \"field\": \"event_type\",\n" +
                        "        \"size\": 10\n" +
                        "      }\n" +
                        "    }\n" +
                        "  }\n" +
                        "  }\n" +
                        "}").get();
    }

    public void searchByTemplate(){
        Map<String, Object> map = new HashMap<>();
        map.put("event_type","type");
        SearchRequestBuilder searchRequestBuilder = client.prepareSearch("index")
                .setSize(1)
                .setScroll(new TimeValue(60000))
                .addSort(SortParseElement.DOC_FIELD_NAME, SortOrder.ASC)
                .setTemplate(new Template("first_template_aggs", ScriptService.ScriptType.INDEXED, "mustache", XContentType.JSON, map));
                //.setQuery(QueryBuilders.templateQuery("first_template_aggs", ScriptService.ScriptType.INDEXED, map)).setSize(0);
        SearchResponse scrollResp = searchRequestBuilder.get();
        long count = 0;
        while(true){
            //System.out.println(scrollResp.getHits().hits().length);
            //System.out.println(scrollResp.getScrollId());
            System.out.println(scrollResp);
            if(scrollResp.getHits().hits().length != 100){
            }
            scrollResp = client.prepareSearchScroll(scrollResp.getScrollId()).setScroll(new TimeValue(60000)).get();
            if (scrollResp.getHits().hits().length == 0) {
                break;
            }
        }
    }
```
