# UI 組件-Link

組件 Link 為超鏈接。指向一個外部資源。 Link 實際為一HTML 鏈接。和 Button 不同的是,Link 不會在伺服器端觸發一個事件。你也可以使用 setIcon 為 Link 添加一個圖標：

```
// Textual link
Link link = new Link("Click Me!",
        new ExternalResource("http://vaadin.com/"));
	...
// Image link
Link iconic = new Link(null,
        new ExternalResource("http://vaadin.com/"));
iconic.setIcon(new ThemeResource("img/nicubunu_Chain.png"));

// Image + caption
Link combo = new Link("To appease both literal and visual",
        new ExternalResource("http://vaadin.com/"));
combo.setIcon(new ThemeResource("img/nicubunu_Chain.png"));
```

上面代碼顯示結果如下：

![](images/25.png)

打開超鏈接時可以支持超鏈接打開的目標模式(Target)，可以通過 setTargetName 來指定，比如 _blank 在新窗口中顯示超鏈接。 此外，可以通過 setTargetWidth, setTargetHeight, setTargetBorder 指定顯示窗口的大小和邊框。如下面代碼：

```
// Open the URL in a popup
link.setTargetName("_blank");
link.setTargetBorder(Link.TARGET_BORDER_NONE);
link.setTargetHeight(300);
link.setTargetWidth(400);
```

除 Link 組件之外，Vaadin 也可以通過 Button （使用 Reindeer.BUTTON_LINK 風格）來定義一個超鏈接，也可以使用 XHTML 模式使用 Label 來顯示一個超鏈接。

Tags: [Java EE](http://www.imobilebbs.com/wordpress/archives/tag/java-ee), [Vaadin](http://www.imobilebbs.com/wordpress/archives/tag/vaadin), [Web](http://www.imobilebbs.com/wordpress/archives/tag/web)