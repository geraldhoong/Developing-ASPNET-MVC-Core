# Module 09: Managing Security

# Lab: Managing Security

Estimated Time: **60 minutes**

### Exercise 1: Use Identity

#### Task 1: Add the Entity Framework database context

1. In File Explorer, navigate to **[Repository Root]\Allfiles\Mod09\Labfiles\01_Library_begin\Library**, and then from the address bar, copy the address.

2. Click **Start**, and then type **cmd**.

3. Under **Best match**, right-click **Command Prompt**, and then click **Run as administrator**.

4. In the **User Account Control** dialog box, click **Yes**.

5. In the **Administrator: Command Prompt** window, type the following command, and then press Enter.
  ```cs
       cd  {copied folder path}
```

>**Note**: If the *{copied folder path}* is different from the disk drive where the command prompt is located, then you should type *{disk drive}:* before typing the **cd** *{copied folder path}* command.

6. In the **Administrator: Command Prompt** window, type the following command, and then press Enter.
  ```cs
       npm install
```
>**Note**: If warning messages are shown in the command prompt, you can ignore them.

7. Close the window.

8. In File Explorer, navigate to **[Repository Root]\Allfiles\Mod09\Labfiles\01_Library_begin**, and then double-click **Library.sln**.

    >**Note**: If a **Security Warning for Library** dialog box appears, verify that the **Ask me for every project in this solution** check box is cleared, and then click OK.

9. In the **Library - Microsoft Visual Studio** window, in Solution Explorer, expand **Models**, and then click **User.cs**.

10. In the **User.cs** code window, locate the following code:
  ```cs
      using System.Threading.Tasks;
```
11. Ensure that the cursor is at the end of the  **System.Threading.Tasks** namespace, press Enter, and then type the following code:
  ```cs
      using Microsoft.AspNetCore.Identity;
```

12. In the **User.cs** code window, locate the following code:
  ```cs
      public class User
```

13.  Append the following code to the existing line of code.
  ```cs
      : IdentityUser
```

14. In the **Library - Microsoft Visual Studio** window, in Solution Explorer, expand **Data**, and then click **LibraryContext.cs**.

15. In the **LibraryContext.cs** code window, locate the following code:
  ```cs
      using System.Threading.Tasks;
```
16. Ensure that the cursor is at the end of the  **System.Threading.Tasks** namespace, press Enter, and then type the following code:
  ```cs
      using Microsoft.AspNetCore.Identity.EntityFrameworkCore;
```

17. In the **LibraryContext.cs** code window, locate the following code:
  ```cs
      public class LibraryContext : DbContext
```

18. Replace the selected code with the following code:
  ```cs
      public class LibraryContext : IdentityDbContext<User>
```

#### Task 2: Enable using Identity

1. In the **Library - Microsoft Visual Studio** window, in Solution Explorer, click **Startup.cs**.

2. In the **Startup.cs** code window, locate the following code:
  ```cs
      using Microsoft.Extensions.DependencyInjection;
```
3. Ensure that the cursor is at the end of the  **Microsoft.Extensions.DependencyInjection** namespace, press Enter, and then type the following code:
  ```cs
      using Library.Models;
      using Microsoft.AspNetCore.Identity;
```

