﻿# Pang.AutoMapperMiddleware

可以非常简洁的使用Automapper

## 用法

### 1. 引入

1. 按照正常方式在`service`中注入AutoMapper

2. 按照下方方式引入中间件

```csharp
public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    //引入中间件
    app.UseAutoMapperMiddleware();
}
```

3. 使用方法

```csharp
var res = entity.MapTo<dto>();
```

4. 推荐AutoMapper用法

不使用`Profile`的方式，采用`Attribute`.

```csharp
[AutoMap(typeof(TestUser2), ReverseMap = true)]
public class UserDto
{
    [JsonIgnore]
    public string FirstName{get; set;}
    [JsonIgnore]
    public string LastName{get; set;}

    public string Name
    {
        get
        {
            return $"{FirstName} {LastName}";
        }
        set{}
    }
}
```

```csharp
public class TestUser2: EntityBase
{
    public Guid Id { get; set; }

    public string FirstName{get; set;}

    public string LastName{get; set;}

    public IEnumerable<UserItem> UserItems { get; set; }
}
```
