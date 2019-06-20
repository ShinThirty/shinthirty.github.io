---
layout: post
title:  "PowerMock Tips and Tricks 1"
date:   2019-06-19
categories: [note]
tags:   [unittest, powermock]
---
When I tried to fix some unit tests due to the recent API invocation changes, I realized that the mocking statements have to be in the **SAME** test method to make the mocking in effect, as follows:

```java
@Test
public void executeQueryTest() throws Exception {
    FUDHandler mockFudHandler = PowerMockito.mock(FUDHandler.class);
    PowerMockito.whenNew(FUDHandler.class).withAnyArguments().thenReturn(mockFudHandler);
    PowerMockito.when(mockFudHandler.executeQuery(Matchers.anyString())).thenReturn(mockListOfResults);

    Map<String, List<String>> mapOfResults = databaseUtilities.executeQuery(QUERY);
    Assert.assertEquals(1, mapOfResults.size());
}
```

If the first 3 lines were in another method, the mocking won't be in effect and the original constructor and ```executeQuery``` method will be invoked by the test.
