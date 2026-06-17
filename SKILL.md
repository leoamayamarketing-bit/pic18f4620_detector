# SKILL: Pulse MCP - PIC18F4620 Port

## Descripción
Proyecto portado desde MC68HC908AP32 a PIC18F4620 manteniendo la misma funcionalidad: detector de metales Pulse con LCD 20x4, PWM audio, control de bobina, y menú completo.

## Configuración de Hardware
- **MCU:** PIC18F4620 (DIP-40)
- **Cristal:** 4MHz + HSPLL → 16MHz Fosc / 4MHz Fcy
- **LCD:** 20x4, modo 4-bit

## Pin Mapping (HC08 → PIC18F4620)

| Función | HC08 | PIC18F4620 | Dirección |
|---------|------|------------|-----------|
| RETENCION_POWER | PTA3 | RA0 | OUT |
| LED_FERROSO | PTA5 | RA1 | OUT |
| LED_NO_FERROSO | PTA4 | RA2 | OUT |
| BOTON_MENOS | PTD3 | RA3 | IN |
| BOTON_MENU | PTD4 | RA4 | IN |
| BOTON_LIGHT | PTD5 | RA5 | IN |
| SENSMA | PTB0 | RB0 | OUT |
| SENSME | PTB1 | RB1 | OUT |
| VOLUMA | PTB2 | RB2 | OUT |
| VOLUME | PTB3 | RB3 | OUT |
| LCD_E | PTB4 | RB4 | OUT |
| LCD_BACK | PTC4 | RB5 | OUT |
| LCD_RS | PTC5 | RB6 | OUT |
| BOTON_MUTE | PTD0 | RC5 | IN |
| BOTON_RESET | PTD1 | RC6 | IN |
| BOTON_MAS | PTD2 | RC7 | IN |
| CCP1 (AUDIO) | PTB5 | RC2 | OUT |
| SAMPLE | PTB6 | RC3 | OUT |
| PULSO_BOBINA | PTB7 | RC4 | OUT |
| LCD_DB4 | PTC0 | RD0 | OUT |
| LCD_DB5 | PTC1 | RD1 | OUT |
| LCD_DB6 | PTC2 | RD2 | OUT |
| LCD_DB7 | PTC3 | RD3 | OUT |
| KEY_SENSE | PTC7 | RE0 | IN |

## Periféricos
| Periférico | HC08 | PIC18F4620 |
|------------|------|------------|
| Timer base 1ms | TIM2 | Timer2 (PR2=249, prescaler 16) |
| PWM audio | TIM1 | CCP1 (RC2) |
| ADC | 8-bit, canales 6/7 | 10-bit, AN6/AN7 |
| Config storage | Flash (0x0860) | EEPROM interna (0x00-0x07) |
| Botones | KBI interrupt + polling | Polling directo |
| Serie | SCI | EUSART (RC6/RX, RC7/TX) |

## ADC Scaling
Original ADC era 8-bit (0-255), PIC tiene 10-bit (0-1023).
ValorPIC = valorHC08 × 4, para mantener compatibilidad de umbrales.

## Delays
Fcy = 4MHz (1 instrucción = 1µs). Usar `__delay_ms()`/`__delay_us()` de XC8.
Los delays HC08 estaban calculados para 7.3728MHz.

## EEPROM vs Flash
HC08 usaba Flash con rutinas ROM. PIC18 usa EEPROM interna con funciones XC8:
- `eeprom_read(addr)`
- `eeprom_write(addr, data)`
