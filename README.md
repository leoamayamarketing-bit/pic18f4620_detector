# Pulse MCP - PIC18F4620

Puerto del detector de metales Pulse desde MC68HC908AP32 a PIC18F4620.

## Hardware
- **MCU:** PIC18F4620 (cristal 4MHz + PLL → 16MHz / 4MIPS)
- **LCD:** 20x4 modo 4-bit
- **Display:** Vúmetro de 40 segmentos, info de sensibilidad, volumen, frecuencia

## Pines
| Puerto | Conexión |
|--------|----------|
| RA0 | Retención Power |
| RA1 | LED Ferroso |
| RA2 | LED No Ferroso |
| RA3-RA5 | Botones (MENOS, MENU, LIGHT) |
| RB0-RB1 | Control Sensibilidad |
| RB2-RB3 | Control Volumen |
| RB4 | LCD E |
| RB5 | LCD Backlight |
| RB6 | LCD RS |
| RC2 | PWM Audio (CCP1) |
| RC3 | Sample Switch |
| RC4 | Pulso Bobina |
| RC5-RC7 | Botones (MUTE, RESET, MAS) |
| RD0-RD3 | LCD DB4-DB7 |
| RE0 | Key Sense (ON/OFF) |

## Compilación
- **IDE:** MPLAB X (importar carpeta)
- **Toolchain:** XC8
- **Build:** `make`
- **Programar:** MPLAB IPE o `make flash` (con Pickit3)

## Diferencia vs Original
- ADC 10-bit (vs 8-bit) → valores escalados x4
- EEPROM para configuración (vs Flash HC08)
- Timer2 para base 1ms (vs TIM2)
- CCP1 para PWM (vs TIM1)
- Botones por polling (vs KBI)
# pic18f4620_pulse_m
