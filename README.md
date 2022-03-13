# NotSoTinySeleniumVBA

A Selenium wrapper written in VBA based on JSon wire protocol.

Modified extensively from https://github.com/uezo/TinySeleniumVBA/

# ✨ Features

- No installation: Everyone even who doesn't have permissions to install can automate browser operations.
- Useful helper Methods: FindElement(s)By*, Get/Set value to form, click and more.
- Open spec: Basically this wrapper is just a HTTP client of WebDriver server. Learning this wrapper equals to learning WebDriver.
https://www.w3.org/TR/webdriver/


# 📦 Setup

1. Set reference to `Microsoft Scripting Runtime`

1. Add `WebDriver.cls`, `WebElement.cls` and `JsonConverter.bas` to your VBA Project
    - Latest (v0.1.1): https://github.com/uezo/TinySeleniumVBA/archive/v0.1.1.zip

1. Download WebDriver (driver and browser should be the same version)
    - Edge: https://developer.microsoft.com/ja-jp/microsoft-edge/tools/webdriver/
    - Chrome: https://chromedriver.chromium.org/downloads

# 🪄 Usage

```vb
Public Sub main()
    ' Start WebDriver (Edge)
    Dim Driver As New WebDriver
    Driver.Edge "path\to\msedgedriver.exe"
    
    ' Open browser
    Driver.OpenBrowser
    
    ' Navigate to Google
    Driver.Navigate "https://www.google.co.jp/?q=selenium"

    ' Get search textbox
    Dim searchInput
    Set searchInput = Driver.FindElement(By.Name, "q")
    
    ' Get value from textbox
    Debug.Print searchInput.GetValue
    
    ' Set value to textbox
    searchInput.SetValue "yomoda soba"
    
    ' Click search button
    Driver.FindElement(By.Name, "btnK").Click
    
    ' Refresh - you can use Execute with driver command even if the method is not provided
    Driver.Execute Driver.CMD_REFRESH
End Sub
```

# ❤️ Thanks

[VBA-JSON](https://github.com/VBA-tools/VBA-JSON) by Tim Hall, JSON converter for VBA helps me a lot to make HTTP client and this awesome library is included in the release under its license. Thank you!
