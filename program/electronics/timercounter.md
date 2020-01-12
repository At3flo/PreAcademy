# Timer/counters in the attiny44

- [Timer/counters in the attiny44](#timercounters-in-the-attiny44)
  - [The problem of the blinking LED](#the-problem-of-the-blinking-led)
  - [Operation modes](#operation-modes)
    - [Normal mode](#normal-mode)
    - [CTC mode](#ctc-mode)
    - [Selecting the mode of Operation](#selecting-the-mode-of-operation)

The **timer/counter** is a **piece of hardware** inside the microcontroller that can be used to **count and control time**. Actually, it does not count time, because it doesn't know anything about time. It should be actually named counter because **it just counts clock cycles**. What makes timers so interesting is the fact that they are **totally independent of the CPU**. The timers run parallel to the CPU without its intervention.

> **Note:** All the information listed here is a extract from the attiny44 datasheet. It just organized differently in order to be easier to understand. Other microcontrollers will have different register names.

## The problem of the blinking LED

Let's see the classical blinking LED code, where we have an LED in PA3, connected to ground.

```c
#include <avr/io.h>
#include <util/delay.h>

int main (void) {
    DDRA |= (1 << PA3); // set LED pin as output

while(1) {
      PORTA |= (1 << PA3);  // turn on the LED
      _delay_ms(1000);      // wait a second
      PORTA &= ~(1 << PA3); // turn off the LED
      _delay_ms(1000);      // wait a second
         }
  }
  ```

The problem when counting time this way, is that **the microcontroller cannot do anything else while we are waiting with the delay**. As your coding abilities increase you will notice a limitation in what you can achieve due to this problem. In fact, **you should never use delays**.

## The timers/counters

The ATtiny44 has two independent internal timers. One 8-bit (`TIMER0`) and another 16-bit (`TIMER1`), each with 2 PWM channels (more on this [later](pwm.md)). **Timers are actually registers** that increase automatically from 0 to 255. For the 8-bit, the count is stored in the `TCNT0` register:

![tcnt0 register](img/timercounter/tcnt0.png)

For the 16-bit register, the count from 0 to 65535 is stored in the `TCNT1` register, which in reality is split as two 8-bit registers, high `TCNT1H` and low `TCNT1L`:

![tcnt1 registers](img/timercounter/tcnt1.png)

When they reach the maximum value, they overflow back to zero and start counting again. So far, so good.

## The Prescaler

By default, the timer register increment at the speed of the microcontroller (if a microcontroller clock speed of 1 MHz is used, then 1,000,000 times per second). So at every tick of the clock you count 1/1,000,000 s.

> **Question:** Do you foresee the problem?

That is an impressive resolution. But we may want to time large time intervals as well. Sometimes we want to count a few seconds. So the problem is that, at 1Mhz speed, the register `TCNT0` is going to overflow too fast, exactly at 0.000256s.

Somehow we need to slow down the speed at which the counter is updating. One way if doing that it is hooking a slower oscillator or crystal. Actually most watches use a 32768Hz oscillator.

> **Question:** 32768Hz, Why this weird number?
> Clue: Power of two.

Another way to slow down the count is only increasing the count when a certain amount of clock cycles has occurred. This is called **prescaling**. For the AtTiny, the prescaler can be set to 8, 64, 256 or 1024 compared to the system clock.

If we set the prescaler to 1024. Then the register `TCNT0` will increase the count every 1024 clock cycles, thus every 1024/1000000 = 0.001024 s and will overflow at 0.262144 s.

### Setting the prescaler for `TIMER0`

The prescaler for `TIMER0` is set using the control register `TCCR0B`:
![](img/timercounter/tccr0b.png)
![](img/timercounter/timer0-prescaler.png)

### Setting the prescaler for `TIMER1`

The prescaler for `TIMER1` is set using the control register `TCCR1B`:
![](img/timercounter/tccr1b.png)
![](img/timercounter/timer1-prescaler.png)

> **WARNING!** Once you set the prescaler, the counter will start!

Let's see an example of using `TIMER0` to blink an LED every 124 counts at 1024 prescaler.

```c
#include <avr/io.h>

int main(void)
{
    // connect led to pin PA3
    DDRA |= (1 << PA3);

    // initialize timer
    // set up timer with prescaler = 1024
    TCCR0B |= (1 << CS02)|(1 << CS00);

    // initialize counter
    TCNT0 = 0;

    // loop forever
    while(1)
    {
        // check if the timer count reaches 124
        if (TCNT0 >= 124)
        {
            PORTA ^= (1 << PA3);    // toggles the led
            TCNT0 = 0;            // reset counter
        }
    }
}
```

## Operation modes

Timers have different modes of operation. We will focus in two for now: Normal mode and CTC mode. Let's explain what these modes do, one at a time.

### Normal mode

By default the timers will run in this mode. They will count from 0 to their maximum value 255/65535, and then overflow. The problem with this mode is that it is uncommon that we want to count up to that specific number, that is why the have the CTC mode.

### CTC mode

This is **clear timer on compare match** mode. This is the most common case. We will load a specific value in a register and then we will count up to that number. In each timer you can set up to 2 independent values that will trigger 2 independent interrupts. These for `TIMER0`:

![](img/timercounter/ocr0a.png)
![](img/timercounter/ocr0b.png)

And these for `TIMER1`:

![](img/timercounter/ocr1ab.png)

### Selecting the mode of Operation

Operation modes are set with the control registers `TCCR0A` and `TCCR0B` for the 8-bit `TIMER0`, according to the following table.

![](img/timercounter/tccr0a.png)
![](img/timercounter/tccr0b.png)
![](img/timercounter/timer0-wgm.png)

And `TCCR1A` and `TCCR1B` for the 16-bit `TIMER1`.

![](img/timercounter/tccr1a.png)
![](img/timercounter/tccr1b.png)
![](img/timercounter/timer1-wgm.png)

> **Learn by doing:** Write a piece of code that counts exactly 1 second. Assume you are using a 8 Mhz resonator.

---
[Back to Summary](../summary.md)
