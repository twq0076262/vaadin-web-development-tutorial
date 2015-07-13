# 使用 Item 介面管理一組 Property

Item 介面用來管理一組命名的 Property 對象。每個 Property 由一個標識符（PID）來定義，Item通過 PID 使用方法 getItemProperty()來讀寫其中的 Property。
使用 Item 的地方例如 Table 的一行，每個屬性（Property）對應行的每個欄位（列column)。或者是 Tree 的一個節點，以及綁定到表單 From 的數據，此時 Item 中的每個屬性對應的表單中的一個輸入域(Field)。
使用在面向對象概念來說,Item 對應到一個對象，但 Item 可以支持配置及通過事件處理機制（主要是數據變化事件）。
使用 Item 的最簡單的方法是使用 Vaadin 的一些內置實現，比如 PropertysetItem 或 BeanItem。此外 Form 也實現了 Item 介面因此可當作 Item 對象來使用。Form 可以通過 Item 自動創建其中的 UI 組件，可以參見件 [Vaadin Web 應用開發教程(23):UI 組件-Form 組](http://www.imobilebbs.com/wordpress/?m=20120811)。
Item 介面定義了一些介面來管理其中的 Propert y或監聽 Property 值變化事件。

## 使用 PropertysetItem
PropertysetItem 是實現了 Item 介面的通用實現，可以用來存放屬性值。屬性通過addItemProperty 添加到集合中。

```
PropertysetItem item = new PropertysetItem();
item.addItemProperty("name", new ObjectProperty("Zaphod"));
item.addItemProperty("age", new ObjectProperty(42));
        
// Bind it to a component
Form form = new Form();
form.setItemDataSource(item);
```

## 使用 BeanItem 
BeanItem 也實現了 Item 介面可以用來包容一個 JavaBean 對象。實際上只使用 Java Bean 規範中的 setter 和 getter 而未使用其它 JavaBean 功能，因此 BeanItem 也可以用在一般的 Java 對象（POJO)上。

```
// Here is a bean (or more exactly a POJO)
class Person {
    String name;
    int    age;
    
    public String getName() {
        return name;
    }
    
    public void setName(String name) {
        this.name = name;
    }
    
    public Integer getAge() {
        return age;
    }
    
    public void setAge(Integer age) {
        this.age = age.intValue();
    }
}

// Create an instance of the bean
Person bean = new Person();
        
// Wrap it in a BeanItem
BeanItem<Person> item = new BeanItem<Person>(bean);
        
// Bind it to a component
Form form = new Form();
form.setItemDataSource(item);
```

## 嵌套使用 Bean
在使用聚合類，某個類包含其它某個類，比如下面的 Planet 類定義了一個發現人 Discovery（為Person 類）

```
// Here is a bean with two nested beans
public class Planet implements Serializable {
    String name;
    Person discoverer;
    
    public Planet(String name, Person discoverer) {
        this.name = name;
        this.discoverer = discoverer;
    }

    ... getters and setters ...
}

...
// Create an instance of the bean
Planet planet = new Planet("Uranus",
                    new Person("William Herschel", 1738));
```

當需要在 Form 顯示時，你可以希望在顯示 Planet 屬性的同時顯示 Disoveryer 的一些屬性，可以通過 MethodProperty 或 NestedMethodProperty 單獨綁定這些屬性，通常此時需要隱藏嵌套類本身被綁定到屬性，可以在構造函數中只列出需要綁定的屬性，比如只綁定 Planet 的 Name 屬性。

```
// Wrap it in a BeanItem and hide the nested bean property
BeanItem<Planet> item = new BeanItem<Planet>(planet,
        new String[]{"name"});
    
// Bind the nested properties.
// Use NestedMethodProperty to bind using dot notation.
item.addItemProperty("discoverername",
    new NestedMethodProperty(planet, "discoverer.name"));
    
// The other way is to use regular MethodProperty.
item.addItemProperty("discovererborn",
     new MethodProperty<Person>(planet.getDiscoverer(),
                                "born"));
```

NestedMethodProperty 和 MethodProperty 不同點在於 NestedMethodProperty 只在需要訪問屬性值時才訪問嵌套類，而 MethodProperty 則是在創建這個 Method Property 就訪問嵌套類（如Person)。

下面代碼將 Item 綁定到一個 Form

```
// Bind it to a component
Form form = new Form();
form.setItemDataSource(item);
    
// Nicer captions
form.getField("discoverername").setCaption("Discoverer");
form.getField("discovererborn").setCaption("Born");
```

![](images/103.png)

Tags: [Java EE](http://www.imobilebbs.com/wordpress/archives/tag/java-ee), [Vaadin](http://www.imobilebbs.com/wordpress/archives/tag/vaadin), [Web](http://www.imobilebbs.com/wordpress/archives/tag/web)
