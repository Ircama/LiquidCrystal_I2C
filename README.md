# LiquidCrystal_I2C version 1.1.3

LiquidCrystal Arduino library supporting a dot matrix alphanumeric LCD (Liquid Crystal Display) driven by an Hitachi HD44780 controller (or other LCD compatible drivers) and with I2C backpack (e.g., through an NXP PCF8574). Typical LCD has 16x2 or 20x4 (chars)x(lines) and 5x8 or 5x10 dots per char.

LCD Compatible drivers with parallel input include the following:

- Samsung KS0073, KS0070S, KS0066, KS0066S
- Sanyo LC7985NA
- Epson SED1278
- OKI MSM6222
- Sitronix ST7066U
- NT8331
- Sunplus SPLC780

-------------------------------------------------------------------------------------------------------------------

# Installation
Create a new folder called "LiquidCrystal_I2C" under the folder named "libraries" in your Arduino sketchbook folder.
Create the folder "libraries" in case it does not exist yet. Place all the files in the "LiquidCrystal_I2C" folder.

# Usage
To use the library in your own sketch, select it from *Sketch > Import Library*.

# Description of the functions

Check https://www.arduino.cc/en/Reference/LiquidCrystal

# Usage of lcd.init()

This library supports `lcd.init()` and `lcd.begin()`.

`lcd.init()` performs the following steps:

- initialize I2C with default SDA and SCL (depending on the selected board);
- set the display to 4 bit, 1 line, 5x8 dots;
- run	lcd.begin() using the same rows and cols set in the object initialization

Since version 1.1.3, `lcd.init(SDA, SCL)` is also supported.

# Support of ESP8266
Version 1.1.2 already supports ESP8266 (warning message for non supported architecture shall be ignored).

The "Generic ESP8266 module" adopts the following:

    SDA=4
    SCL=5
    BUILTIN_LED=1
    LED_BUILTIN=1

Reference is here: https://github.com/esp8266/Arduino/blob/master/variants/generic/pins_arduino.h

After setting "Generic ESP8266 module", `lcd.init()` uses D4 for SDA and D5 for SCL.

Example:

    LiquidCrystal_I2C lcd(0x27,20,4);  // LCD2004 0x27 I2C address and columns by rows.
    lcd.init(); // Use D4 for SDA and D5 for SCL
    lcd.setCursor(3,0);
    lcd.print("Hello, world!");

As ESP-01 does not provide D4 and D5, SDA and SCL need to be changed. In order to do that, replace `lcd.init()` with `Wire.begin(SDA, SCL)`. Then use `lcd.begin(cols, rows)`.

Example:

    LiquidCrystal_I2C lcd(0x27,20,4);  // LCD2004 0x27 I2C address and columns by rows.
    Wire.begin(0 /* SDA */ ,2 /* SCL */ );
    lcd.begin(20, 4);
    lcd.setCursor(3,0);
    lcd.print("Hello, world!");

Since version 1.1.3, `lcd.init(SDA, SCL)` is also supported. Example:

    LiquidCrystal_I2C lcd(0x27,20,4);  // LCD2004 0x27 I2C address and columns by rows.
    lcd.init(0 /* SDA */ ,2 /* SCL */ );
    lcd.setCursor(3,0);
    lcd.print("Hello, world!");

Also, 1.1.3 removes the warning message when the architecture is different from *arm*.
