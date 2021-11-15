# SSD1306
Modified SSD1306 driver from micropython

Added hardware horizontal scroll and a clear function

Heres a usage example:

    # runs under micropython version 1.17
    
    from machine import Pin, I2C
    import time
    import ssd1306

    def lcdInit():
        # I2C pins
        # I have 4k7 pull ups on scl and sda
        # set up I2C on gpio 14 and 16
        i2c = I2C(scl=Pin(16), sda=Pin(14), freq=100000)
        lcd = ssd1306.SSD1306_I2C(128, 32, i2c)            # lcd is 128x32
        return lcd

    def main():

        display = lcdInit()
        display.clear()

        while True:

            display.text("Hello World", 0, 0)
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
