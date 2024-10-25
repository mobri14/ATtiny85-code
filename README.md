#- - - - -ATtiny85-code- - - - -
Simple code examples for ATtiny85 


![arduino-attiny85-pcb-usb](https://github.com/user-attachments/assets/ec9cc974-8c52-437f-be14-7bcbf83fe92c)

![attiny85_blink_schematic](https://github.com/user-attachments/assets/9c6f8e76-f12d-4708-b34b-21c3e3d57888)


1. LED Blinker



```#include <avr/io.h>
#include <util/delay.h>

int main(void) {
    DDRB |= (1 << PB0); // Set PB0 as output
    while (1) {
        PORTB ^= (1 << PB0); // Toggle PB0
        _delay_ms(500);
    }
}
```


2. Digital Dice with LED



```#include <avr/io.h>
#include <util/delay.h>

int main() {
    DDRB = 0xFF; // Set all pins as outputs
    while (1) {
        PORTB = rand() % 7; // Random LED on
        _delay_ms(1000);
    }
}
```



3. Temperature Monitor (using LM35)



```#include <avr/io.h>
#include <util/delay.h>
#include <stdio.h>

int readADC() {
    ADMUX = (1 << REFS0);
    ADCSRA = (1 << ADEN) | (1 << ADSC);
    while (ADCSRA & (1 << ADSC));
    return ADC;
}

int main() {
    DDRB = 0xFF;
    while (1) {
        int temp = readADC() * 0.488;
        if (temp > 30) PORTB |= (1 << PB0);
        else PORTB &= ~(1 << PB0);
        _delay_ms(500);
    }
}
```
