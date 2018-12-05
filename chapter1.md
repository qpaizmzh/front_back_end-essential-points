# 关于前后端的CROS跨域请求的实现

1、前端发送ajax请求的时候按照正常的设置进行访问

2、后端的代码主要是设置几个http协议头的属性：

```
package com.sq.filter;
 
import org.springframework.stereotype.Component;
 
import javax.servlet.*;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
 
 
@Component
public class AccessFilter extends HttpServlet implements Filter {
 
    private static final long serialVersionUID = 1L;
 
 
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
 
    }
 
    //设置http协议头的方法，一般在filter进行
    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
 
        HttpServletResponse httpResponse = (HttpServletResponse) response;
        httpResponse.setHeader("Access-Control-Allow-Origin", "*");
        httpResponse.setHeader("Access-Control-Allow-Methods", "GET, POST, PUT, DELETE");
        httpResponse.setHeader("Access-Control-Max-Age", "1800");
        httpResponse.setHeader("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
        httpResponse.setHeader("Access-Control-Allow-Credentials", "true");
        chain.doFilter(request, httpResponse);
    }
}


```



