# u235-astrolib

A useful node/browser library for astrophotographers and astronomers.

Modules:
- **lrgb-exposure-calculator** helps you create full color images using your monochrome camera and filters. You begin by specifying the desired integration time of the luminance filter. In response it calculates the integration time of each color filter so as to balance the signal-to-noise ratio over all channels. Optionally, you can select the amount of hardware binning, and the color balance ratios for your particular camera and filters. Click [here](https://u235.herokuapp.com/lrgb-exposure-calculator.html) to visit a working calculator and a discussion of the theory of operation.

Install via

- `npm install u235-astrolib`
- `yarn add u235-astrolib`

Differences between major version 1 and 2:
- The browser namespace was changed from `u235Astrolib` to `U235Astrolib`.
- The name of the exported function was changed from `lrgbExposureCalculator` to `LrgbExposureCalculator`.
- The `create()` instance method was replaced by the constructor function `LrgbExposureCalculator`.

## Basic Examples
##### Node Example
```javascript
var Calc = require('u235-astrolib/lrgb-exposure-calculator');
var calc = new Calc();
```
##### Browser Example
```html
<script src="node_modules/u235-astrolib/lrgb-exposure-calculator/src/lrgb-exposure-calculator.js"></script>
<script>
  var Calc = u235Astrolib.LrgbExposureCalculator;
  var calc = new Calc();
</script>
```

### Examples cont.

##### Calculate RGB exposures given 60s luminance exposure, 2x2 binning, and custom color balance for a given camera and filters:
```javascript
var Calc = require('u235-astrolib/lrgb-exposure-calculator');
var calc = new Calc();
calc.rgbBinning = 2;
calc.redBalance = 1.62;
calc.greenBalance = 1;
calc.blueBalance = 1.34;
calc.luminanceExposure = 60;
console.log(calc.redExposure);    // 72.9
console.log(calc.greenExposure);  // 45
console.log(calc.blueExposure);   // 60.3
```

##### Calculate RGB exposures and frame counts given 60s luminance exposure and 40 frames:
```javascript
var { LrgbExposureCalculator } = require('u235-astrolib');
var calc = new LrgbExposureCalculator();
calc.rgbBinning = 2;
calc.redBalance = 1.62;
calc.greenBalance = 1;
calc.blueBalance = 1.34;
calc.luminanceExposure = 60;
calc.luminanceFrameCount = 40;
console.log(calc.redExposure);      // 72.9
console.log(calc.greenExposure);    // 45
console.log(calc.blueExposure);     // 60.3
console.log(calc.redFrameCount);    // 40
console.log(calc.greenFraneCount);  // 40
console.log(calc.blueFrameCount);   // 40
```

##### Calculate RGB frame counts given RGB exposures:
```javascript
var Calc = require('u235-astrolib/lrgb-exposure-calculator');
var calc = new Calc();
calc.commonFrameCountMode = false;
calc.rgbBinning = 2;
calc.redBalance = 1.62;
calc.greenBalance = 1;
calc.blueBalance = 1.34;
calc.luminanceExposure = 60;
calc.luminanceFrameCount = 40;
calc.redExposure = 55;
calc.greenExposure = 55;
calc.blueExposure = 55;
console.log(calc.redExposure);      // 55
console.log(calc.greenExposure);    // 55
console.log(calc.blueExposure);     // 55
console.log(calc.redFrameCount);    // 53.0
console.log(calc.greenFrameCount);  // 32.7
console.log(calc.blueFrameCount);   // 43.9
```

##### Subclass the calculator:
```javascript
var Calc = require('u235-astrolib/lrgb-exposure-calculator');
function MyCalc(name) {
  Calc.call(this);
  this._name = name;
}
var calc1 = new MyCalc("Bortle 5");
var calc2 = new MyCalc("Bortle 4");
```

## Instance Methods:
```javascript
number = calc.rgbBinning;           // getter
calc.rgbBinning = number;           // setter
number = calc.redBalance;           // getter
calc.redBalance = number;           // setter
number = calc.greenBalance;         // getter
calc.greenBalance = number;         // setter
number = calc.blueBalance;          // getter
calc.blueBalance = number;          // setter
number = calc.luminanceExposure;    // getter
calc.luminanceExposure = number;    // setter
number = calc.luminanceFrameCount;  // getter
calc.luminanceFrameCount = number;  // setter
bool = calc.commonFrameCountMode;   // getter
calc.commonFrameCountMode = bool;   // setter
number = calc.redFrameCount;        // getter
number = calc.greenFrameCount;      // getter
number = calc.blueFrameCount;       // getter
```

## License
The MIT License (MIT)

Copyright (c) 2019 Brian Morgan

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
