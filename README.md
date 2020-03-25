# SwapChainPanelCursor

An example on how to change the default cursor in a SwapChainPanel


# Getting Started

The following applications are required to be installed:

* Visual Studio 2017 or 2019 with C++ Windows Universal App Development package installed

# Build and Run (C# example)

1. Open the csharp/SwapChainPanelCursor.sln with Visual Studio 2017 or 2019

1. Select the x64/x64 configuration

1. Double-click on the Package.appxmanifest file in the SwapChainPanelCursor project. 

	* Navigate to the Packaging tab
	
	* Click on Choose Certificate...
	
	* Click on Configure Certificate...
	
	* Select Create test certificate...
	
	* Click on OK (do not enter a password)

1. Make sure the SwapChainPanelCursor project is the Startup Project	

1. Run the SwapChainPanelCursor application. 

	* Move the mouse pointer over the SwapChainPanel. The cursor should change to an I-beam a cursor. 
	
The C# solution has 3 projects

* SwapChainPanelCursor: The C# UWP application

* DirectXPanels: A C++ WinRT Component containing the code for the SwapChainPanel

* CustomCursors: A Win32 Desktop DLL that builds and compiles the custom cursor resources

Note: The Configuration Manager in the Build menu was used to set CustomCursors to a Release build for All Platforms/Configurations

In order to use the CustomCursor resources, we need to add the compiled CustomCursor.res file to the C# SwapChainPanelCursor UWP project

* Right click on the SwapChainPanelCursor and select Unload Project

* Right click on the SwapChainPanelCursor and select Edit

* Add the following to the end of the first PropertyGroup 

```xml
    <Win32Resource>$(SolutionDir)CustomCursors\$(Platform)\Release\CustomCursors.res</Win32Resource>
```

* Right click on the SwapChainPanelCursor and select Reload Project

This will automate adding the compiles CustomResource file to the CSharp UWP app.

# Build and Run (C++ example)

1. Open the cpp/SwapChainPanelCursor.sln with Visual Studio 2017 or 2019

1. Select the x64/Debug configuration

1. Double-click on the Package.appxmanifest file in the SwapChainPanelCursor project. 

	* Navigate to the Packaging tab
	
	* Click on Choose Certificate...
	
	* Click on Configure Certificate...
	
	* Select Create test certificate...
	
	* Click on OK (do not enter a password)
	
1. Make sure the SwapChainPanelCursor project is the Startup Project	

1. Build the solution

1. Run the SwapChainPanelCursor application. 

	* Move the mouse pointer over the SwapChainPanel. The cursor should remain a hand cursor. 

	* Click on the Change Cursor button. The cursor should change to a cross hair over the window and the SwapChainPanel.

##  Comments

In the file DirectXPage.xaml.cpp, look at the SetCursor() function. You will see that we need to change the cursor for both the CoreWindow and the SwapChainPanel.

```c++
void SwapChainPanelCursor::DirectXPage::SetCursor(Windows::UI::Core::CoreCursor^ cursor)
{
    m_currentCursor = cursor;
    CoreWindow::GetForCurrentThread()->PointerCursor = m_currentCursor;
    m_coreInput->Dispatcher->RunAsync(CoreDispatcherPriority::Normal, ref new DispatchedHandler([this]() {
        m_coreInput->PointerCursor = m_currentCursor;
    }));
}
```

Look at the page's constructor for how to set up the required CoreIndependentInputSource that is needed to set the cursor for the SwapChainPanel.

##  Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.microsoft.com.

When you submit a pull request, a CLA-bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., label, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.


## Reporting Security Issues

Security issues and bugs should be reported privately, via email, to the Microsoft Security
Response Center (MSRC) at [secure@microsoft.com](mailto:secure@microsoft.com). You should
receive a response within 24 hours. If for some reason you do not, please follow up via
email to ensure we received your original message. Further information, including the
[MSRC PGP](https://technet.microsoft.com/en-us/security/dn606155) key, can be found in
the [Security TechCenter](https://technet.microsoft.com/en-us/security/default).
