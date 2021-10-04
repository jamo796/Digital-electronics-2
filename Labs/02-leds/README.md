# [DIGITAL ELECTRONICS <font size="5"> 2 </font>](https://github.com/jamo796/Digital-electronics-2/)
## LAB 02
### Doplňte následující tabulky

| **DDRB** | **Description** |
| :-: | :-- |
| 0 | Input pin |
| 1 | Output pin|

| **PORTB** | **Description** |
| :-: | :-- |
| 0 | Output Low Value |
| 1 | Output High Value |

| **DDRB** | **PORTB** | **Direction** | **Internal pull-up resistor** | **Description** |
| :-: | :-: | :-: | :-: | :-- |
| 0 | 0 | input | no | Vysoká ipedance, tři stavy |
| 0 | 1 | input | yes | na vstupu je log. H virtuálně odpojeno |
| 1 | 0 | output | no | Výstupní log. L |
| 1 | 1 | output | no | Výstupní log. H |


### 2. vypište část kódu v jazyce C se zvýrazněnou syntaxí, která obsluhuje 2 LED-ky jedna na portu C a bruhá na portu B


```c
int main(void)
{
	// Set both LEDs pins to output
    DDRB |= 1 << LED_GREEN; // output    
    // Reset one, set second
    PORTB |= (1 << LED_GREEN); // out 1

    DDRC |= 1 << LED_TWO;
    PORTC &= ~(1 << LED_TWO); 



    // Infinite loop
    while (1)
    {		
            // delay, toggle both LEDs
            _delay_ms(BLINK_DELAY);
            PORTC ^= (1 << LED_TWO);
            PORTB ^= (1 << LED_GREEN);    
        }
    }

    // Will never reach this
    return 0;
}
```

### 3. Výpis kódu C se zvýrazněnou syntaxí 

```c
int main(void)
{
    // Green LED at port B
    // Set pin as output in Data Direction Register...
    DDRB = DDRB | (1<<LED_GREEN);
    // ...and turn LED off in Data Register
    PORTB = PORTB & ~(1<<LED_GREEN);

    DDRD = DDRD | (0<<LED_GREEN);

    // Configure the second LED at port C
    DDRC = DDRC | (1<<LED_TWO);
    PORTC = PORTC & ~(1<<LED_TWO);
    
    PORTB = PORTB & ~(1<<LED_GREEN);
    PORTC = PORTC | (1<<LED_TWO);
    PORTD = PORTD | (1<<BUTTON);
    // Configure Push button at port D and enable internal pull-up resistor

    // Infinite loop
    while (1)
    {

        if(bit_is_set(PIND, BUTTON)) //pokud je bit nastaven tak vykonej jinak přeskoč jinak bit is clear znamená že bit je čistý (LOG. 0) tj. kód se vykoná pouze pokud tlačítko není stisknuté
        {
            
                    // Pause several milliseconds
            _delay_ms(BLINK_DELAY);

                    // WRITE YOUR CODE HERE
                    
            PORTB = PORTB ^ (1<<LED_GREEN);
            PORTC = PORTC ^ (1<<LED_TWO);
                           
        }
       
    }

    // Will never reach this
    return 0;
}

```

### Schema zapojení pro řadu led diod a jednoho tlačítka

###### obrázek