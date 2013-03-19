---
title: Create Fiddler Extension project
slug: CreateExtension
tags: Extend Fiddler, .NET, Extension, Interfaces, modify request string
publish: true
ordinal: 3
---

Create Fiddler Extension Project
================================

Follow these steps to create a sample Fiddler Extension that modifies the User-Agent string of all outbound requests:

Add Reference to Fiddler
------------------------

1. Start **Visual Studio 2005** or later.

2. Create a new Project of type **Visual C# Class Library**.

3. Right-click the project's **References** folder in the **Solution Explorer**.

4. Click the **Browse** tab and select **Fiddler.exe** in the **C:\Program Files\Fiddler2** folder. 

5. Click **Ok** to add the reference.

Add Reference to System.Windows.Forms
-------------------------------------

If your extension modifies Fiddler's UI:

1. Right-click the project's **References** folder in the **Solution Explorer** again.

2. On the **.NET** tab, choose **System.Windows.Forms**.

3. Click **Ok** to add the reference.

Add Build Event
---------------

1. In the **Solution Explorer**, right click the project. 

2. Click **Properties**.

3. Click the **Build Events** tab. 

4. Add the following to the **Post-build event command line**:

		copy "$(TargetPath)" "%userprofile%\My Documents\Fiddler2\Scripts\$(TargetFilename)"

Implement a [Fiddler Interface][2]
----------------------------------

Modify the default **class1.cs** (or create a new class) in your project as follows:

		using System;
		using System.Windows.Forms;
		using Fiddler;

		[assembly: Fiddler.RequiredVersion("2.3.5.0")]

		public class Violin : IAutoTamper    // Ensure class is public, or Fiddler won't see it!
		{
		  string sUserAgent = "";

		  public Violin(){
		  /* NOTE: It's possible that Fiddler UI isn't fully loaded yet, so don't add any UI in the constructor.

			 But it's also possible that AutoTamper* methods are called before OnLoad (below), so be
			 sure any needed data structures are initialized to safe values here in this constructor */
    
			 sUserAgent = "Violin";
		  }

		  public void OnLoad(){ /* Load your UI here */ }
		  public void OnBeforeUnload() { }

		  public void AutoTamperRequestBefore(Session oSession){
			oSession.oRequest["User-Agent"] = sUserAgent;
		  }
		  public void AutoTamperRequestAfter(Session oSession){}
		  public void AutoTamperResponseBefore(Session oSession){}
		  public void AutoTamperResponseAfter(Session oSession){}
		  public void OnBeforeReturningError(Session oSession){}
		}

Load Extension in Fiddler
-------------------------

1. Compile your project.

2. Copy the assembly .DLL to the correct **Scripts** folder:

 + Use **\My Documents\Fiddler2\Scripts** to make the extension available to the current user.
 + Use **\Program Files\Fiddler2\Scripts** to make the extension available to all users on the machine.

3. Restart Fiddler.

[1]: ./Interfaces.md