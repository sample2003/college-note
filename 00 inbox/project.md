# 数据库

## 表设计

### user



### 表数据

### user



# 后端

## 环境配置

pom.xml

```xml
<!-- 导入web起步依赖 -->
<!-- 导入mybatis起步依赖 -->
<!-- 导入mysql起步依赖 -->
<!-- 导入lombok起步依赖 -->
<!-- 导入validation起步依赖 -->
<!-- 导入jwt起步依赖 -->
<!-- 导入test起步依赖 -->

```

applicatio.yml
```yml
# 配置数据库
spring:
	application:  
		name: demo  
	datasource:  
		url: jdbc:mysql:///test?serverTimezone=UTC
		username: root  
		password: 123456  
		driver-class-name: com.mysql.cj.jdbc.Driver
```

## pojo

User
```java
@Data  
public class User {  
    private Integer id;  
    private String username;  
    private String password;
    ...
}
```

Result
```java
@AllArgsConstructor  
@NoArgsConstructor  
@Data  
public class Result<T> {  
    private Integer code;  
    private String message;  
    private T data;  
  
    public static <E> Result<E> success(E data) {  
        return new Result<>(1, "操作成功", data);  
    }  
    public static Result success() {  
        return new Result<>(1, "操作成功", null);  
    }  
    public static Result error(String message) {  
        return new Result<>(0, message, null);  
    }  
}
```

## controller

UserController
```java
@RestController  
@RequestMapping("/user")  
public class UserController {  
    @Autowired  
    private UserService userService;  
  
    @RequestMapping("/register")  
    public Result register(@Pattern(regexp="^\\S{5,16}$") String username, @Pattern(regexp="^\\S{5,16}$") String password){  
        // 查询用户  
        User u = userService.findByUserName(username);  
        if(u==null){  
            // 创建用户, 注册  
            userService.register(username, password);  
            return Result.success();  
        }else{  
            return Result.error("用户名已存在");  
        }  
    }  
}
```
## service

UserService
```java
public interface UserService {  
    // 根据用户名查询用户  
    User findByUserName(String username);  
    // 注册用户  
    void register(String username, String password);  
}
```

impl.UserServiceImpl
```java
@Service  
public class UserServiceImpl implements UserService {  
    @Autowired  
    private UserMapper userMapper;  
    @Override  
    public User findByUserName(String username) {  
        User u = userMapper.findByUserName(username);  
        return u;  
    }  
    @Override  
    public void register(String username, String password) { 
        // 加密  
        //添加  
        userMapper.add(username,password);  
    }  
}
```

## mapper

UserMapper
```java
@Mapper  
public interface UserMapper {  
    @Select("select * from ...")  
    User findByUserName(String username);  
  
    @Insert("insert into ...")  
    void add(String username, String password);  
}
```

## utils

## exception

GlobalExceptionHandler
```java
@RestControllerAdvice  
public class GlobalExceptionHandler {  
  
    @ExceptionHandler(Exception.class)  
    public Result handleException(Exception e){  
        e.printStackTrace();  
        return Result.error(StringUtils.hasLength(e.getMessage()) ? e.getMessage() : "操作失败");  
    }  
}
```

# 前端

# 其它