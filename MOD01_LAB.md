# Module 1: Exploring ASP.NET Core MVC

# Lab: Exploring ASP.NET Core MVC 

Estimated Time: **90 minutes**

### Exercise 1: Exploring a Razor Pages Application

#### Task 1: Creating a Razor Pages application

1. Start Visual Studio 2017.

2. In the **Start Page - Microsoft Visual Studio** window, on the **FILE** menu, point to **New**, and then click **Project**.

3. In the **New Project** dialog box, in the navigation pane, expand **Installed**, and then click **Visual C#**.

4. In the **New Project** dialog box, in the result pane, click **ASP.NET Core Web Application**.

5. In the **Name** box, type **ActorsRazorPages**.

6. Replace the content of the **Location** box with **[Repository Root]\Allfiles\Mod01\Labfiles\01_ActorsRazorPages_begin**, and then click **OK**.

7. In the result pane of the **New ASP.NET Core Web Application - ActorsRazorPages** dialog box, select **ASP.NET Core 2.1** from the dropdown at the top of the dialog box.

7. In the result pane of the **New ASP.NET Core Web Application - ActorsRazorPages** dialog box, ensure that the **Configure for HTTPS** check box is not selected.

8. In the **New ASP.NET Core Web Application - ActorsRazorPages** dialog box, in the result pane, click **Web Application**, and then click **OK**.

9. In the **ActorsRazorPages –  Microsoft Visual Studio** window, on the **DEBUG** menu, click **Start Without Debugging**.

10. In Microsoft Edge, in the address bar, note the port number that appears at the end of the URL **http://localhost:[port]**. You will use the port number during this lab.

11. In Microsoft Edge, in the navigation bar, click **Contact** to review its content.

12. In Microsoft Edge, click **Close**.
 
#### Task 2: Explore the application structure

1. In the **ActorsRazorPages - Microsoft Visual Studio** window, in **Solution Explorer**, expand **Pages**, and then click  **_ViewStart.cshtml**.

2. In the **_ViewStart.cshtml** code window, note that the value of **Layout** is **"_Layout"**.

    >**Note**: This indicates that all the files inside the **Pages** folder use the same layout file, **~/Pages/_Layout.cshtml**.

3. In the **ActorsRazorPages - Microsoft Visual Studio** window, in **Solution Explorer**, under **Pages**, click **Contact.cshtml**.

4. In the **Contact.cshtml** code window, examine the Razor code, and verify that there are no links to .css files.

5. In the **ActorsRazorPages - Microsoft Visual Studio** window, in **Solution Explorer**, expand **Pages**, expand **Shared**, and then click  **_Layout.cshtml**.

6. In the **_Layout.cshtml** code window, in the **HEAD** element, note that there is a link to **~/css/site.css**.

7. In the **ActorsRazorPages - Microsoft Visual Studio** window, in **Solution Explorer**, under **ActorsRazorPages**, expand **wwwroot**, expand **css**, and then click **site.css**

    >**Note**: This is the CSS stylesheet file that is applied in the **_Layout.cshtml**.

#### Task 3: Add simple functionality

1. In the **ActorsRazorPages - Microsoft Visual Studio** window, in **Solution Explorer**, right-click **Pages**, point to **Add**, and then click **New Item**.

2. In the **Add New Item – ActorsRazorPages** dialog box, click **Razor Page**.

3. In the **Add New Item – ActorsRazorPages** dialog box, in the **Name** box, type **TestPage**, and then click **Add**. 

4. In the **ActorsRazorPages – Microsoft Visual Studio** window, in the **TestPage.cshtml** code window, replace the content below **@model line**  with the following code:
  ```cs
       @{
        ViewData["Title"] = "Test Page";
       }

       <h1>@ViewData["Title"]</h1>
       <h2>This is a Test Page</h2>
```

5. In the **ActorsRazorPages - Microsoft Visual Studio** window, in **Solution Explorer**, expand **Pages**, expand **Shared** and then click  **_Layout.cshtml**.

6. In the **_Layout.cshtml** code window, locate the following code:
  ```cs
       <li><a asp-page="/Contact">Contact</a></li>
```

