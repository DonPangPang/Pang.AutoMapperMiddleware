# Pang.AutoMapperMiddleware

���Էǳ�����ʹ��Automapper

## �÷�

### 1. ����

1. ����������ʽ��`service`��ע��AutoMapper

2. �����·���ʽ�����м��

```csharp
public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }
    else
    {
        app.UseExceptionHandler("/Home/Error");
    }
    app.UseStaticFiles();
    
    //�����м��
    app.UseAutoMapperMiddleware();

    app.UseRouting();
    app.UseEndpoints(endpoints =>
    {
        endpoints.MapControllerRoute(
            name: "default",
            pattern: "{controller=Home}/{action=Index}/{id?}");
    });
}
```

3. ʹ�÷���

```csharp
var res = entity.MapTo<dto>();
```

4. �Ƽ�AutoMapper�÷�

��ʹ��`Profile`�ķ�ʽ������`Attribute`.

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
[AutoMap(typeof(UserDto), ReverseMap = true)]
public class TestUser2: EntityBase
{
    public Guid Id { get; set; }

    public string FirstName{get; set;}

    public string LastName{get; set;}

    public IEnumerable<UserItem> UserItems { get; set; }
}
```