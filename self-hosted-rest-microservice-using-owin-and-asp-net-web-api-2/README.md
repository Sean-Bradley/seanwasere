# Self Hosted REST Microservice using OWIN and ASP.NET Web API 2

## Video Tutorial
[![Self Hosted REST Microservice using OWIN and ASP.NET Web API 2](https://img.youtube.com/vi/AM2HtQTAQaY/0.jpg)](https://www.youtube.com/watch?v=AM2HtQTAQaY)

[Self Hosted REST Microservice using OWIN and ASP.NET Web API 2](https://www.youtube.com/watch?v=AM2HtQTAQaY)


## All the steps in the video

1. Open Visual Studio Express for Desktop

2. New Project -> C# -> Console Application

3. Name the project “SeansOWINRestService”

4. Tools-> NuGet Package manager

5. `PM> Install-Package Microsoft.AspNet.WebApi.OwinSelfHost`

6. `PM> Install-Package Microsoft.AspNet.WebApi.Cors`

7. Right click the project and Add->Class and name it Startup.cs

8. Replace all of the boilerplate code with: 

```c#
using Owin; 
using System.Web.Http; 

namespace SeansOWINRestService
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

9. Right click the project ADD->Class and Name it ‘WebsitesController’

10. Replace all of the boilerplate code with: 

```c#
using System;
using System.Collections;
using System.Collections.Generic;
using System.Web.Http;
using System.Web.Http.Cors;

namespace SeansOWINRestService
{
    public class Website
    {
        public int Id { get; set; }
        public string Name { get; set; }
        public string Description { get; set; }
    }

    [EnableCors(origins: "*", headers: "*", methods: "*")]
    public class WebsitesController : ApiController
    {
        Website[] websites = new Website[] 
        { 
            new Website { Id = 1, Name = "BirdMMO.com", Description = "Bird Flapping Game For Everybody"}, 
            new Website { Id = 2, Name = "SpiderMMO.com", Description = "Spider Versus Spider Death Match"}, 
            new Website { Id = 3, Name = "LiveAutoWheel.com", Description = "Random Number Generator"},
	        new Website { Id = 4, Name = "SeanWasEre.com", Description = "A Blog of Trivial Things"}  
        };

        // GET api/Websites 
        public IEnumerable Get()
        {
            return websites;
        }

        // GET api/Websites/5 
        public Website Get(int id)
        {
            try
            {
                return websites[id];
            }
            catch (Exception e)
            {
                return new Website();
            }
        }

        // POST api/values 
        public void Post([FromBody]string value)
        {
            Console.WriteLine("Post method called with value = " + value);
        }

        // PUT api/values/5 
        public void Put(int id, [FromBody]string value)
        {
            Console.WriteLine("Put method called with value = " + value);
        }

        // DELETE api/values/5 
        public void Delete(int id)
        {
            Console.WriteLine("Delete method called with id = " + id);
        }
    }
}
```

11. Open Program.cs

12. Replace all of the boilerplate code in the Program.cs file with the following: 

```c#
using Microsoft.Owin.Hosting;
using System;
using System.Net.Http;

namespace SeansOWINRestService
{ 
    public class Program 
    { 
        static void Main() 
        { 
            string baseAddress = "http://127.0.0.1:8080/"; 

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

13. Start it up,

14. Open browser and test visiting 

```
http://127.0.0.1:8080/api/websites
http://127.0.0.1:8080/api/websites/1
http://127.0.0.1:8080/api/websites/0
```

15. Now to create a simple web page to display and manage the data from the Self Hosted OWIN REST Service

16. Open Visual Studio for Web

17. New Project->C#->ASP.net web application

18. Choose Empty Project, with nothing else selected

19. Right click project, ADD->New HTML Page and name it index.html

20. Replace all the HTML code with: 

```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <title>Some of Seans Websites</title>
</head>
<body>

    <div>
        <h2>Some of Seans Websites</h2>
        <ul id="websites" />
    </div>
    <div>
        <h2>Search by ID</h2>
        
        
        <p id="website" />
    </div>

    <a href="http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.js">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.js</a>
    
    <script>
    var uri = 'http://127.0.0.1:8080/api/websites';

    $(document).ready(function () {
        // Send an AJAX request

      $.getJSON(uri)
          .done(function (data) {
            // On success, 'data' contains a list of products.
            $.each(data, function (key, item) {
              // Add a list item for the product.
              $('<li>', { text: formatItem(item) }).appendTo($('#websites'));
            });
          });
    });

    function formatItem(item) {
      return item.Name + ': ' + item.Description;
    }

    function find() {
      var id = $('#websiteId').val();
      $.getJSON(uri + '/' + id)
          .done(function (data) {
            $('#website').text(formatItem(data));
          })
          .fail(function (jqXHR, textStatus, err) {
            $('#website').text('Error: ' + err);
          });
    }
    </script>

</body>
</html>
```

21. Run it and it should all be working

22. Look at the code and experiment with it.



