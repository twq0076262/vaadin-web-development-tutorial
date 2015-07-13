# UI组件-ProgressIndicator组件

ProgressIndicator 组件显示进程条，ProgressIndicator 组件定时向服务器查询其当前值，如果值有变化，则更新进程条进度。Web 应用本身无需实现任何查询服务器的操作，查询由ProgressIndicator 组件自动完成。
ProgressIndicator 组件的值域为0.0到1.0之间。缺省的查询(polling)间隔为1秒，可以使用setPollingInterval 修改。

```
// Create the indicator
final ProgressIndicator indicator =
        new ProgressIndicator(new Float(0.0));
main.addComponent(indicator);
 
// Set polling frequency to 0.5 seconds.
indicator.setPollingInterval(500);
```

![](images/65.png)

ProgressIndicator 组件通常用来显示一些耗时操作（比如下载文件）的进度。 使用 setValue 为ProgressIndicator 组件设置当前值。
下面代码模拟一个费时操作提供 ProgressIndicator 组件显示进度。

```
// Create an indicator that makes you look busy
final ProgressIndicator indicator =
        new ProgressIndicator(new Float(0.0));
main.addComponent(indicator);

// Set polling frequency to 0.5 seconds.
indicator.setPollingInterval(500);

// Add a button to start working
final Button button = new Button("Click to start");
main.addComponent(button);

// Another thread to do some work
class WorkThread extends Thread {
    public void run () {
        double current = 0.0;
        while (true) {
            // Do some "heavy work"
            try {
                sleep(50); // Sleep for 50 milliseconds
            } catch (InterruptedException e) {}
            
            // Show that you have made some progress:
            // grow the progress value until it reaches 1.0.
            current += 0.01;
            if (current>1.0)
                indicator.setValue(new Float(1.0));
            else 
                indicator.setValue(new Float(current));
            
            // After all the "work" has been done for a while,
            // take a break.
            if (current > 1.2) {
                // Restore the state to initial.
                indicator.setValue(new Float(0.0));
                button.setVisible(true);
                break;
            }
        }
    }
}

// Clicking the button creates and runs a work thread
button.addListener(new Button.ClickListener() {
    public void buttonClick(ClickEvent event) {
        final WorkThread thread = new WorkThread();
        thread.start();
        
        // The button hides until the work is done.
        button.setVisible(false);
    }
});
```

![](images/66.png)

Tags: [Java EE](http://www.imobilebbs.com/wordpress/archives/tag/java-ee), [Vaadin](http://www.imobilebbs.com/wordpress/archives/tag/vaadin), [Web](http://www.imobilebbs.com/wordpress/archives/tag/web)