7. Place the cursor after the located code, press Enter, and then type the following code:
  ```cs
       <li><a asp-page="/TestPage">Test Page</a></li>
```

8. In the **ActorsRazorPages - Microsoft Visual Studio** window, in **Solution Explorer**, right-click **ActorsRazorPages**, point to **Add**, and then click **New Folder**.

9. In the **NewFolder** box, type **Models**, and then press Enter.

10. In the **ActorsRazorPages - Microsoft Visual Studio** window, in **Solution Explorer**, right-click **Models**, point to **Add**, and then click **Class**.

11. In the **Add New Item – ActorsRazorPages** dialog box, in the **Name** box, type **Actor**, and then click **Add**.
    
12. In the **Actor.cs** code block, place the cursor after the second **{** (opening braces) sign, press Enter, and then type the following code:
  ```cs
       public int Id { get; set; }
       public string FirstName { get; set; }
       public string LastName { get; set; }
       public string KnownFor { get; set; }
       public bool OscarWinner { get; set; }
       public string ImageName { get; set; }
```
13. In the **ActorsRazorPages - Microsoft Visual Studio** window, in **Solution Explorer**, right-click **Models**, point to **Add**, and then click **New Item**.

14. In the **Add New Item – ActorsRazorPages** dialog box, click **Interface**.  

15. In the **Add New Item – ActorsRazorPages** dialog box, in the **Name** box, type **IData**, and then click **Add**.

16. In the **IData** interface code block, place the cursor before the word **interface**, and then type **public**.

17. In the **IData** interface code block, place the cursor after the second **{** (opening braces) sign, press Enter, and then type the following code:
  ```cs
       List<Actor> ActorsList { get; set; }
       List<Actor> ActorsInitializeData();
       Actor GetActorById(int? id);
```

18. In the **ActorsRazorPages - Microsoft Visual Studio** window, in **Solution Explorer**, right-click **Models**, point to **Add**, and then select  **Existing Item**.

19. In the dialog box navigate to **[Repository Root]\Allfiles\Mod01\Labfiles\01_ActorsRazorPages_begin**, click **Data.cs**, and then click **Add**.

    >**Note**: Examine the **Data.cs** class content.

20. In the **ActorsRazorPages - Microsoft Visual Studio** window, in **Solution Explorer**, under **wwwroot**, right-click **images**, point to **Add**, and then click **Existing Item**.

21. In the dialog box, navigate to **[Repository Root]\Allfiles\Mod01\Labfiles\01_ActorsRazorPages_begin\Images**, select all the images, and then click **Add**.

22. In the **ActorsRazorPages - Microsoft Visual Studio** window, in **Solution Explorer**,  right-click **Pages**, point to **Add**, and then select **New folder**.

23. In the **NewFolder** box, type **Actors**, and then press Enter.

24. In the **ActorsRazorPages - Microsoft Visual Studio** window, in **Solution Explorer**, under **Pages**, right-click **Actors**, point to **Add**, and then click **New Item**. 

25. In the **Add New Item - ActorsRazorPages** dialog box, click **Web**, and then, in the result pane, click **Razor Page**.

26. In the **Add New Item – ActorsRazorPages** dialog box, in the **Name** box, type **Index**, and then click **Add**.

27. In the **ActorsRazorPages - Microsoft Visual Studio** window, in **Solution Explorer**, expand **Index.cshtml**, click **Index.cshtml.cs**, select the following code, and then press Delete.
  ```cs
       public void OnGet()
       {
       }
```

28. In the **Index.cshtml.cs** code window, place the cursor at the end of the **using Microsoft.AspNetCore.Mvc.RazorPages** namespace code, press Enter, and then type the following code:
  ```cs
       using ActorsRazorPages.Models;
```

29. In the **Index.cshtml.cs** code block, place the cursor after the second **{** (opening braces) sign, press Enter, and then type the following code:
  ```cs
       private IData _data;

       public IndexModel(IData data)
       {
           _data = data;
       }

       public IList<Actor> Actors { get; set; }

       public void OnGet()
       {
          Actors = _data.ActorsInitializeData();
       }
```

30. In the **ActorsRazorPages - Microsoft Visual Studio** window, in **Solution Explorer**, under **Pages**, under **Actors**, click **Index.cshtml**.

31. In the **ActorsRazorPages – Microsoft Visual Studio** window, in the **Index.cshtml** code window, replace the content below **@model line** with the following code:
  ```cs
       @{
           ViewData["Title"] = "Index";
       }

       <h2>Index</h2>

       <table class="table">
            <thead>
                <tr>
                    <th>
                        @Html.DisplayNameFor(model => model.Actors[0].FirstName)
                    </th>
                    <th>
                        @Html.DisplayNameFor(model => model.Actors[0].LastName)
                    </th>
                    <th></th>
                </tr>
            </thead>
            <tbody>
                @foreach (var item in Model.Actors)
                {
                <tr>
                    <td>
                        @Html.DisplayFor(modelItem => item.FirstName)
                    </td>
                    <td>
                        @Html.DisplayFor(modelItem => item.LastName)
                    </td>
                    <td>
                        <a asp-page="./Details" asp-route-id="@item.Id">Details</a>
                    </td>
                </tr>
                }
            </tbody>
       </table>
```

32. In the **ActorsRazorPages - Microsoft Visual Studio** window, in **Solution Explorer**, under **Pages**, right-click **Actors**, point to **Add**, and then click  **Existing Item**.

33. In the dialog box, navigate to **[Repository Root]\Allfiles\Mod01\Labfiles\01_ActorsRazorPages_begin\Pages**, select **Details.cshtml.cs** and **Details.cshtml**, and then click **Add**. 

    >**Note**: Examine the content of the **Details.cshtml.cs** and **Details.cshtml** files.

34. In the **ActorsRazorPages - Microsoft Visual Studio** window, in **Solution Explorer**, click **Startup.cs**.

35. Ensure that the cursor is at the end of the **using Microsoft.Extensions.DependencyInjection** namespace code, press Enter, and then type the following code:
  ```cs
       using ActorsRazorPages.Models;
```

36. Place the cursor after the **{** (opening braces) sign of the **ConfigureServices** method, press Enter, and then type the following code:
  ```cs
       services.AddSingleton<IData, Data>();
``` 

37. In the **ActorsRazorPages - Microsoft Visual Studio** window, in **Solution Explorer**, expand **Pages**, expand **Shared**, and then double-click  **_Layout.cshtml**.

38. In the **_Layout.cshtml** code window, locate the following code:
  ```cs
       <li><a asp-page="/TestPage">Test Page</a></li>
```

39. Place the cursor after the located code, press Enter, and then type the following code:
  ```cs
       <li><a asp-page="/Actors/Index">Actors</a></li>
```

#### Task 4: Run the application

1. In the  **ActorsRazorPages – Microsoft Visual Studio** window, on the **FILE** menu, click **Save All**.

2. In the **ActorsRazorPages – Microsoft Visual Studio** window, on the **DEBUG** menu, click **Start Without Debugging**.

3. In Microsoft Edge, in the navigation bar, click **Test Page**  to view its content.

    >**Note**: The browser window displays the title **Test Page** and the text **&quot;This is a Test Page&quot;**. 
    
4. In the **Test Page** window, in the navigation bar, click **Actors** to view its content.

    >**Note**: The browser window displays the **Index.cshtml** page under the **Actors** folder.

5. In the **Actors** window, select an actor, and then click **Details** to go to the **Details** page.
   
    >**Note**: The browser window displays the **Details.cshtml** page under the **Actors** folder.
 
6. Verify that the standard site layout and styles have been applied to all the pages.

7. In Microsoft Edge, click **Close**.

8. In the **ActorsRazorPages - Microsoft Visual Studio** window, on the **FILE** menu, click **Exit**.

>**Results**: At the end of this exercise, you will be able to build a simple Razor Pages application in Visual Studio.

### Exercise 2: Exploring a Web API Application

#### Task 1: Creating a Web API application

1. Start Visual Studio 2017.

2. In the **Start Page - Microsoft Visual Studio** window, on the **FILE** menu, point to **New**, and then click **Project**.

3. In the **New Project** dialog box, in the navigation pane, expand **Installed**, and then click **Visual C#**.

4. In the **New Project** dialog box, in the result pane, click **ASP.NET Core Web Application**.

5.  In the **Name** box, type **CakeStoreApi**.

6. In the **Location** box, replace its content with **[Repository Root]\Allfiles\Mod01\Labfiles\02_CakeStoreApi_begin**, and then click **OK**.

7. In the result pane of the **New ASP.NET Core Web Application - CakeStoreApi**  dialog box, ensure that the **Configure for HTTPS** check box is not selected.

8. In the **New ASP.NET Core Web Application - CakeStoreApi**  dialog box, in the result pane, click **API**,  and then click **OK**.
 
#### Task 2: Explore the application structure

1. In the **CakeStoreApi - Microsoft Visual Studio** window, in **Solution Explorer**, expand **Controllers**, and then click  **ValuesController.cs**.

    >**Note**: The **Get()** method returns **value1** and **value2**.

2. In the **CakeStoreApi – Microsoft Visual Studio** window, on the **DEBUG** menu, click **Start Without Debugging**. 

    >**Note**: The browser displays **"["value1","value2"]"**.

3. In Microsoft Edge, click **Close**.

#### Task 3: Add simple functionality

1. In the **CakeStoreApi - Microsoft Visual Studio** window, in **Solution Explorer**, right-click **CakeStoreApi**, point to **Add**, and then click **New Folder**.

2. In the **NewFolder** box, type **Models**, and then press Enter.

3. In the **CakeStoreApi - Microsoft Visual Studio** window, in **Solution Explorer**, right-click **Models**, point to **Add**, and then click **Class**.

4. In the **Add New Item – CakeStoreApi** dialog box, in the **Name** box, type **CakeStore**, and then click **Add**.
    
5. In the **CakeStore.cs** code block, place the cursor after the second **{** (opening braces) sign, press Enter, and then type the following code:
  ```cs
       public int Id { get; set; }
       public string CakeType { get; set; }
       public int Quantity { get; set; }
```

6. In the **CakeStoreApi - Microsoft Visual Studio** window, in **Solution Explorer**,  right-click **Models**, point to **Add**, and then click **New Item**.

7. In the **Add New Item - CakeStoreApi** dialog box, click **Interface**.

8. In the **Add New Item – CakeStoreApi** dialog box, in the **Name** box, type **IData**, and then click **Add**.

9. In the **IData.cs** code block, place the cursor before the word **interface**, and then type **public**.

10. In the **IData.cs** code block, place the cursor after the second **{** (opening braces) sign, press Enter, and then type the following code:
  ```cs
       List<CakeStore> CakesList { get; set; }
       List<CakeStore> CakesInitializeData();
       CakeStore GetCakeById(int? id);
```

11. In the **CakeStoreApi - Microsoft Visual Studio** window, in **Solution Explorer**, right-click **Models**, point to **Add**, and select  **Existing Item**.

12. In the dialog box, navigate to **[Repository Root]\Allfiles\Mod01\Labfiles\02_CakeStoreApi_begin**, click **Data.cs**, and then click **Add**.

    >**Note**: Examine the content in **Data.cs**.

13. In the **CakeStoreApi - Microsoft Visual Studio** window, in **Solution Explorer**, right-click **Controllers**, point to **Add**, and then click **Controller**.

14. In the **Template** list, click **API Controller - Empty**, and then click **Add**.

15. In the **Add Empty API Controller** dialog box, in the **Controller name** box, type **CakeStoreApiController**, and then click **Add**.

16. In the **CakeStoreApiController.cs** code block, ensure that the cursor is at the end of the **using Microsoft.AspNetCore.Mvc** namespace code, press Enter, and then type the following code:
  ```cs
       using CakeStoreApi.Models;
```
17. In the **CakeStoreApiController.cs** code block, place the cursor after the second **{** (opening braces) sign, press Enter, and then type the following code:
  ```cs
       private IData _data;

       public CakeStoreApiController(IData data)
       {
           _data = data;
       }
        
       [HttpGet("/api/CakeStore")]
       public ActionResult<List<CakeStore>> GetAll()
       {
           return _data.CakesInitializeData();
       }
        
       [HttpGet("/api/CakeStore/{id}", Name = "GetCake")]
       public ActionResult<CakeStore> GetById(int? id)
       {
          var item = _data.GetCakeById(id);
          if (item == null)
          {
              return NotFound();
          }
          return new ObjectResult(item);
       }
```
>**Note**: The contents inside the **HttpGet** attributes indicate the URL that the user should write to get to the relevant action.

18. In the **CakeStoreApi - Microsoft Visual Studio** window, in **Solution Explorer**, click **Startup.cs**.

19. Ensure that the cursor is at the end of the **using Microsoft.Extensions.Options** namespace code, press Enter, and then type the following code:
  ```cs
       using CakeStoreApi.Models;
```

20. Place the cursor after the **{** (opening braces) sign of the **ConfigureServices** method, press Enter, and then type the following code:
  ```cs
       services.AddSingleton<IData, Data>();
``` 

#### Task 4: Run the application

1. In the  **CakeStoreApi – Microsoft Visual Studio** window, on the **FILE** menu, click **Save All**.

2. In the **CakeStoreApi – Microsoft Visual Studio** window, on the **DEBUG** menu, click **Start Without Debugging**.

3. In Microsoft Edge, in the address bar, type **http://localhost:[port]/api/CakeStore**, and then press Enter.

    >**Note**: The browser displays a list of cakes in JSON format.
    
4. In Microsoft Edge, in the address bar, type **http://localhost:[port]/api/CakeStore/1**, and then press Enter.

    >**Note**: The browser displays the first cake in the JSON format.

5. In Microsoft Edge, click **Close**.

6. In the **CakeStoreApi - Microsoft Visual Studio** window, on the **FILE** menu, click **Exit**.

>**Results**: At the end of this exercise, you will be able to build a simple Web API application in Visual Studio.

### Exercise 3: Exploring an MVC Application

#### Task 1: Creating an MVC application

1. Start Visual Studio 2017.

2. In the **Start Page - Microsoft Visual Studio** window, on the **FILE** menu, point to **New**, and then click **Project**.

3. In the **New Project** dialog box, in the navigation pane, expand **Installed**, and then click **Visual C#**.

4. In the **New Project** dialog box, in the result pane, click **ASP.NET Core Web Application**.

5. In the **Name** box, type **AnimalsMvc**.

6. In the **Location** box, replace the contents with **[Repository Root]\Allfiles\Mod01\Labfiles\03_AnimalsMvc_begin**, and then click **OK**.

7. In the result pane of the **New ASP.NET Core Web Application - AnimalsMvc** dialog box, ensure that the **Configure for HTTPS** check box is not selected.

7. In the **New ASP.NET Core Web Application** dialog box, in the result pane, click **Web Application (Model-View-Controller)**, and then click **OK**.

8. In the **AnimalsMvc –  Microsoft Visual Studio** window, on the **DEBUG** menu, click **Start Without Debugging**.

9. In Microsoft Edge, in the navigation bar, click **Contact** to review its content.

10. In Microsoft Edge, click **Close**.
 
#### Task 2: Explore the application structure

1. In the **AnimalsMvc - Microsoft Visual Studio** window, in **Solution Explorer**, expand **Views**, and then click **_ViewStart.cshtml**.

2. In the **_ViewStart.cshtml** code window, note the value for **Layout** is **"_Layout";**.

3. In the **AnimalsMvc - Microsoft Visual Studio** window, in **Solution Explorer**, under **Views**, expand **Home**, and then click **Contact.cshtml**.

4. In the **Contact.cshtml** code window, note there are no files with the .css extension.

5. In the **AnimalsMvc - Microsoft Visual Studio** window, in **Solution Explorer**, under **Views**, collapse **Home**, expand **Shared**, and then click **_Layout.cshtml.**

6. In the **_Layout.cshtml** code window, note that in the **HEAD** element there is a link to **~/css/site.css**.

7. In the **AnimalsMvc - Microsoft Visual Studio** window, in **Solution Explorer**, under **AnimalsMvc**, expand **wwwroot**, expand **css**, and then click **site.css**.

    >**Note**: This is the CSS stylesheet file that was applied in the **_Layout.cshtml**.

#### Task 3: Add simple functionality

1. In the **AnimalsMvc - Microsoft Visual Studio** window, in **Solution Explorer**, expand **Controllers**, click **HomeController.cs**, and then locate the following code:
  ```cs
       public IActionResult Error()
       {
           return View(new ErrorViewModel { RequestId = Activity.Current?.Id ?? HttpContext.TraceIdentifier });
       }
```

2. Place the cursor after the **}** (closing braces) sign of the located code, press Enter, and then type the following code:
  ```cs
       public IActionResult TestPage()
       {
           return View();
       }
```

3. Right-click the code you just added, and then click **Add View**.

4. In the **Add MVC View** dialog box, ensure that the value in the **View name** box is **TestPage**.  

5. In the **Add MVC View** dialog box, ensure that the **Empty (without model)** template is selected.

6. In the **Add MVC View** dialog box, ensure that the **Create as a partial view** check box is cleared and the **Use a layout page** check box is selected, and then click **Add**.

7. In the **TestPage.cshtml** code window, select the following code:
  ```cs
       <h2>TestPage</h2>
```

8. Replace the selected code with the following code: 
  ```cs
       <h2>This is a Test Page</h2>
```

9. In the **AnimalsMvc - Microsoft Visual Studio** window, in **Solution Explorer**, under **Views**, expand **Shared**, and then click **_Layout.cshtml.**

10. In the **_Layout.cshtml** code window, locate the following code: 
  ```cs
       <li><a asp-area="" asp-controller="Home" asp-action="Contact">Contact</a></li>
```
11. Place the cursor after the located code, press Enter, and then type the following code:
  ```cs
       <li><a asp-area="" asp-controller="Home" asp-action="TestPage">Test Page</a></li>
```
12. In the **AnimalsMvc  – Microsoft Visual Studio** window, in **Solution Explorer**, right-click **Models**, point to **Add**, and then click **Class**.

13. In the **Add New Item – AnimalsMvc** dialog box, in the **Name** box, type **Animal**, and then click **Add**.
    
14. In the **Animal.cs** code block, place the cursor after the second **{** (opening braces) sign, press Enter, and then type the following code:
  ```cs
       public int Id { get; set; }
       public string Name { get; set; }
       public string ImageName { get; set; }
       public string UniqueInformation { get; set; }
       public string Category { get; set; }
```

15. In the **AnimalsMvc - Microsoft Visual Studio** window, in **Solution Explorer**, right-click **Models**, point to **Add**, and then click **New Item**. 

16. In the **Add New Item - AnimalsMvc** dialog box, click **Interface**. 

17. In the **Add New Item – AnimalsMvc** dialog box, in the **Name** box, type **IData**, and then click **Add**.

18. In the **IData** interface code block, place the cursor before the word **interface**, and then write **public**.

19. In the **IData** interface code block, place the cursor after the second **{** (opening braces) sign, press Enter, and then type the following code:
  ```cs
       List<Animal> AnimalsList { get; set; }
       List<Animal> AnimalsInitializeData();
       Animal GetAnimalById(int? id);
```
20. In the **AnimalsMvc  – Microsoft Visual Studio** window, in **Solution Explorer**, right-click **Models**, point to **Add**, and then click **Existing Item**.

21. In the dialog box, navigate to **[Repository Root]\Allfiles\Mod01\Labfiles\03_AnimalsMvc_begin**, click **Data.cs**, and then click **Add**.

    >**Note**: Examine the contents of **Data.cs** .

22. In the **AnimalsMvc - Microsoft Visual Studio** window, in **Solution Explorer**, right-click  on the **Models**, point to **Add**, and then click **Class**.

23. In the **Add New Item – AnimalsMvc** dialog box, in the **Name** box, type **IndexViewModel**, and then click **Add**.

24. In the **IndexViewModel.cs** code block, place the cursor after the second **{** (opening braces) sign, press Enter, and then type the following code:
  ```cs
       public List<Animal> Animals { get; set; }
```

25. In the **AnimalsMvc - Microsoft Visual Studio** window, in **Solution Explorer**, right-click **Controllers**, point to **Add**, and then click **Controller**.

26. In the **Add Scaffold** dialog box, click **MVC Controller - Empty**, and then click **Add**.

27. In the **Add Empty MVC Controller** dialog box, in the **Controller name** box, type **AnimalsController**, and then click **Add**.

28. In the **AnimalsController.cs** code window, ensure that the cursor is at the end of the **using Microsoft.AspNetCore.Mvc** namespace code, press Enter, and then type the following code:
  ```cs
       using AnimalsMvc.Models;
```
29. In the **AnimalsController.cs** code window, select the following code, and then press Delete.
  ```cs
       public IActionResult Index()
       {
           return View();
       }
```

30. In the **AnimalsController.cs** code block, place the cursor after the second **{** (opening braces) sign, press Enter, and then type the following code:
  ```cs
       private IData _tempData;
       public AnimalsController(IData tempData)
       {
            _tempData = tempData;
       }

       public IActionResult Index()
       {
            List<Animal> animals = _tempData.AnimalsInitializeData();
            IndexViewModel indexViewModel = new IndexViewModel();
            indexViewModel.Animals = animals;
            return View(indexViewModel);
       }

       public IActionResult Details(int? id)
       {
            var model = _tempData.GetAnimalById(id);
            if (model == null)
            {
                return NotFound();
            }
            return View(model);
       }   
``` 

31. In the **AnimalsMvc - Microsoft Visual Studio** window, in **Solution Explorer**, expand **wwwroot**, right-click on the **images**, point to **Add**, and then click  **Existing Item**.

32. In the dialog box, navigate to **[Repository Root]\Allfiles\Mod01\Labfiles\03_AnimalsMvc_begin\Images**, select all the images, and then click **Add**.

33. In the **AnimalsController.cs** code window, locate the following code, right-click the code, and then click **Add View**.
  ```cs
       public IActionResult Index()
```
34. In the **Add MVC View** dialog box, ensure that the value in the **View name** box is **Index**.  

35. In the **Add MVC View** dialog box, ensure that the **Empty (without model)** template is selected.

36. In the **Add MVC View** dialog box, ensure that the **Create as a partial view** check box is cleared and the **Use a layout page** check box is selected, and then click **Add**.

37. In the **Index.cshtml**, erase all the content in the window, and type the following code:
  ```cs
       @model AnimalsMvc.Models.IndexViewModel
       @{
            ViewData["Title"] = "Index";
       }

       <h2>Index</h2>

       <table class="table">
            <thead>
                <tr>
                    <th>
                        @Html.DisplayNameFor(model => model.Animals[0].Name)
                    </th>
                    <th>
                        @Html.DisplayNameFor(model => model.Animals[0].Category)
                    </th>
                    <th></th>
                </tr>
            </thead>
            <tbody>
                @foreach (var item in Model.Animals)
                {
                    <tr>
                        <td>
                            @Html.DisplayFor(modelItem => item.Name)
                        </td>
                        <td>
                            @Html.DisplayFor(modelItem => item.Category)
                        </td>
                        <td>
                            <a asp-action="Details" asp-route-id="@item.Id">Details</a>
                        </td>
                    </tr>
                }
            </tbody>
       </table>
```

38. In the **AnimalsMvc - Microsoft Visual Studio** window, in the Solution Explorer, under **Controllers**, click **AnimalsController.cs**.

39. In the **AnimalsController.cs** code window, locate the following code, right-click the code, and then click **Add View**.
  ```cs
       public IActionResult Details(int? id)
```
40. In the **Add MVC View** dialog box, ensure that the value in the **View name** box is **Details**.  

41. In the **Add MVC View** dialog box, ensure that the **Empty (without model)** template is selected.

42. In the **Add MVC View** dialog box, ensure that the **Create as a partial view** check box is cleared and the **Use a layout page** check box is selected, and then click **Add**.

43.  In **Details.cshtml**, erase all the contents in the  window, and type the following code:
  ```cs
       @model AnimalsMvc.Models.Animal
       @{
            ViewData["Title"] = "Details";
       }

       <h2>Details</h2>

       <div>
            <h4>Animal</h4>
            <hr />
            <dl class="dl-horizontal">
                <dt>
                    @Html.DisplayNameFor(model => model.Name)
                </dt>
                <dd>
                    @Html.DisplayFor(model => model.Name)
                </dd>
                <dt>
                    @Html.DisplayNameFor(model => model.Category)
                </dt>
                <dd>
                    @Html.DisplayFor(model => model.Category)
                </dd>
                <dt>
                    @Html.DisplayNameFor(model => model.UniqueInformation)
                </dt>
                <dd>
                    @Html.DisplayFor(model => model.UniqueInformation)
                </dd>
            </dl>

            <div style="padding:10px;">
                @if (Model.ImageName != "")
                {
                    <img src="~/images/@Model.ImageName" alt="Sample Image" height="300" />
                }

            </div>
       </div>
       <div>
            <a asp-action="Index">Back to List</a>
       </div>
```

44. In the **AnimalsMvc - Microsoft Visual Studio** window, in **Solution Explorer**, under **Views**, under **Shared**, click **_Layout.cshtml.**


45. In the **_Layout.cshtml** code window, locate the following code: 
  ```cs
       <li><a asp-area="" asp-controller="Home" asp-action="TestPage">Test Page</a></li>
```
46. Place the cursor after the located code, press Enter, and then type the following code:
  ```cs
       <li><a asp-area="" asp-controller="Animals" asp-action="Index">Animals</a></li>
```

47. In the **AnimalsMvc - Microsoft Visual Studio** window, in **Solution Explorer**, click **Startup.cs**.

48. Ensure that the cursor is at the end of the **using Microsoft.Extensions.DependencyInjection** namespace code, press Enter, and then type the following code:
  ```cs
       using AnimalsMvc.Models;
```
   
49. Place the cursor after the **{** (opening braces) sign of the **ConfigureServices** method, press Enter, and then type the following code:
  ```cs
       services.AddSingleton<IData, Data>();
``` 

#### Task 4: Run the application

1. In the  **AnimalsMvc – Microsoft Visual Studio** window, on the **FILE** menu, click **Save All**.

2. In the **AnimalsMvc – Microsoft Visual Studio** window, on the **DEBUG** menu, click **Start Without Debugging**.

3. In Microsoft Edge, in the navigation bar, click **Test Page** to review its content.

    >**Note**: The browser window displays the text **&quot;This is a Test Page&quot;**.
    
4. In the **Test Page** window, in the navigation bar, click **Animals** to view its content.

    >**Note**: The browser window displays the **Index.cshtml** page, under the **Animals** folder.

5. In the **Animals** window, select an animal, and then click **Details** to go to the **Details** page.
 
    >**Note**: The browser window displays the **Details.cshtml** page, under the **Animals** folder.
 
6. Verify that the standard site layout and styles have been applied to all the pages.

11. In Microsoft Edge, click **Close**.

12. In the **AnimalsMvc - Microsoft Visual Studio** window, on the **FILE** menu, click **Exit**.

>**Results**: At the end of this exercise, you will be able to build a simple MVC application in Visual Studio.

©2018 Microsoft Corporation. All rights reserved.

The text in this document is available under the  [Creative Commons Attribution 3.0 License](https://creativecommons.org/licenses/by/3.0/legalcode), additional terms may apply. All other content contained in this document (including, without limitation, trademarks, logos, images, etc.) are  **not**  included within the Creative Commons license grant. This document does not provide you with any legal rights to any intellectual property in any Microsoft product. You may copy and use this document for your internal, reference purposes.

This document is provided &quot;as-is.&quot; Information and views expressed in this document, including URL and other Internet Web site references, may change without notice. You bear the risk of using it. Some examples are for illustration only and are fictitious. No real association is intended or inferred. Microsoft makes no warranties, express or implied, with respect to the information provided here.
