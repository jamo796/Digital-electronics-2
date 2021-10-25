# [DIGITAL ELECTRONICS <font size="5"> 2 </font>](https://github.com/jamo796/Digital-electronics-2/)
 
Lab 5: Jan Pelka

Link to your Digital-electronics-2 GitHub repository:

https://github.com/jamo796/Digital-electronics-2/tree/main/Labs/05-segment

7-segment library

   In your words, describe the difference between Common Cathode and Common Anode 7-segment display.
    
   - CC SSD
      - jedná se o zapojení 7 seg se společnou katodou
      to znamená že mají společnou zem a tím pádem segment svítí pouze pokud na pin segmentu dovedem log. 1 tak se segmentu vlivem procházejícího proudu rozvítí pokud naň dovedem log. 0 tak není rozdíl potenciálů a tedy nemůže procházet proud (potom ani segment nemůže svítit)

   - CA SSD
      - jedná se o zapojení 7 seg se společného anodou (kladné napětí) poté abychom segment rozsvítily tak je potřeba na pin segmentu dovést log. 0 potom proud protéká od anody do katody a tímto proudem rozvítíme segment

   Code listing with syntax highlighting of two interrupt service routines (TIMER1_OVF_vect, TIMER0_OVF_vect) from counter application with at least two digits, ie. values from 00 to 59:

```c
/**********************************************************************
 * Function: Timer/Counter1 overflow interrupt
 * Purpose:  Increment counter value from 00 to 59.
 **********************************************************************/
ISR(TIMER1_OVF_vect)
{
   hod ++;
   if (hod >= 10000)
      {
          value = 0;
      }  // nastaví hodnotu proměnné hod na 0 pokud (do/pře)sáhne hodnotu 10 000
}

/**********************************************************************
 * Function: Timer/Counter0 overflow interrupt
 * Purpose:  Display tens and units of a counter at SSD.
 **********************************************************************/
ISR(TIMER0_OVF_vect)
{
    static uint8_t pos = 0;
    
    uint16_t hod2 = (hod % 10**(pozice+1)) / (10**(pozice)); // výpočet hodnoty kterou zobrazí

    SEG_update_shift_regs(hod2, pozice);

    pozice ++;
    if pozice == 4
        {
            pozice =0 ;
        }

}
```



Flowchart figure for function SEG_clk_2us() which generates one clock period on SEG_CLK pin with a duration of 2 us. The image can be drawn on a computer or by hand. Use clear descriptions of the individual steps of the algorithms.

  ![your figure](https://github.com/jamo796/Digital-electronics-2/blob/main/Labs/04-interups/obslou%C5%BEen%C3%AD%20p%C5%99eru%C5%A1en%C3%AD.png)

Kitchen alarm

Consider a kitchen alarm with a 7-segment display, one LED and three push buttons: start, +1 minute, -1 minute. Use the +1/-1 minute buttons to increment/decrement the timer value. After pressing the Start button, the countdown starts. The countdown value is shown on the display in the form of mm.ss (minutes.seconds). At the end of the countdown, the LED will start blinking.

  ![your figure](https://github.com/jamo796/Digital-electronics-2/blob/main/Labs/04-interups/obslou%C5%BEen%C3%AD%20p%C5%99eru%C5%A1en%C3%AD.png)
