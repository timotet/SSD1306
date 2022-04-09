# SSD1306
Modified SSD1306 driver from micropython

Added hardware horizontal scroll and a clear function

Heres a usage example:

    # runs under micropython version 1.18
    # Tested using a cheap ESP32 module
    
    from machine import Pin, I2C
    import time
    import ssd1306

    def lcdInit():
        # set up default hardware I2C
        i2c = I2C(0)                                       # default hardware scl=Pin(18), sda=Pin(19)
        lcd = ssd1306.SSD1306_I2C(128, 32, i2c)            # my lcd is 128x32
        return lcd

    def main():

        display = lcdInit()
        display.clear()

        while True:

            display.text("Hello World", 0, 0, 1)
            display.show()
            
            # scroll right
            display.hw_scroll_h()

            time.sleep(3)

            # scroll left
            display.hw_scroll_h(False)

            time.sleep(3)

            display.hw_scroll_off()
            time.sleep(3)
            display.clear()
            time.sleep(1)