4. In the **Startup.cs** code window, in the **ConfigureServices** method, place the cursor after the **{** (opening braces) sign, press Enter, type the following code, and then press Enter.
  ```cs
       services.AddIdentity<User, IdentityRole>(options =>
       {
           options.Password.RequireDigit = true;
           options.Password.RequiredLength = 7;
           options.Password.RequireUppercase = true;

           options.User.RequireUniqueEmail = true;
       })
        .AddEntityFrameworkStores<LibraryContext>();
```
5. In the **Startup.cs** code window, locate the following code:
  ```cs
       app.UseStaticFiles();
```

6. Place the cursor at the end of the located code, press Enter twice, and then type the following code:
  ```cs
       app.UseAuthentication();
```

#### Task 3: Add sign in logic

1. In the **Library - Microsoft Visual Studio** window, in Solution Explorer, right-click **Controllers**, point to **Add**, and then click **Controller**.

2. In the **Add Scaffold** dialog box, click **MVC Controller - Empty**, and then click **Add**.

3. In the **Add Empty MVC Controller** dialog box, in the **Controller name** box, type **AccountController**, and then click **Add**.

4. In the **AccountController.cs** code window, locate the following code:
  ```cs
       using Microsoft.AspNetCore.Mvc;
```
5. Ensure that the cursor is at the end of the **Microsoft.AspNetCore.Mvc** namespace, press Enter, and then type the following code:
  ```cs
       using Library.Models;
       using Library.ViewModels;
       using Microsoft.AspNetCore.Identity;
```
6. In the **AccountController.cs** code window, select the following code:
  ```cs
       public IActionResult Index()
       {
          return View();
       }
```

7. Replace the selected code with the following code:
  ```cs
       private SignInManager<User> _signInManager;
       private UserManager<User> _userManager;

       public AccountController(SignInManager<User> signInManager, UserManager<User> userManager)
       {
           _signInManager = signInManager;
           _userManager = userManager;
       }
```

8. Ensure that the cursor is at the end of the **AccountController** constructor code block, press Enter twice, and then type the following code:
  ```cs
       public IActionResult Login()
       {
           if (this.User.Identity.IsAuthenticated)
           {
               return RedirectToAction("Index", "Library");
           }
           return View();
       }
```

9. In the **AccountController.cs** code window, ensure that the cursor is at the end of the **Login** action code block, press Enter twice, and then type the following code:
  ```cs
       [HttpPost, ActionName("Login")]
       public async Task<IActionResult> LoginPost(LoginViewModel loginModel)
       {
           if (ModelState.IsValid)
           {
               var result = await _signInManager.PasswordSignInAsync(loginModel.UserName, loginModel.Password, loginModel.RememberMe, false);
               if (result.Succeeded)
               {
                   return RedirectToAction("Index", "Library");
               }
           }
           ModelState.AddModelError("", "Faild to Login");
           return View();
       }
```

10. In the **AccountController.cs** code window, ensure that the cursor is at the end of the **LoginPost** action code block, press Enter twice, and then type the following code:
  ```cs
       public async Task<IActionResult> Logout()
       {
           await _signInManager.SignOutAsync();
           return RedirectToAction("Index", "Library");
       }
```

#### Task 4: Add user registration logic

1. In the **AccountController.cs** code window, ensure that the cursor is at the end of the **Logout** action code block, press Enter twice, and then type the following code:
  ```cs
       public IActionResult Register()
       {
           return View();
       }
```

2. In the **AccountController.cs** code window, ensure that the cursor is at the end of the **Register** action code block, press Enter twice, and then type the following code:
  ```cs
       [HttpPost, ActionName("Register")]
       public async Task<IActionResult> RegisterPost(RegisterViewModel registerModel)
       {
           if (ModelState.IsValid)
           {
               User user = new User
               {
                   FirstName = registerModel.FirstName,
                   LastName = registerModel.LastName,
                   UserName = registerModel.UserName,
                   PhoneNumber = registerModel.PhoneNumber,
                   Email = registerModel.Email
               };

               var result = await _userManager.CreateAsync(user, registerModel.Password);
               if (result.Succeeded)
               {
                   var resultSignIn = await _signInManager.PasswordSignInAsync(registerModel.UserName, registerModel.Password,registerModel.RememberMe,false);
                   if (resultSignIn.Succeeded)
                   {
                       return RedirectToAction("Index", "Library");
                   }
               }
               foreach (var error in result.Errors)
               {
                   ModelState.AddModelError("", error.Description);
               }
           }
           return View();
       }
```

3. In the **AccountController.cs** code window, ensure that the cursor is at the end of the **RegisterPost** action code block, press Enter twice, and then type the following code:
  ```cs
       public IActionResult AccessDenied()
       {
           return View();
       }
```

#### Task 5: Retrieve data from the Identity property

1.  In the **Library - Microsoft Visual Studio** window, in Solution Explorer, expand **Views**, expand **Library**, and then click **LendingBook.cshtml**.

2. In the **LendingBook.cshtml** code window, locate the following code:
  ```cs
       @{
           ViewData["Title"] = "LendingBook";
       }
```
3. Place the cursor at the end of the located code, press Enter twice, and then type the following code:
  ```cs
       <h1 class="title">Hello @User.Identity.Name - Lending Book Information</h1>
```
4. In the **Library - Microsoft Visual Studio** window, in Solution Explorer, under **Views**, expand **Shared**, and then click **_Layout.cshtml**.

5. In the **_Layout.cshtml** code window, locate the following code:
  ```cs
       <li class="nav-item">
           <a class="nav-link" href="@Url.Action("GetBooksByGener", "Library")">Our Books</a>
       </li>
```
6. Place the cursor at the end of the located code, press Enter twice, and then type the following code:
  ```cs
       @if (User.IsInRole("Administrator"))
       {
           <li class="nav-item">
               <a class="nav-link" href="@Url.Action("Index", "Librarian")">Workers Portal</a>
           </li>
       }
       @if (User.Identity.IsAuthenticated)
       {
           <li class="nav-item">
               <a class="nav-link" href="@Url.Action("Logout", "Account")">Logout</a>
           </li>
       }
       else
       {
           <li class="nav-item">
               <a class="nav-link" href="@Url.Action("Login", "Account")">Login</a>
           </li>
       }
```

#### Task 6: Run the application

1. In the **Library - Microsoft Visual Studio** window, on the **FILE** menu, click **Save All**.

2. In the **Library - Microsoft Visual Studio** window, on the **DEBUG** menu, click **Start Without Debugging**.

3. In the menu bar, click **Our Books**.

    >**Note**: The **Our Books** page is only for authorized users; therefore, you redirected to the login page.

4. On the **Login** page, click **Register**.

5. On the **Register** page, in the **First Name** box, type _&lt;A first name of your choice&gt;._

6. On the **Register** page, in the **Last Name** box, type _&lt;A last name of your choice&gt;._

7. On the **Register** page, in the **Phone Number** box, type _&lt;A phone number of your choice&gt;._

8. On the **Register** page, in the **Email** box, type _&lt;An email address of your choice&gt;._

9. On the **Register** page, in the **User Name** box, type _&lt;A user name of your choice&gt;._

10. On the **Register** page, in the **Password** box, type **123qwe!@#QWE**, and then click **Register**.

11. In the menu bar, click **Our Books**.

      >**Note**: Examine the page; you have been authorized to enter the **Our Books** page, and your user name data has been retrieved from the Identity property.

12. On the **Our Books** page, select a book of your choice, and then click **Lend a Book**.

13. Click **Lend a Book**.

      >**Note**: The book you lent is not available anymore.

14.  In Microsoft Edge, click **Close**.


>**Results**: After completing this exercise, you will be able to configure identity in the application, add logic to the sign in and register pages, and retrieve data from identity.


### Exercise 2: Add Authorization

#### Task 1: Add AuthorizeAttribute to an action

1. In the **Library - Microsoft Visual Studio** window, in Solution Explorer, expand **Controllers**, and then click **LibraryController.cs**.

2. In the **LibraryController.cs** code window, locate the following code:
  ```cs
      using Microsoft.AspNetCore.Mvc;
```
3. Ensure that the cursor is at the end of the **Microsoft.AspNetCore.Mvc** namespace, press Enter, and then type the following code:
  ```cs
      using Microsoft.AspNetCore.Authorization;
```
4. In the **Index** action code block, locate the following code:
  ```cs
       public IActionResult Index()
```
5. Place the cursor before the located code, press the up arrow key, and then type the following code:
  ```cs
       [AllowAnonymous]
```  

6. In the **GetBooksByGener** action code block, locate the following code:
  ```cs
       public IActionResult GetBooksByGener()
```

7. Place the cursor before the located code, press the up arrow key, and then type the following code:
  ```cs
       [Authorize]
```  

8. In the **GetBooksByGener** action code block, select the following code:
  ```cs
       if (this.User.Identity.IsAuthenticated)
       {
           var booksGenerQuery = from b in _context.Books
                                 orderby b.Genre.Name
                                 select b;

           return View(booksGenerQuery);
       }
       return RedirectToAction("Login", "Account");
```

9. Replace the selected code with the following code:
  ```cs
       var booksGenerQuery = from b in _context.Books
                             orderby b.Genre.Name
                             select b;

       return View(booksGenerQuery);
```

10. In the **LendingBookPost** action code block, locate the following code:
  ```cs
       public async Task<IActionResult> LendingBookPost(int id)
```

11. Place the cursor before the located code, press the up arrow key, and then type the following code:
  ```cs
       [Authorize]
``` 
#### Task 2: Add role-based policy authentication

1. In the **Library - Microsoft Visual Studio** window, in Solution Explorer, expand **ViewModels**, and then click **RegisterViewModel.cs**.

2. In the **RegisterViewModel.cs** code window, locate the following code:
  ```cs
       [Display(Name = "Last Name")]
       [Required(ErrorMessage = "Please enter your last name")]
       public string LastName { get; set; }
```

3. Place the cursor at the end of the located code, press Enter twice, and then type the following code:
  ```cs
       [Display(Name = "Role Name")]
       [Required(ErrorMessage = "Please select a role")]
       public string RoleName { get; set; }
```

4. In the **Library - Microsoft Visual Studio** window, in Solution Explorer, under **Controllers**, click **AccountController.cs**.

5. In the **AccountController.cs** code window, select the following code:
  ```cs
       private SignInManager<User> _signInManager;
       private UserManager<User> _userManager;

       public AccountController(SignInManager<User> signInManager, UserManager<User> userManager)
       {
           _signInManager = signInManager;
           _userManager = userManager;
       }
```

6. Replace the selected code with the following code:
  ```cs
       private SignInManager<User> _signInManager;
       private UserManager<User> _userManager;
       private RoleManager<IdentityRole> _roleManager;

       public AccountController(SignInManager<User> signInManager, UserManager<User> userManager, RoleManager<IdentityRole> roleManager)
       {
           _signInManager = signInManager;
           _userManager = userManager;
           _roleManager = roleManager;
       }
```

7. In the **AccountController.cs** code window, in the **RegisterPost** action code block, select the following code:
  ```cs
       var result = await _userManager.CreateAsync(user, registerModel.Password);
       if (result.Succeeded)
       {
           var resultSignIn = await _signInManager.PasswordSignInAsync(registerModel.UserName, registerModel.Password, registerModel.RememberMe, false);
           if (resultSignIn.Succeeded)
           {
               return RedirectToAction("Index", "Library");
           }
       }
```

8. Replace the selected code with the following code:
  ```cs
        var result = await _userManager.CreateAsync(user, registerModel.Password);
        if (result.Succeeded)
        {
            bool roleExists = await _roleManager.RoleExistsAsync(registerModel.RoleName);
            if (!roleExists)
            {
                await _roleManager.CreateAsync(new IdentityRole(registerModel.RoleName));
            }

            if (!await _userManager.IsInRoleAsync(user, registerModel.RoleName))
            {
                await _userManager.AddToRoleAsync(user, registerModel.RoleName);
            }

            var resultSignIn = await _signInManager.PasswordSignInAsync(registerModel.UserName, registerModel.Password,registerModel.RememberMe,false);
            if (resultSignIn.Succeeded)
            {
                return RedirectToAction("Index", "Library");
            }
        }
```

9. In the **Library - Microsoft Visual Studio** window, in Solution Explorer, under **Views**, expand **Account**, and then click **Register.cshtml**.

10. In the **Register.cshtml** code window, locate the following code:
  ```cs
       <div class="form-group row">
           <label asp-for="Password" class="col-sm-4 col-form-label"></label>
           <div class="col-sm-6">
               <input asp-for="Password" type="password" class="form-control" placeholder="Password" required>
               <span asp-validation-for="Password"></span>
           </div>
       </div>
```
11. Place the cursor at the end of the located code, press Enter, and then type the following code:
  ```cs
       <div class="form-group row">
           <label asp-for="RoleName" class="col-sm-4 col-form-label"></label>
           <div class="col-sm-6">
               <select asp-for="RoleName" class="form-control">
                   <option selected>Member</option>
                   <option>Administrator</option>
               </select>
           </div>
       </div>
```

12. In the **Library - Microsoft Visual Studio** window, in Solution Explorer, under **Controllers**, click **LibrarianController.cs**.

13. In the **LibrarianController.cs** code window, locate the following code:
  ```cs
      using Microsoft.AspNetCore.Mvc;
```

14. Ensure that the cursor is at the end of the **Microsoft.AspNetCore.Mvc** namespace, press Enter, and then type the following code:
  ```cs
      using Microsoft.AspNetCore.Authorization;
```

15. In the **LibrarianController.cs** code window, locate the following code:
  ```cs
       public class LibrarianController : Controller
```

16. Place the cursor before the located code, press the up arrow key, and then type the following code:
  ```cs
       [Authorize(Roles = "Administrator")]
``` 

#### Task 3: Add claim-based policy authentication

1. In the **Library - Microsoft Visual Studio** window, in Solution Explorer, click **Startup.cs**.

2. In the **Startup.cs** code window, locate the following code:
  ```cs
      using Microsoft.Extensions.DependencyInjection;
```

3. Ensure that the cursor is at the end of the **Microsoft.Extensions.DependencyInjection** namespace, press Enter, and then type the following code:
  ```cs
      using System.Security.Claims;
```

4. In the **Startup.cs** code window, locate the following code:
  ```cs
       services.AddMvc();
```

5. Place the cursor at the end of the located code, press Enter twice, and then type the following code:
  ```cs
       services.AddAuthorization(options =>
       {
           options.AddPolicy("RequireEmail", policy => policy.RequireClaim(ClaimTypes.Email));
       });
```

6. In the **Library - Microsoft Visual Studio** window, in Solution Explorer, under **Controllers**, click **AccountController.cs**.

7. In the **AccountController.cs** code window, locate the following code:
  ```cs
      using Microsoft.AspNetCore.Identity;
```

8. Ensure that the cursor is at the end of the **Microsoft.AspNetCore.Identity** namespace, press Enter, and then type the following code:
  ```cs
      using System.Security.Claims;
```

9. In the **AccountController.cs** code window, in the **RegisterPost** action code block, select the following code:
  ```cs
       var result = await _userManager.CreateAsync(user, registerModel.Password);
        if (result.Succeeded)
        {
            bool roleExists = await _roleManager.RoleExistsAsync(registerModel.RoleName);
            if (!roleExists)
            {
                await _roleManager.CreateAsync(new IdentityRole(registerModel.RoleName));
            }

            if (!await _userManager.IsInRoleAsync(user, registerModel.RoleName))
            {
                await _userManager.AddToRoleAsync(user, registerModel.RoleName);
            }

            var resultSignIn = await _signInManager.PasswordSignInAsync(registerModel.UserName, registerModel.Password,registerModel.RememberMe,false);
            if (resultSignIn.Succeeded)
            {
                return RedirectToAction("Index", "Library");
            }
        }
```

10. Replace the selected code with the following code:
  ```cs
        var result = await _userManager.CreateAsync(user, registerModel.Password);
        if (result.Succeeded)
        {
            bool roleExists = await _roleManager.RoleExistsAsync(registerModel.RoleName);
            if (!roleExists)
            {
                await _roleManager.CreateAsync(new IdentityRole(registerModel.RoleName));
            }

            if (!await _userManager.IsInRoleAsync(user, registerModel.RoleName))
            {
                await _userManager.AddToRoleAsync(user, registerModel.RoleName);
            }

            if (!string.IsNullOrWhiteSpace(user.Email))
            {
                Claim claim = new Claim(ClaimTypes.Email, user.Email);
                await _userManager.AddClaimAsync(user, claim);
            }

            var resultSignIn = await _signInManager.PasswordSignInAsync(registerModel.UserName, registerModel.Password,registerModel.RememberMe,false);
            if (resultSignIn.Succeeded)
            {
                return RedirectToAction("Index", "Library");
            }
        }
```
11. In the **Library - Microsoft Visual Studio** window, in Solution Explorer, under **Controllers**, click **LibrarianController.cs**.

12. In the **LibrarianController.cs** code window, locate the following code:
  ```cs
       [Authorize(Roles = "Administrator")]
```

13. Place the cursor before the located code, press the up arrow key, and then type the following code:
  ```cs
       [Authorize(Policy = "RequireEmail")]
``` 

#### Task 4: Run the application

1. In the **Library - Microsoft Visual Studio** window, on the **FILE** menu, click **Save All**.

2. In the **Library - Microsoft Visual Studio** window, on the **DEBUG** menu, click **Start Without Debugging**.

3. In the menu bar, click **Login**.

4. On the **Login** page, click **Register**.

5. On the **Register** page, in the **First Name** box, type _&lt;A first name of your choice&gt;._

6. On the **Register** page, in the **Last Name** box, type _&lt;A last name of your choice&gt;._

7. On the **Register** page, in the **Phone Number** box, type _&lt;A phone number of your choice&gt;._

8. On the **Register** page, in the **Email** box, type _&lt;An email address of your choice&gt;._

9. On the **Register** page, in the **User Name** box, type _&lt;A user name of your choice&gt;._

10. On the **Register** page, in the **Password** box, type **123qwe!@#QWE**.

11. On the **Register** page, in the **Role Name** list, select **Administrator**, and then click **Register**.

12. In the menu bar, click **Workers Portal**.

      >**Note**: Examine the page; you have been authorized to enter the **Workers Portal** page, because you are an administrator.

13. On the **Add Book to Library** page, click **Add Book to the Library**.

14. On the **Add Book to Library** page, in the **Genre** list, select _&lt;A genre of your choice&gt;._

15. On the **Add Book to Library** page, in the **Name** box, type _&lt;A name of your choice&gt;._

16. On the **Add Book to Library** page, in the **Author** box, type _&lt;An author of your choice&gt;._

17. On the **Add Book to Library** page, in the **Date Published** box, type _&lt;a publishing date of your choice&gt;._

18. On the **Add Book to Library** page, in the **Photo** box, import an image from **[Repository Root]\Allfiles\Mod09\Labfiles\Image\book.jpg**, and then click **Add a Book**.

19. Click **Back to Our Books**.

      >**Note**: The book you added is in the library books list.

20. In the menu bar, click **Logout**.

21. In the menu bar, click **Login**.

22. On the **Login** page, click **Register**.

23. On the **Register** page, in the **First Name** box, type _&lt;A first name of your choice&gt;._

24. On the **Register** page, in the **Last Name** box, type _&lt;A last name of your choice&gt;._

25. On the **Register** page, in the **Phone Number** box, type _&lt;A phone number of your choice&gt;._

26. On the **Register** page, in the **Email** box, type _&lt;An email address of your choice&gt;._

27. On the **Register** page, in the **User Name** box, type _&lt;A user name of your choice&gt;._

28. On the **Register** page, in the **Password** box, type **123qwe!@#QWE**.

29. On the **Register** page, in the **Role Name** list, select **Member**, and then click **Register**.

30. In Microsoft Edge, in the address bar, type **http://localhost:[port]/Librarian/Index**, and then press Enter.

      >**Note**: You are redirected to the **access denied** page; only administrators are allowed to view the page. Also note that the menu bar doesn't have a navigation tab for **Workers Portal**.

31.  In Microsoft Edge, click **Close**.

>**Results**: After completing this exercise, you will be able to add authorization in the application, and add configuration and the relevant attribute for role-based and claim based policy authentication.

### Exercise 3: Avoid the Cross-Site Request Forgery Attack

#### Task 1: Write the Cross-Site Request Forgery attack

1. In Solution Explorer, right-click **CrossSiteRequestForgeryAttack**, point to **Add**, and then click **New Folder**.

2. In the **NewFolder** box, type **Controllers**, and then press Enter.

3. In the **Library - Microsoft Visual Studio** window, in Solution Explorer, in the **CrossSiteRequestForgeryAttack** project, right-click the **Controllers** folder, point to **Add**, and then click **Controller**.

4. In the **Add Scaffold** dialog box, click **MVC Controller - Empty**, and then click **Add**.

5. In the **Add Empty MVC Controller** dialog box, in the **Controller name** box, type **HomeController**, and then click **Add**.

6. In the **HomeController.cs** code window, right-click the following code, and then click **Add View**.
```cs
    public IActionResult Index()
```

7. In the **Add MVC View** dialog box, ensure that the value in the **View name** box is **Index**.

8. In the **Add MVC View** dialog box, ensure that **Empty (without model)** template is selected.

9. In the **Add MVC View** dialog box, ensure that the **Create as a partial view** and **Use a layout page** check boxes are cleared, and then click **Add**.

10. In the **Index.cshtml** code window, locate the following code:
```cs
    <title>Index</title>
```

11. Place the cursor at the end of the located code, press Enter, and then type the following code:
```cs
    <link href="~/css/style.css" rel="stylesheet" />
```

12. In the **Index.cshtml** code window, in the **BODY** element, type the following code:
```cs
    <h1>Cross-Site Request Forgery Attack</h1>
    <h3>Click - Submit to Perform the Attack</h3>
    <form action="http://localhost:[port]/Account/Register?FirstName=Forgery_Attacker&LastName=Cross_Site&PhoneNumber=123&Email=attack@@.com&UserName=Forgery_Attacker&Password=123qwe!!!QWE123&RoleName=Member" method="post">
        <input type="submit" value="Attack">
    </form>
```

#### Task 2: Run the application – Now the attack is possible

1. In the **Library - Microsoft Visual Studio** window, on the **FILE** menu, click **Save All**.

2. In Solution Explorer, right-click **Library**, and then click **Set as StartUp Project**. 

3. In the **Library - Microsoft Visual Studio** window, on the **DEBUG** menu, click **Start Without Debugging**.

      >**Note**: The menu bar has a navigation tab for **Login** meaning you are not logged in.

4. In Solution Explorer, right-click **CrossSiteRequestForgeryAttack**, point to **Debug**, and then click **Start new instance**.

5. On the **Cross-Site Request Forgery Attack** page, click **Attack**.

      >**Note**: The menu bar has a navigation tab for **Logout** meaning you are logged in.

6.  In Microsoft Edge, click **Close**.

    >**Note**: If the **Do you want to close all tabs?** dialog box appears, click **Close all**.

7. On the **Library(Running) - Microsoft Visual Studio** window, on the Debug menu, click **Stop Debugging**. 

#### Task 3: Avoid the Cross-Site Request Forgery attack

1. In the **Library - Microsoft Visual Studio** window, in Solution Explorer, under **Controllers**, click **AccountController.cs**.

2. In the **RegisterPost** action code block, locate the following code:
  ```cs
       public async Task<IActionResult> RegisterPost(RegisterViewModel registerModel)
```
3. Place the cursor before the located code, press the up arrow key, and then type the following code:
  ```cs
       [ValidateAntiForgeryToken]
``` 
4. In the **Library - Microsoft Visual Studio** window, in Solution Explorer, under **Controllers**, click **LibrarianController.cs**.

5. In the **AddBookPost** action code block, locate the following code:
  ```cs
       public IActionResult AddBookPost(Book book)
```
6. Place the cursor before the located code, press the up arrow key, and then type the following code:
  ```cs
       [ValidateAntiForgeryToken]
``` 
7. In the **Library - Microsoft Visual Studio** window, in Solution Explorer, under **Controllers**, click **LibraryController.cs**.

8. In the **LendingBookPost** action code block, locate the following code:
  ```cs
       public async Task<IActionResult> LendingBookPost(int id)
```
9. Place the cursor before the located code, press the up arrow key, and then type the following code:
  ```cs
       [ValidateAntiForgeryToken]
``` 

#### Task 4: Run the application – Now the attack is not possible

1. In the **Library - Microsoft Visual Studio** window, on the **FILE** menu, click **Save All**.

2. In Solution Explorer, right-click **Library**, and then click **Set as StartUp Project**. 

3. In the **Library - Microsoft Visual Studio** window, on the **DEBUG** menu, click **Start Without Debugging**.

      >**Note**: The menu bar has a navigation tab for **Login**, meaning that you are not logged in.

5. In Solution Explorer, right-click **CrossSiteRequestForgeryAttack**, point to **Debug**, and then click **Start new instance**.

6. On the **Cross-Site Request Forgery Attack** page, click **Attack**.

      >**Note**: An HTTP 400 error is thrown.

7.  In Microsoft Edge, click **Close**.

    >**Note**: If the **Do you want to close all tabs?** dialog box appears, click **Close all**.

8. On the **Library(Running) - Microsoft Visual Studio** window, on the Debug menu, click **Stop Debugging**. 

9. In the **Library - Microsoft Visual Studio** window, on the **FILE** menu, click **Exit**.

>**Results**: After completing this exercise, you will be able to avoid cross-site request forgery attack.

©2018 Microsoft Corporation. All rights reserved.

The text in this document is available under the [Creative Commons Attribution 3.0 License](https://creativecommons.org/licenses/by/3.0/legalcode), additional terms may apply. All other content contained in this document (including, without limitation, trademarks, logos, images, etc.) are  **not**  included within the Creative Commons license grant. This document does not provide you with any legal rights to any intellectual property in any Microsoft product. You may copy and use this document for your internal, reference purposes.

This document is provided &quot;as-is.&quot; Information and views expressed in this document, including URL and other Internet Web site references, may change without notice. You bear the risk of using it. Some examples are for illustration only and are fictitious. No real association is intended or inferred. Microsoft makes no warranties, express or implied, with respect to the information provided here.
