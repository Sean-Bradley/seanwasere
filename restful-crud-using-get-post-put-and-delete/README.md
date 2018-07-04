# RESTful CRUD using GET, POST, PUT and DELETE

In this demo,

1. Create the Self Hosted OWIN MicroService

2. Create the minimal HTML and JQuery Client

3. I communicate between the two using GET, POST, PUT and DELETE

[![RESTful CRUD using GET, POST, PUT and DELETE](https://img.youtube.com/vi/5qPamPlcb5I/0.jpg)](https://www.youtube.com/watch?v=5qPamPlcb5I)

[RESTful CRUD using GET, POST, PUT and DELETE](https://www.youtube.com/watch?v=5qPamPlcb5I)


## Create the Self Hosted OWIN MicroService

1. Create new C# Console Application

2. Open Tools->NuGet Package Manager->Package Manager and execute 

`PM> Install-Package Microsoft.AspNet.WebApi.OwinSelfHost`

and also

`PM> Install-Package Microsoft.AspNet.WebApi.Cors`

3. Create new folder ‘Controller’

4. Create new class ‘UserController.cs’

5. Paste the code below 

```c#
using System;
using System.Collections;
using System.Web.Http;
using System.Web.Http.Cors;
using OWINService.Model;

namespace OWINService.Controller
{
    [EnableCors(origins: "*", headers: "*", methods: "*")]
    public class UsersController : ApiController
    {

        // GET api/Users 
        public IEnumerable Get()
        {
            return Program.Users;
        }

        // GET api/Users/5 
        public User Get(int id)
        {
            try
            {
                return Program.Users[id];
            }
            catch (Exception e)
            {
                return new User(-1, "", "");
            }
        }

        // POST api/Users 
        public void Post([FromBody] User value)
        {
            Program.Users.Add(++Program.UserCounter, new User(Program.UserCounter, value.Name, value.City));
        }

        // PUT api/Users/5 
        public void Put(int id, [FromBody] User value)
        {
            Program.Users[id].Name = value.Name;
            Program.Users[id].City = value.City;
        }

        // DELETE api/Users/5 
        public void Delete(int id)
        {
            Program.Users.Remove(id);
        }
    }
}
```

6. Create new folder ‘Model’

7. Create new class ‘User.cs’

8. Paste the code below 

```c#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace OWINService.Model
{
    public class User
    {
        public int Id { get; set; }
        public string Name { get; set; }
        public string City { get; set; }

        public User(int Id, string Name, string City)
        {
            this.Id = Id;
            this.Name = Name;
            this.City = City;
        }
    }
}
```


9. Open program.cs and paste the code below

```c#
using Microsoft.Owin.Hosting;
using System;
using OWINService.Model;
using System.Collections.Generic;

namespace OWINService
{
    public class Program
    {
        public static int UserCounter = 0;
        public static Dictionary Users = new Dictionary();

        static void Main()
        {
            Users.Add(++UserCounter, new User(UserCounter, "Sean", "London"));
            Users.Add(++UserCounter, new User(UserCounter, "Emmy", "Helsinki"));
            Users.Add(++UserCounter, new User(UserCounter, "Cosmo", "New York"));

            string baseAddress = "http://*:8080";

            // Start OWIN host
            using (WebApp.Start(url: baseAddress))
            {
                Console.WriteLine("Service Listening at " + baseAddress);

                System.Threading.Thread.Sleep(-1);
            }
        }
    }
}
```

10. Create new class ‘Startup.cs’

11. Copy and paste the code below 

```c#
using Owin;
using System.Web.Http;

namespace OWINService
{
    public class Startup
    {
        // This code configures Web API. The Startup class is specified as a type
        // parameter in the WebApp.Start method.
        public void Configuration(IAppBuilder appBuilder)
        {
            // Configure Web API for self-host.
            HttpConfiguration config = new HttpConfiguration();
            config.EnableCors();
            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );

            appBuilder.UseWebApi(config);
        }
    }
}
```

12. Build and Execute

13. Leave it running

## Create the minimal HTML and JQuery Client

1. Open Visual Studio 2015 again

2. Create new project->C# -> Web -> ASP.Net Web Application

3. Choose Empty project, deselect any check boxes.

4. Paste the html code from my GitHub page at [https://github.com/Sean-Bradley/SeansOWINRestfulService/blob/master/index.html](https://github.com/Sean-Bradley/SeansOWINRestfulService/blob/master/index.html)

5. Press Play and Test


This code from this tutorial is also hosted at [https://github.com/Sean-Bradley/SeansOWINRestfulService](https://github.com/Sean-Bradley/SeansOWINRestfulService)


Thanks for reading, remember to like, comment, subscribe and share.


