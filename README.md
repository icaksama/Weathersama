# Weathersama (Build on Swift 4, xCode 9.0)
Weathersama is library for access weather data on openweathermap.org.
You can find clone apple weather app in WeatersamaDemo project.

This is simple library with class model inside. You can make code short and faster. This library integrated with google geocode. So, its simple to find location and send that to get weather data.
<br><br>
<p align="center">
<img width="250" src="https://github.com/icaksama/Weathersama/blob/master/ss1.jpeg?raw=true">&nbsp;&nbsp;&nbsp;
<img width="250" src="https://github.com/icaksama/Weathersama/blob/master/ss2.jpeg?raw=true">&nbsp;&nbsp;&nbsp;
<img width="250" src="https://github.com/icaksama/Weathersama/blob/master/ss3.jpeg?raw=true">
</p>
<br>

# Add to Podfile
Add Weathersama library to your Podfile and install
```Swift
pod 'Weathersama', '~> 1.1.2'
```

# Install Demo Project
The demo project is a clone of apple weather app. The demo project have weather backgrounds moves like apple weather app. But, that is videos, not animations. Let's contribute to change them with animations.
```Swift
1. Download the project
2. Open WeathersamaDemo.xcworkspace
2. No need to change appId or googleKey
3. Library already uploaded on CocoaPods repository with version 1.1.2
3. Just change Bundle indentifier & Run
```

# Import Library
You need to import library before use the library in your class.
```Swift
import Weathersama
```

# Weathersama with Delegete
You can get date response from openweathermap.org with delegete.
```Swift
class ViewController: UIViewController, CardViewListDelegete {
    var weatherSama: Weathersama!
    override func viewDidLoad() {
        super.viewDidLoad()
        weatherSama = Weathersama(appId: "YOUR_APP_ID", temperature: TEMPERATURE_TYPES.Celcius, language: LANGUAGES.French, dataResponse: DATA_RESPONSE.JSON)
        weatherSama.delegete = self
        
        // You can set nil if use Weathersama library with delegete
        weatherSama.weatherByCityId(cityId: 12345, requestType: .dailyForecast, completion: nil)
    }
}
```

<b> And add the method delegete for response</b>
```Swift
public func didStartRequestResponder() {
    print("Request start!")
}

public func didEndRequestResponder(result: Bool, description: String, requestType: REQUEST_TYPE) {
    if result {
        if requestType == .dailyForecast {
            print("response json : \(description)")
        } else if requestType == .Forecast {
            print("response json : \(description)")
        } else if requestType == .Weather {
            print("response json : \(description)")
        }
    } else {
        print("response error: \(description)")
    }
}
```

# Weathersama with Completion Method
You can get the data response from openweathermap.org with class model and without delegete. This is very easy to use data with class model.
```Swift
class ViewController: UIViewController {
    fileprivate var weatherSama: Weathersama!
    fileprivate var dailyForecastModel: DailyForecastModel!
    override func viewDidLoad() {
        super.viewDidLoad()
        weatherSama = Weathersama(appId: "YOUR_APP_ID", temperature: TEMPERATURE_TYPES.Celcius, language: LANGUAGES.French, dataResponse: DATA_RESPONSE.JSON)
        
        weatherSama.weatherByCityId(cityId: 12345, requestType: .dailyForecast) { (isSuccess, description, classModel) -> () in
            if isSuccess {
                // you can user response json or class model
                print("response json : \(description)")
                self.dailyForecastModel = classModel as! DailyForecastModel
            } else {
                print("response error : \(description)")
            }
        }
    }
}
```

# List of Request Types
```Swift
public enum REQUEST_TYPE: String {
    case Weather = "weather"
    case Forecast = "forecast"
    case dailyForecast = "forecast/daily"
}
```

# List of Class Model
Every request type have different class model. So, you need to casting the classModel from response such as request type.
<b>Class model for request type Weather</b>
```Swift
let weatherModel: WeatherModel = WeatherModel()
```

<b>Class model for request type Forecast</b>
```Swift
let forecastModel: ForecastModel = ForecastModel()
```

<b>Class model for request type Daily Forecast</b>
```Swift
let dailyForecastModel: DailyForecastModel = DailyForecastModel()
```

# List of Temperature Types
```Swift
public enum TEMPERATURE_TYPES: String {
    case Kelvin = ""
    case Celcius = "&units=metric"
    case Fahrenheit = "&units=imperial"
}
```
# List of Languages Supported
```Swift
public enum LANGUAGES: String {
    case Ukrainian = "&lang=uk"
    case Italian = "&lang=it"
    case German = "&lang=de"
    case Portuguese = "&lang=pt"
    case English = "&lang=en"
    case Romanian = "&lang=ro"
    case Russian = "&lang=ru"
    case ChineseSimplified = "&lang=zh_cn"
    case Spanish = "&lang=es"
    case French = "&lang=fr"
    case Bulgarian = "&lang=bg"
    case Polish = "&lang=pl"
    case Turkish = "&lang=tr"
    case Catalan = "&lang=ca"
    case Croatian = "&lang=hr"
    case Finnish = "&lang=fi"
    case Dutch = "&lang=nl"
    case Swedish = "&lang=sv"
    case ChineseTraditional = "zh_tw"
}
```

# List of Response Types
```Swift
public enum DATA_RESPONSE: String {
    case JSON = ""
    case XML = "&mode=xml"
}
```

# MIT License

Copyright (c) 2017 Saiful Irham Wicaksana

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.


