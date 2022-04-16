# Input-and-Output
/* Learn More - Program Analysis Activities
*
* 1. How many times do the LEDs flash if SW2 is quickly pressed and released?they all flash 1 time each.
*    Do the LEDs keep flashing when SW2 is held? Look at the program and
*    explain why this happens when SW2 is held.
	Yes the LEDs keep flashing because the While loop is set to 1, this means the loop will run as soon as SW2 is held. 
*
* 2. Explain the difference between the statements: LED3 = 0; and LED3 = 1; LED3 = 0 means that the LED will not turn on and LED3 = 1 means the LED will turn on
*
* 3. What voltage do you expect the microcontroller to output to LED D3 when
*    the statement LED3 = 0; runs?It will output 0V to the LED What voltage do you expect the output to be
*    when the statement LED3 = 1; runs?It will output 1V to the LED
*
*    You can confirm the output voltage with a voltmeter if you have access
*    to one. If you tried that, did the voltage match your prediction?
*
* 4. The statement 'if(SW2 == 0)' uses two equal signs, while the statement
*    'LED3 = 1;' uses a single equal sign. What operation is performed by one “=” assigns something to a value.
*    equal sign? What operation is performed by two equal signs?”==” asks is “a” equal to “b”. 
*
* 5. The following program code includes instructions that write to the PORTC
*    output latches directly. Try it by copying and pasting this code below
*    the existing SW2 'if' structure, at the location shown by the comment.
 
       if(SW3 == 0)
       {
           LATC = 0b00000000;
           __delay_ms(100);
           LATC = 0b11110000;
           __delay_ms(100);
       }
 
*    What happens when pushbutton SW3 is pressed?When SW3 is pressed the 4 LEDs turn on Identify at least one
*    advantage and one disadvantage of controlling the LEDs using 'LATC' writes The LEDs will flash while holding SW3, one disadvantage is that the LEDs will stay on indefinitely, one advantage is that you wont need to hold SW3 to have the LEDs on.
*    rather than through individual 'LEDn = x;' statements.
*
* 6. Next, compare the operation of 'if' and 'while' structures to simulate
*    momentary buttons. Replace the code you added in 5, above, with this code:
 
       // Momentary button using if structure
       if(SW3 == 0)
       {
           LED4 = 1;
       }
       else
       {
           LED4 = 0;
       }
 
       // Momentary button using while structure
       while(SW4 == 0)
       {
           LED5 = 1;
       }
       LED5 = 0;
 
*    First, try pressing and releasing SW3 and SW4 one at a time.
*
*    Next, press and hold SW3 while pressing and releasing SW4. Does it work
*    as expected?Yes it does work as expected.
*
*    Next, try press and holding SW4 while pressing and releasing SW3. Does it
*    work as expected? Explain the difference in operation between the 'if' and
*    'while' structures making up the momentary button code.The While statement will turn on LED5 while SW4 is pressed. The If statement states, if SW3 is pressed LED4 will turn on, otherwise LED4 will remain turned off.
*
* 7. Let's explore logical conditions using 'if' statements. Replace the code
*    added in 6, above, with this nested if code to make a logical AND
*    condition that will light LED D4 only if both SW3 and SW4 are pressed:
 
       // Nested if 'AND' code
       if(SW3 == 0)
       {
           if(SW4 == 0)
           {
               LED4 = 1;
           }
           else
           {
               LED4 = 0;
           }
       }
       else
       {
           LED4 = 0;
       }
 
*    Test the code to ensure it works as expected. Does the order of the if
*    conditions matter? (eg. swap the conditional checks for SW3 and SW4)
*	No the order does not matter but it would matter if this was to turn on 2 different LEDs 
* 8. Next, replace the code from 7 with the following code which implements a
*    logical AND conditional operator composed of two ampersands '&&':
       // Conditional 'AND' code
       if(SW3 == 0 && SW4 == 0)
       {
           LED4 = 1;
       }
       else
       {
           LED4 = 0;
       }
 
*    Does '&&' work the same way as the nested if structures? Can you think of
*    at least one advantage of using a logical conditional operator instead of
*    nested if structures? Using Logical conditional operators are better because they use at least one If statement where as Nested if statements use at least two.
*
* 9. Replace the double ampersand '&&' with double vertical bars '||)' to make
*    a logical OR conditional operator. Your code should look like this:
        // Conditional 'OR' code
       if(SW3 == 0 || SW4 == 0)
       {
           LED4 = 1;
       }
       else
       {
           LED4 = 0;
       }
 
*    Describe the conditions under which LED4 turns on.
*    LED4 turns on if SW3 or SW4 is pressed.
*
* Programming Activities
*
* 1. The statement '__delay_ms(100);' creates a 100ms delay. Try changing one
*    or more of the delay values in the program to 500ms and see what happens.
*
*    Can the delay be made even longer? Try 1000 ms. How big can the delay be
*    before MPLAB-X produces an error message? (Hint: can you think of a fast
*    and efficient way of guessing an unknown number?)
*
* 2. The '__delay_ms();' function only accepts integers as delay values. To
*    make delays shorter than 1ms, specify a delay in microseconds using the
*    '__delay_us();' function. You won't be able to see such short LED flashes
*    with your eyes, but you could measure them using an oscilloscope, or hear
*    them if they are used to turn the piezo beeper on and off. Try this code:
       // Make a tone while SW5 is held
       if(SW5 == 0)
       {
           BEEPER = 1;
           __delay_us(567);
           BEEPER = 0;
           __delay_us(567);
       }
 
*    Try changing the delay values in both of the __delay_us(); functions.
*    Does the pitch of the tone increase or decrease if the delay value is
*    made smaller? The smaller the value the higher the pitch of the beeper.
*
* 3. This code demonstrates a more compact way of toggling the beeper output
*    using a logical NOT operator '!'. Replace the code above, with this code:
       // Make a tone while SW5 is held
       if(SW5 == 0)
       {
           BEEPER = !BEEPER;
           __delay_us(567);
       }
 
*    One difference between this code and the code in 2, above, is the state
*    of the BEEPER pin when SW5 is released. What state will the BEEPER output
*    be in after this code runs?The beeper will turn off without a delay While one advantage of this method is smaller
*    code, can you think of one or more disadvantages based on its output when
*    the button is released? A disadvantage would be that if you wanted to play a tune then the beeber would turn off if you are not holding the button.
*
* 4. Using modified versions of the original SW2 'if' structure, create a
*    program that makes a unique LED flashing pattern for each pushbutton.
*
//LED patterns
 
//SW2 LED pattern   
if(SW2 == 0)
 
{
    LED5 = 1;
    __delay_ms(100);
    LED3 = 1;
    __delay_ms(100);
    LED4 = 1;
    __delay_ms(100);
    LED6 = 1;
    __delay_ms(100);
    LED5 = 0;
    __delay_ms(100);
    LED3 = 0;
    __delay_ms(100);
    LED4 = 0;
    __delay_ms(100);
    LED6 = 0;
    __delay_ms(100);
 
}
//SW3 LED pattern
if(SW3 == 0)
{
   LED4 = 1;
   __delay_ms(250);
   LED3 = 1;
   __delay_ms(250);
   LED5 = 1;
   __delay_ms(250);
   LED6 = 1;
   __delay_ms(250);
   LED4 = 0;
   __delay_ms(250);
   LED3 = 0;
   __delay_ms(250);
   LED5 = 0;
   __delay_ms(250);
   LED6 = 0;
   __delay_ms(250);
}
//SW4 LED Pattern
if(SW4 == 0)
{
   LED5 = 1;
   __delay_ms(500);
   LED4 = 1;
   __delay_ms(500);
   LED3 = 1;
   __delay_ms(500);
   LED6 = 1;
   __delay_ms(500);
   LED5 = 0;
   __delay_ms(500);
   LED4 = 0;
   __delay_ms(500);
   LED3 = 0;
   __delay_ms(500);
   LED6 = 0;
   __delay_ms(500);
 
}
//SW5 LED pattern
if(SW5 == 0)
{
   LED6 = 1;
   __delay_ms(50);
   LED5 = 1;
   __delay_ms(50);
   LED4 = 1;
   __delay_ms(50);
   LED3 = 1;
   __delay_ms(50);
   LED6 = 0;
   __delay_ms(50);
   LED5 = 0;
   __delay_ms(50);
   LED4 = 0;
   __delay_ms(50);
   LED3 = 0;
   __delay_ms(50);
}
 
 
*    Test each of your flashing patterns. Describe what happens when more than
*    one button is held. Do all of the patterns try to flash the LEDs at the
*    same time, or sequentially? Explain why this is.
	The LED patterns flash one after the other because the Delay statement in the if statement makes the pattern output until it is finished with that set of code then it will go to the next if statement while the appropriate button is held.
*
* 5. Create a program that makes a different tone for each pushbutton.
*
//Beeper tones
 
//SW2 Beeper tone
if(SW2 == 0)
{
   BEEPER = 1;
   __delay_us(1000);
   BEEPER = 0;
   __delay_us(1000);
}
 
//SW3 Beeper tone
if(SW3 == 0)
{
    BEEPER = 1;
   __delay_us(250);
   BEEPER = 0;
   __delay_us(250);
}
 
//SW4 Beeper tone
if(SW4 == 0)
{
    BEEPER = 1;
   __delay_us(500);
   BEEPER = 0;
   __delay_us(500);
}
//SW5 Beeper tone
if(SW5 == 0)
{
    BEEPER = 1;
   __delay_us(750);
   BEEPER = 0;
   __delay_us(750);
}
 
 
 
*    Test each tone by pressing each button individually. Next, press two or
*    more buttons at the same time. Describe what the tone waveform would look
*    like when more than one button is held. The different tones overlap each other. 
*
* 6. Use individual 'if' structures to simulate 'Start' and 'Stop' buttons for
*    an industrial machine. LED D4 should turn on when SW3 is pressed, stay on
*    even after SW3 is released, and turn off when SW4 is pressed. Test your
*    program to make sure it works.
*
* 7. Running your program from 6, above, describe what happens when both SW3
*    and SW4 are pressed. Does LED D4 stay on? If so, how does the brightness
*    of LED D4 compare between its normal on state following SW3 being pressed
*    to this new state when both SW3 and SW4 are bing held? Can you explain
*    why it changes? The LED dims in brightness because SW3 is sending power to the LED and SW4 is reducing the power, so The LED gets dimmer. 
*
 
* 8. As you can imagine, an industrial machine that is able to turn on even
*    while its 'Stop' button is pressed represents a significant safety hazard.
*    Using a logical conditional operator, modify the start-stop program from
 
 
 
 
 
 
 
*    activity 5 to make it safer. SW3 should only turn on LED D4 if SW4 is
*    released.
//Industrial machine Start and Stop (The safe way)
while(SW4 == 1)
{
if(SW3 == 0)
{
   LED4 = 1;
 
}
}
   if(SW4 ==0)
   {
       LED4 = 0;
   }
 
 
*
* 9. LED D1 is normally used to indicate that a program is running, but it can
*    be controlled by your program as well. If you take a look at the UBMP4
*    schematic, you will see that LED D1's cathode (or negative) pin is
*    connected to the microcontroller instead of the anode (positive) pin as
*    with the other LEDs. This means that you need to make D1's output a zero
*    to turn D1 on. Try it! Make a program that controls or flashes LED D1.
*/
//Messing around With LED1
 if(SW3 == 0)
{
    LED1 = 0;
    __delay_ms(50);
    LED1 = 1;
    __delay_ms(50);
 
}
 
 

