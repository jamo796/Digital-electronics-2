# [DIGITAL ELECTRONICS <font size="5"> 2 </font>](https://github.com/jamo796/Digital-electronics-2/)
 
Lab 7: Jan Pelka

Link to your Digital-electronics-2 GitHub repository:

https://github.com/jamo796/Digital-electronics-2/tree/main/Labs/07-UART

### Analog-to-Digital Conversion

1. Complete table with voltage divider, calculated, and measured ADC values for all five push buttons.

   | **Push button** | **PC0[A0] voltage** | **ADC value (calculated)** | **ADC value (measured)** |
   | :-: | :-: | :-: | :-: |
   | Right  | 0&nbsp;V | 0   | 1 |
   | Up     | 0.495&nbsp;V | 101 | 100  |
   | Down   | 1.2 V | 246 | 245 |
   | Left   | 1,97 V | 402 | 399 |
   | Select | 3,18 V | 651 | 656 |
   | none   |  5 V  | 1023 | 1022 |

2. Code listing of ACD interrupt service routine for sending data to the LCD/UART and identification of the pressed button. Always use syntax highlighting and meaningful comments:

```c
/**********************************************************************
 * Function: ADC complete interrupt
 * Purpose:  Display value on LCD and send it to UART.
 **********************************************************************/
ISR(ADC_vect)
{
    uint16_t value = 0;
    char lcd_string[4] = "0000";
    
    value = ADC;    


    lcd_gotoxy(8, 0);    
    lcd_puts("    ");
    
    lcd_gotoxy(13, 0);
    lcd_puts("   ");
    
    
    itoa(value, lcd_string, 10);
    lcd_gotoxy(8, 0);
    lcd_puts(lcd_string);
    
    itoa(value, lcd_string, 16);
    lcd_gotoxy(13, 0);
    lcd_puts(lcd_string); 
    

    uart_puts(lcd_string);
    uart_puts("    ");
        // B je na hodnotì 13

}
```

### UART communication

1. (Hand-drawn) picture of UART signal when transmitting three character data `De2` in 4800 7O2 mode (7 data bits, odd parity, 2 stop bits, 4800&nbsp;Bd).

   ![your figure]()

2. Flowchart figure for function `uint8_t get_parity(uint8_t data, uint8_t type)` which calculates a parity bit of input 8-bit `data` according to parameter `type`. The image can be drawn on a computer or by hand. Use clear descriptions of the individual steps of the algorithms.

   ![your figure]()

### Temperature meter

Consider an application for temperature measurement and display. Use temperature sensor [TC1046](http://ww1.microchip.com/downloads/en/DeviceDoc/21496C.pdf), LCD, one LED and a push button. After pressing the button, the temperature is measured, its value is displayed on the LCD and data is sent to the UART. When the temperature is too high, the LED will start blinking.

1. Scheme of temperature meter. The image can be drawn on a computer or by hand. Always name all components and their values.

   ![your figure]()