
## Tutuorial MySQL

1. Install 3 packages: 
Microsoft.EntityFrameworkCore
Microsoft.EntityFrameworkCore.Tools
Pomelo.EntityFrameworkCore.MySql

2. appsettings.json
```
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "AllowedHosts": "*",
  "ConnectionStrings": {
    "MySqlConn" : "Server=localhost;Database=DotCore;User=root;Password=root;"
  }
}
```

3. Models.{modelname}.cs - Create the model with the attributes (? = nullable)
```
public class Customer
    {
        public int id { get; set; }
        public string? CustomerName { get; set; }
        public string? Address { get; set; }
        public string? EmailAddress { get; set; }
    }

```

4. Data folder with AppDbContext.cs
```
using Microsoft.EntityFrameworkCore;
using WebApplication1.Models;

namespace WebApplication1.Data
{
    public class AppDbContext : DbContext
    {
        public AppDbContext(DbContextOptions<AppDbContext> options) : base(options)
        {

        }

        public DbSet<Customer> Customers { get; set; }
    }
}

```

5. Program.cs - Add this code before build
```
var connectionString = builder.Configuration.GetConnectionString("MySqlConn");

            builder.Services.AddDbContext<AppDbContext>(options => {
                options.UseMySql(connectionString, ServerVersion.AutoDetect(connectionString));
            });
```

6. In Package Mangager Console - run this command:
```
Add-Migration initDB
```