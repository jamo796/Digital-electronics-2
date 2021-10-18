# [DIGITAL ELECTRONICS <font size="5"> 2 </font>](https://github.com/jamo796/Digital-electronics-2/)

## LAB 4: interrupts



### Overflow times

1.  Complete table with overflow times.



| **Module**     | **Number of bits** | **1**   | **8**     | **32** | **64**     | **128** | ***\*256\**** | ***\*1024\**** |
| -------------- | ------------------ | ------- | --------- | ------ | ---------- | ------- | ------------- | -------------- |
| Timer/Counter0 | 8                  | 16 us   | 128 us    | --     | 1024 us    | --      | 4096 us       | 16384 us       |
| Timer/Counter1 | 16                 | 4096 us | 32,768 ms | --     | 262,144 ms | --      | 1,0486 s      | 4,1944 s       |
| Timer/Counter2 | 8                  | 16 us   | 128 us    | 512 us | 1024 us    | 2048 us | 4096 us       | 16384 us       |



### Timer library



1. In your words, describe the difference between common C function and interrupt service routine.

* Function 
  * fukce se volá z hlavního programu a je tedy její volání vyžádáno z Hlavního programu není přerušeno vykonávání programu jen se vykonávání přesunulo na část která je vysunuta do knihovny nebo obecně do FCE 

* Interrupt service routine 
  * přerušení není voláno z hlavního programu přímo periferie sama přeruší vykonávání halvního programu a skočí na předem definovanou adresu kde vykoná instrukce a jakmile bude přerušení obslouženo vrátí se do hlavního programu a vykonávání bude pokračovat



2. Part of the header file listing with syntax highlighting, which defines settings for Timer/Counter0:



```c
/**

 \* @name  Definitions of Timer/Counter0

 \* @note  F_CPU = 16 MHz

 */

#define TIM0_stop()      TCCR0B &= ~((1<<CS02) | (1<<CS01) | (1<<CS00));

/** @brief Set overflow 4ms, prescaler 001 --> 1 */

#define TIM0_overflow_4ms()  TCCR0B &= ~((1<<CS02) | (1<<CS01)); TCCR0B |= (1<<CS00);

/** @brief Set overflow 33ms, prescaler 010 --> 8 */

#define TIM0_overflow_33ms()  TCCR0B &= ~((1<<CS02) | (1<<CS00)); TCCR0B |= (1<<CS01);

/** @brief Set overflow 262ms, prescaler 011 --> 64 */

#define TIM0_overflow_262ms() TCCR0B &= ~(1<<CS02); TCCR0B |= (1<<CS01) | (1<<CS00);

/** @brief Set overflow 1s, prescaler 100 --> 256 */

#define TIM0_overflow_1s()   TCCR0B &= ~((1<<CS01) | (1<<CS00)); TCCR0B |= (1<<CS02);

/** @brief Set overflow 4s, prescaler // 101 --> 1024 */

#define TIM0_overflow_4s()   TCCR0B &= ~(1<<CS01); TCCR0B |= (1<<CS02) | (1<<CS00);

/** @brief Enable overflow interrupt, 1 --> enable */

#define TIM0_overflow_interrupt_enable()  TIMSK1 |= (1<<TOIE1);

/** @brief Disable overflow interrupt, 0 --> disable */

#define TIM0_overflow_interrupt_disable() TIMSK1 &= ~(1<<TOIE1);
```



\3. Flowchart figure for function `main()` and interrupt service routine `ISR(TIMER1_OVF_vect)` of application that ensures the flashing of one LED in the timer interruption. When the button is pressed, the blinking is faster, when the button is released, it is slower. Use only a timer overflow and not a delay library. The image can be drawn on a computer or by hand. Use clear descriptions of the individual steps of the algorithms.



  ![your figure](..\obsloužení přerušení.png)





### Knight Rider

1. Scheme of Knight Rider application with four LEDs and a push button, connected according to Multi-function shield. Connect AVR device, LEDs, resistors, push button, and supply voltage. The image can be drawn on a computer or by hand. Always name all components and their values.



  ![your figure](..\knight rider.png)
