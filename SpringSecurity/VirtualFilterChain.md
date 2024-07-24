### VirtualFilterChain

## 1. ApplicationFilterChain

> Spring的过滤器链

```java
ApplicationFilterConfig filterConfig = this.filters[this.pos++];
// 获取filter,springSecurityFilterChain在其中
Filter filter = filterConfig.getFilter();
// 进入DelegatingFilterProxy
filter.doFilter(request, response, this);
```

## 2. DelegatingFilterProxy

```java
//delegate=WebMvcSecurityConfiguration$CompositeFilterChainProxy@9640
//Let the delegate perform the actual doFilter operation
private volatile Filter delegate;

//filterChain是ApplicationFilterChain
delegate.doFilter(request, response, filterChain);
```

### 2.1 CompositeFilterChainProxy

```java
//CompositeFilter		
private final Filter doFilterDelegate;

//???
private final FilterChainProxy springSecurityFilterChain;

//doFilterDelegate=CompositeFilter
this.doFilterDelegate.doFilter(request, response, chain);
```

#### 2.1.1 CompositeFilter

```java
// HandlerMappingIntrospector$lambda@9742
// DebugFilter@9614
// SpringSecurityConfig启动时，初始化以上两个过滤器
private List<? extends Filter> filters = new ArrayList<>();

//chain=Spring过滤器链,构建真实过滤器链
new VirtualFilterChain(chain, this.filters).doFilter(request, response);

```

##### 2.1.1.1 VirtualFilterChain

> additionalFilters执行完毕，跳转上级过滤器链

```java
//原生过滤器链=Spring过滤器链
private final FilterChain originalChain;
//真实执行过滤器
private final List<? extends Filter> additionalFilters;

@Override
public void doFilter(final ServletRequest request, final ServletResponse response)
    throws IOException, ServletException {
	//执行完毕后，回归Spring过滤器链中
  if (this.currentPosition == this.additionalFilters.size()) {
    this.originalChain.doFilter(request, response);
  }
  else {
    this.currentPosition++;
    Filter nextFilter = this.additionalFilters.get(this.currentPosition - 1);
    //VirtualFilterChain过滤器链传递，继续执行doFilter。
    nextFilter.doFilter(request, response, this);
  }
}
```



## DebugFilter

> VirtualFilterChain中additionalFilters的过滤器

```java
//??
private final FilterChainProxy filterChainProxy;

//filterChain=VirtualFilterChain
this.filterChainProxy.doFilter(request, response, filterChain);
```

### FilterChainProxy

```java
//SecurityConfig配置的SecurityFilterChain
private List<SecurityFilterChain> filterChains;

//构造VirtualFilterChain,保证执行完filterChains，继续回CompositeFilter$VirtualFilterChain@10230
private FilterChainDecorator filterChainDecorator = new VirtualFilterChainDecorator();


this.filterChainDecorator.decorate(reset, filters).doFilter(firewallRequest, firewallResponse);
```



