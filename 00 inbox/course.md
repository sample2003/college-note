# 一、设计模式

## 1. tomcat中的观察者模式

lifecycle ：抽象主题角色

lifecycleBase ：具体主题

```java
// lifecycleBase
// tomcat执行初始化方法init()

// setStateInternal(); // 设置当前状态为initializing,并通知observer执行相应操作

// initInternal(); // 内部初始化

// setStateInternal(); // 设置当前状态为initialized,并通知observer执行相应操作

@Override
public final synchronized void init() throws LifecycleException {
        if (!state.equals(LifecycleState.NEW)) {
            invalidTransition(BEFORE_INIT_EVENT);
        }
        try {
            setStateInternal(LifecycleState.INITIALIZING, null, false);
            initInternal();
            setStateInternal(LifecycleState.INITIALIZED, null, false);
        } catch (Throwable t) {
            handleSubClassException(t, "lifecycleBase.initFail", toString());
        }
    }
```

```java
// lifecycleBase

// 并不是在observer端进行操作，而是根据observer提供的接口lifecycleEvent(lifecycleEvent event)来操作

private synchronized void setStateInternal(LifecycleState state, Object data, boolean check)
        if (check) {
        ...
	        this.state = state;
	        String lifecycleEvent = state.getLifecycleEvent();
	        if (lifecycleEvent != null) {
	            fireLifecycleEvent(lifecycleEvent, data);
	        }
    }
```

```java
// lifecycleBase

// 观察者方法fireLifecycleEvent，该方法会被setStateInternal()方法调用

protected void fireLifecycleEvent(String type, Object data) {
        LifecycleEvent event = new LifecycleEvent(this, type, data);
        for (LifecycleListener listener : lifecycleListeners) {
            listener.lifecycleEvent(event);
        }
    }
```
lifecycleListener ：抽象观察者

UserConfig ：具体观察者

```java
// userconfig

// setStateInternal()的调用使得lifecycleEvent被执行，达到消息传递的目的

@Override
    public void lifecycleEvent(LifecycleEvent event) {
        // Identify the host we are associated with
        try {
            host = (Host) event.getLifecycle();
        } catch (ClassCastException e) {
            log.error(sm.getString("hostConfig.cce", event.getLifecycle()), e);
            return;
        }
        // Process the event that has occurred
        if (event.getType().equals(Lifecycle.START_EVENT)) {
            start();
        } else if (event.getType().equals(Lifecycle.STOP_EVENT)) {
            stop();
        }
}
```

## 2. Spring中的

1. 控制反转（IoC）：Spring框架通过控制反转（IoC）机制来管理对象之间的依赖关系。在这里，JianzhiyingpinController类通过@Autowired注解来自动注入JianzhiyingpinService接口的实现类，从而避免了手动创建对象和管理对象之间的依赖关系。
    
2. 面向切面编程（AOP）：Spring框架通过面向切面编程（AOP）机制来实现横切关注点的模块化。在这里，可以使用AOP机制来实现日志记录、性能监控等横切关注点。
    
3. MVC模式：Spring框架通过MVC模式来实现Web应用程序的分层架构。在这里，JianzhiyingpinController类充当了控制器层，它接收HTTP请求并调用相应的服务层方法来处理请求。
    
4. 依赖注入（DI）：Spring框架通过依赖注入（DI）机制来管理对象之间的依赖关系。在这里，JianzhiyingpinController类通过构造函数注入HttpServletRequest对象


这些Spring的类中运用了以下设计模式：
import org.springframework.web.bind.annotation.PathVariable;  
import org.springframework.web.bind.annotation.RequestBody;  
import org.springframework.web.bind.annotation.RequestMapping;  
import org.springframework.web.bind.annotation.RequestParam;  
import org.springframework.web.bind.annotation.RestController;

1. 前端控制器模式（Front Controller Pattern）：Spring框架中的@RestController注解和@RequestMapping注解，可以将JianzhiyingpinController类看作是一个前端控制器，它负责处理所有来自客户端的请求，并将请求分发给相应的处理程序。
    
2. 适配器模式（Adapter Pattern）：Spring框架中的@RequestParam注解和@RequestBody注解，可以将HTTP请求参数适配为Java方法参数，从而使得Java方法能够更方便地处理HTTP请求。
    
3. 策略模式（Strategy Pattern）：Spring框架中的@RequestMapping注解，可以将HTTP请求映射到不同的处理程序，这些处理程序可以根据请求的URL、HTTP方法、请求参数等信息来选择不同的策略来处理请求。
    
4. 工厂模式（Factory Pattern）：Spring框架中的@RestController注解和@RequestMapping注解，都是通过工厂模式来创建和管理对象的，这些对象包括控制器、处理程序、拦截器等。
    

总之，Spring框架中运用了多种设计模式来实现其核心功能，这些设计模式使得Spring框架具有高度的灵活性、可扩展性和可维护性。

# 二、软件工程


