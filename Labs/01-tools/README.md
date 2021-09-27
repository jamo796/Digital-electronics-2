# [DIGITAL ELECTRONICS <font size="5"> 2 </font>](https://github.com/jamo796/Digital-electronics-2/)
<font size="2"> odkaz na github je v nadpise </font>
 
### 1. Co znamenají Následující operátory v jazyce C?
   - ```|``` - Logický OR (součet)
   - ```&``` - Logický AND (sučin)
   - ```^``` - Logický XOR 
   - ```~``` - Logický NOT (negace)
   - ```<<``` - bitový posuv doleva (ve smyslu šimek)
   - ```>>``` - bitový posuv doprava (ve smyslu šimek)

### 2. Vyplňte pravdivostní tabulku s operátory <font size="3"> |, &, ^, ~ </font>


| **b** | **a** |**b or a** | **b and a** | **b xor a** | **not b** |
| :-: | :-: | :-: | :-: | :-: | :-: |
| 0 | 0 | 0 | 0 | 0 | 1 |
| 0 | 1 | 1 | 0 | 1 | 1 |
| 1 | 0 | 1 | 0 | 1 | 0 |
| 1 | 1 | 1 | 1 | 0 | 0 |


### 3. Výpis kódu C se zvýrazněnou syntaxí <font size="3"> opakující se tečka a čárka (morseova abeceda) </font>

```c
int main(void)
{
    // Set pin as output in Data Direction Register
    // DDRB = DDRB or 0010 0000
    DDRB = DDRB | (1<<LED_GREEN);

    // Set pin LOW in Data Register (LED off)
    // PORTB = PORTB and 1101 1111
    PORTB = PORTB & ~(1<<LED_GREEN);

    // Infinite loop
    while (1)
    {
        // Pause several milliseconds

        // Invert LED in Data Register
        // PORTB = PORTB xor 0010 0000

        _delay_ms(LONG_DELAY);//Dlouha Zapne
        PORTB = PORTB ^ (1<<LED_GREEN); //Dlouha
        _delay_ms(LONG_DELAY);//Dlouha Vypne
        PORTB = PORTB ^ (1<<LED_GREEN); //Dlouha

        _delay_ms(SHORT_DELAY);//kratka Zapne
        PORTB = PORTB ^ (1<<LED_GREEN); //kratka
        _delay_ms(SHORT_DELAY);//kratka Vypne
        PORTB = PORTB ^ (1<<LED_GREEN); //kratka


    }

    // Will never reach this
    return 0;
}

```

### Schema zapojení pro signalizaci Morseova kodu

###### obrázek
