## SeleniumVBA v1.3

A comprehensive Selenium wrapper for Edge and Chrome written in Windows Excel VBA.

Modified/extended from [TinySeleniumVBA](https://github.com/uezo/TinySeleniumVBA/)

## Features

- Edge and Chrome browser support
- Wrappers for most of Selenium's JSon Wire Protocol
- Support for HTML DOM, Action Chains, SendKeys, Shadow Roots, Cookies, ExecuteScript, and Capabilities
- Automated Browser/WebDriver version alignment via WebDriverManager class (see [test_UpdateDriver.bas](https://github.com/GCuser99/SeleniumVBA/tree/main/test))
- Open spec: This wrapper is an HTTP client of the Selenium WebDriver server, conforming to [W3C standards](https://www.w3.org/TR/webdriver/).


## Setup

1. Import class and standard modules from this repository into into Excel VBA
2. Set the following VBA references:

<img src="https://github.com/GCuser99/SeleniumVBA/blob/main/src/references.png" width="300" height="200">`

3. Or alternatively... download the zipped Excel file [seleniumvba_v1.3.zip](https://github.com/GCuser99/SeleniumVBA/tree/main/dist/) - it's ready to go...
4. Download WebDrivers into same directory as the Excel file (each driver should be same major version as corresponding browser)
   
   Edge: https://developer.microsoft.com/en-us/microsoft-edge/tools/webdriver/
   
   Chrome: https://chromedriver.chromium.org/downloads

5. Or alternatively... let WebDriverManager class download and install drivers automatically (see [test_UpdateDriver.bas](https://github.com/GCuser99/SeleniumVBA/tree/main/test))

## SendKeys Example

```vb
Sub doSendKeys()
    Dim driver As New WebDriver
    Dim keys As New Keyboard
    
    driver.StartChrome
    driver.OpenBrowser
    
    driver.NavigateTo "https://www.google.com/"
    driver.Wait 1000
    
    keySeq = "This is COOKL!" & keys.LeftKey & keys.LeftKey & keys.LeftKey & keys.DeleteKey & keys.ReturnKey
    
    driver.FindElement(by.name, "q").SendKeys keySeq
    driver.Wait 2000
    
    driver.CloseBrowser
    driver.Shutdown
End Sub
```

## WebDriver/Browser Version Alignment

```vb
Sub updateEdgeDriver()
    'this checks for installed driver compatibility and then if not, installs updated driver
    Dim mngr As New WebDriverManager
    
    browserName = "msedge" 'or "chrome"
    driverPath = ".\msedgedriver.exe" 'or ".\chromedriver.exe"
    
    mngr.AlignDriverAndBrowser browserName, driverPath
    
    browserVer = mngr.GetInstalledBrowserVersion(browserName)
    driverVer = mngr.GetInstalledDriverVersion(browserName, driverPath)
    
    MsgBox "Edge " & "Webdriver and Browser are compatible!" & vbCrLf & vbCrLf & "Browser version: " & browserVer & vbCrLf & "Driver version:    " & driverVer, , "SeleniumVBA"
End Sub
```

## Action Chain Example
```vb
Sub doActionChain()
    Dim driver As New WebDriver
    Dim keys As New Keyboard
    Dim actions As ActionChain
    Dim elemSearch As WebElement
    
    driver.StartChrome
    driver.OpenBrowser
    
    driver.NavigateTo "https://www.google.com/"
    driver.Wait 1000
    
    Set elemSearch = driver.FindElement(by.name, "btnK")
    
    Set actions = driver.ActionChain
    
    'build the chain and then execute with Perform method
    actions.KeyDown(keys.ShiftKey).SendKeys("upper case").KeyUp(keys.ShiftKey)
    actions.MoveToElement(elemSearch).Click().Perform

    driver.Wait 2000
    
    driver.CloseBrowser
    driver.Shutdown
End Sub
```

## Credits

[TinySeleniumVBA](https://github.com/uezo/TinySeleniumVBA/) by Uezo and other contributors to that project

[VBA-JSON](https://github.com/VBA-tools/VBA-JSON) by Tim Hall, JSON converter for VBA
