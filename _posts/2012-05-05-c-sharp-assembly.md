---
id: 4
timestamp: 1336262413
author: "Matt Keller"
title: "Is there a way to view the assembly of a C# Program?"
excerpt: "Let's get down into the nitty gritty of IL and the .NET framework."
---

Following in the themes of [[2012-05-03-dot-net-framework|.NET]] and [[2012-05-04-dot-net-framework-2|.NET(redux)]] blog posts, let's dive deeper into C#, IL and the CLR

There is a tool in the Visual Studio called ildasm.exe. By opening the developer command prompt ildasm can be run on the output of building within the Visual Studio sdk.  
  
This shows the hierarchy of the objects and their member functions, and fields and data types.  
This is an image of the output of running ildasm on the C# version of hello world.


As you can see the structure of the program in shown including the namespace (ConsoleApplication1), the class (ConsoleApplication1.Program) and the functions(.ctor[constructor], Main)

In addition to being able to see this hierarchy, ildasm also allows the programmer to see the true IL code.

Above is the corresponding IL code for the hello world program that I wrote/copied. It is not particularly interesting code but it can be used to demonstrate an interesting property of IL. It uses a virtual stack of variables and calls functions on the top of the stack and returns the solution to the top of the stack. The ldstr instruction above represents the string "Hello World" being added to the stack.

**Resources:**
 - ildasm.exe Tutorial - http://msdn.microsoft.com/en-us/library/aa309387(v=vs.71).aspx