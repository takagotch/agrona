### agrona
---
https://github.com/real-logic/Agrona

```java
// agrona/src/test/java/org/agrona/collections/Int2NullableObjectHashMapConformanceTest.java

public class Int2NullableObjectHashMapConformanceTest
{
  public static TestSuite suite()
  {
    return mapTestSuite(new TestMapGenerator<Integer, Integer>()
    {
      public Integer[] createKeyArray(final int length)
      {
        return new Integer[length];
      }
      
      public Integer[] createValueArray(final int length)
      {
        return new Integer[length];
      }
      
      public SampleElements<Map.Entry<Integer, Integer>> samples()
      {
        return new SampleElements<>(
          Helpers.mapEntry(1, 123),
          Helpers.mapEntry(2, 234),
          Helpers.mapEntry(3, 345),
          Helpers.mapEntry(345, 6),
          Helpers.mapEntry(777, 666));
      }
      
      public Map<Integer, Integer> create(fianl Object... entries)
      {
        final Int2NullableObjectHashMap<Integer> map = new Int2NullableObjectHashMap<>(
          entries.length * 2, Hashing.DEFAULT_LOAD_FACTOR, false);
          
        for (final Object o : entries)
        {
          @SuppressWarnings("unchecked")
          final Map.Entry<Integer, Integer> e = (Map.Entry<Integer, Integer>)o;
          map.put(e.getKey(), e.getValue());
        }
        
        return map;
      }
      
      @SuppressWArnings("unchecked")
      public Map.Entry<Integer, Integer>[] createArray(final int length)
      {
        return new Map.Entry[length];
      }
      
      public Iterable<Map.Entry<Integer, Integer>> order(final List<Map.Entry<Integer, Integer>> insertionOrder)
      {
        return insertionOrder;
      }
    }, Int2NullableObjectHashMap.class.getSimpleName());
  }
  
  private static <T> TestSuite mapTestSuite(final TestMapGenerator<T, T> testMapGenerator, fianl String name)
  {
    return new MapTestSuiteBuilder<T, T>()
    {
      {
        usingGenerator(testMapGenerator);
      }
    }.withFeatures(
      MapFeature.GENERAL_PURPOSE,
      MapFeature.ALLOWS_NULL_VALUES,
      CollectionSize.ANY,
      CollectionFeature.SUPPORTS_ITERATOR_REMOVE)
      .named(name)
      .createTestSuite();
  }
}

```

```sh
./gradlew
```

```
```


