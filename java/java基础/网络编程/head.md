#### 获取所有头
```java
ServletRequestAttributes requestAttributes = (ServletRequestAttributes) RequestContextHolder.getRequestAttributes();
HttpServletRequest request = requestAttributes.getRequest();
Map<String, String> map = new HashMap<String, String>();
Enumeration headerNames = request.getHeaderNames();
while (headerNames.hasMoreElements()) {
    String key = (String) headerNames.nextElement();
    String value = request.getHeader(key);
    map.put(key, value);
}
```
