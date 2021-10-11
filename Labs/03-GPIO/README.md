# [DIGITAL ELECTRONICS <font size="5"> 2 </font>](https://github.com/jamo796/Digital-electronics-2/)
 
### Data types in C

1. Complete table.

| **Data type** | **Number of bits** | **Range** | **Description** |
| :-: | :-: | :-: | :-- | 
| `uint8_t`  | 8 | 0, 1, ..., 255 | Unsigned 8-bit integer |
| `int8_t`   | 8 | -128,127,...,126,127 | znaménkový 8-bitový INT první bit symbolizuje znaménko 1 = záporné ; 0 = kladné |
| `uint16_t` | 16 | 0  -  64 Ki | neznaménkový 16-bit INT |
| `int16_t`  | 16 | -32 Ki  -  32 Ki | znamenkový 16-bitový INT první bit symbolizuje znamnko |
| `float`    | 32 | -3.4e+38, ..., 3.4e+38 | Single-precision floating-point |
| `void`     | 0 | 0 | žádná hodnota |

Ki = 1024

64 Ki = 64 * 1024


### GPIO library


1. In your words, describe the difference between the declaration and the definition of the function in C.
   * Function declaration - H file tento dokument zakládá základní strukturu funkce jako paraetry se kterými bude fce pracovat její název atd. tyto data předává kompilátoru

   * Function definition - C file tento dokument přímo říká jak daná FCE vypadá jak zprcovává vstupy a co vrací na výstup

2. Part of the C code listing with syntax highlighting, which toggles LEDs only if push button is pressed. Otherwise, the value of the LEDs does not change. Use function from your GPIO library. Let the push button is connected to port D:

```c
    // Configure Push button at port D and enable internal pull-up resistor
    // WRITE YOUR CODE HERE

    GPIO_config_output(&DDRB, LED_TWO); //výstupní Ledka
    GPIO_write_low(&PORTB, LED_TWO);; //nastavení led diodu na hodnotu log.H
    GPIO_config_input_pullup(&DDRD, BUTON); //nastavujeme tlačítko na pord D 

    // Infinite loop
    while (1)
    {
        // Pause several milliseconds
        _delay_ms(BLINK_DELAY);

        // WRITE YOUR CODE HERE
        if(GPIO_read(&PIND, BUTON) == 0) 
        /* 
        jelikož je pull-up rezistor nám zajišťuje log.H proto musíme hledat log.L pro
        označení že je tlačítko sepnuté
        */
            {
                GPIO_toggle(&DDRB, LED_TWO)
            }
    }
```


### Traffic light

1. Scheme of traffic light application with one red/yellow/green light for cars and one red/green light for pedestrians. Connect AVR device, LEDs, resistors, one push button (for pedestrians), and supply voltage. The image can be drawn on a computer or by hand. Always name all components and their values!

   ![Trafic Lights](https://github.com/jamo796/Digital-electronics-2/blob/main/Labs/03-GPIO/trafic%20lights.png)
