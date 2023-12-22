# avr-interrupt-macro

This crate was designed for the ATmega1284p, so the interrupts and their vector numbers can differ when using a different AVR chip.

This crate provides a macro to define interrupt handlers for the AVR architecture.
As the implementation of interrupts is required to have very specific and hard to read function names, this macro
provides a way to define interrupt handlers with a more readable name. The macro renames the given function at
compile time to the required name. The macro also adds the `#[no_mangle]` attribute to the function, so that the
linker does not change the name of the function. The syn crate is used to parse the function definition, and the
quote crate is used to generate viable Rust code.
For every interrupt vector of the ATmega1284p microcontroller, there is a macro defined in this crate. The macro is
named `interrupt_handler_<vector_name>`, where `<vector_name>` is the name of the interrupt vector.
Here's a list of all interrupt vectors and a short description of their purpose:

| Interrupt vector name | Description                                                                                        |
| --------------------- | -------------------------------------------------------------------------------------------------- |
| `reset`               | The reset vector is called when the microcontroller is reset.                                      |
| `int0`                | The external interrupt 0 vector is called when the external interrupt 0 is triggered.              |
| `int1`                | The external interrupt 1 vector is called when the external interrupt 1 is triggered.              |
| `int2`                | The external interrupt 2 vector is called when the external interrupt 2 is triggered.              |
| `pcint0`              | The pin change interrupt 0 vector is called when a pin change interrupt is triggered on pins 7:0.  |
| `pcint1`              | The pin change interrupt 1 vector is called when a pin change interrupt is triggered on pins 15:8. |
| `pcint2`              | The pin change interrupt 2 vector is called when a pin change interrupt is triggered on pins 23:16.|
| `wdt`                 | The watchdog timer vector is called when the watchdog timer times out.                             |
| `timer2_compa`        | The timer2 compare match A vector is called when the timer2 compare match A is triggered.          |
| `timer2_compb`        | The timer2 compare match B vector is called when the timer2 compare match B is triggered.          |
| `timer2_ovf`          | The timer2 overflow vector is called when the timer2 overflows.                                    |
| `timer1_capt`         | The timer1 capture event vector is called when the timer1 capture event is triggered.              |
| `timer1_compa`        | The timer1 compare match A vector is called when the timer1 compare match A is triggered.          |
| `timer1_compb`        | The timer1 compare match B vector is called when the timer1 compare match B is triggered.          |
| `timer1_ovf`          | The timer1 overflow vector is called when the timer1 overflows.                                    |
| `timer0_compa`        | The timer0 compare match A vector is called when the timer0 compare match A is triggered.          |
| `timer0_compb`        | The timer0 compare match B vector is called when the timer0 compare match B is triggered.          |
| `timer0_ovf`          | The timer0 overflow vector is called when the timer0 overflows.                                    |
| `spi_stc`             | The SPI serial transfer complete vector is called when the SPI serial transfer is complete.        |
| `usart0_rx`           | The USART0 RX complete vector is called when the USART0 RX is complete.                            |
| `usart0_udre`         | The USART0 data register empty vector is called when the USART0 data register is empty.            |
| `usart0_tx`           | The USART0 TX complete vector is called when the USART0 TX is complete.                            |
| `analog_comp`         | The analog comparator vector is called when the analog comparator triggers.                        |
| `adc`                 | The ADC conversion complete vector is called when the ADC conversion is complete.                  |
| `ee_ready`            | The EEPROM ready vector is called when the EEPROM is ready.                                        |
| `twi`                 | The 2-wire serial interface vector is called when the 2-wire serial interface triggers.            |
| `spm_ready`           | The SPM ready vector is called when the SPM is ready.                                              |
| `usart1_rx`           | The USART1 RX complete vector is called when the USART1 RX is complete.                            |
| `usart1_udre`         | The USART1 data register empty vector is called when the USART1 data register is empty.            |
| `usart1_tx`           | The USART1 TX complete vector is called when the USART1 TX is complete.                            |
| `timer3_capt`         | The timer3 capture event vector is called when the timer3 capture event is triggered.              |
| `timer3_compa`        | The timer3 compare match A vector is called when the timer3 compare match A is triggered.          |
| `timer3_compb`        | The timer3 compare match B vector is called when the timer3 compare match B is triggered.          |
| `timer3_ovf`          | The timer3 overflow vector is called when the timer3 overflows.                                    |
# Examples
```Rust
use interrupt_macro::interrupt_handler_timer0_ovf;
#[interrupt_handler_timer0_ovf]
fn timer0_ovf() {
   // Interrupt handler code
}
```
In this example, the function `timer0_ovf` is defined as the interrupt handler for the timer0 overflow interrupt. The
macro renames the function to `__vector_10`, which is the name of the interrupt vector for the timer0 overflow interrupt.
The user does not have to worry about the name of the interrupt vector, as the macro takes care of it. This makes
the implementation of interrupt handlers much easier and more readable.
