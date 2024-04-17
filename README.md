# PMOD-LAN8720
![3D render](doc/3D%20render.png "3D rendering")
This is a single-width PMOD module with the RMII DP83TC813 100BASE-T1 PHY.

## Master/Slave
**100BASE-T1 require one of the device to be setup as a Slave, and the other one as a Master.** This concept doesn't exist in 100BASE-T and most usual Ethernet types, and seems to be a particularity of 100BASE-T1 and 1000BASE-T1. Check R42 placement to setup Master/Slave mode.

## Configuration
Straps have been setup for RMII slave mode (refclk has to be supplied from the host at 50MHz), 100BASE-T1 Master Mode (R43 present) and MDIO PHYADD=0 (JP1 and JP2 open).

### Master/Slave
When R42 is placed, the DP83TC813 acts as a **Master**. When R42 isn't placed, the internal pulldown of the PHY enables the **Slave** mode.

### Phyaddress
MDIO PHY address is set with JP1 and JP2. 9 different addresses can be configured:

| JP1  | JP2  | PHYADD[0-1] | PHYADD[2-3] | PHYADD |
|------|------|-------------|-------------|--------|
| OPEN | OPEN | 0b00        | 0b00        | 0b0000 |
| 1-2  | OPEN | 0b11        | 0b00        | 0b0011 |
| 2-3  | OPEN | 0b01        | 0b00        | 0b0001 |
| OPEN | 1-2  | 0b00        | 0b11        | 0b1100 |
| 1-2  | 1-2  | 0b11        | 0b11        | 0b1111 |
| 2-3  | 1-2  | 0b01        | 0b11        | 0b1101 |
| OPEN | 2-3  | 0b00        | 0b01        | 0b0100 |
| 1-2  | 2-3  | 0b11        | 0b01        | 0b0111 |
| 2-3  | 2-3  | 0b01        | 0b01        | 0b0101 |

## Pinout
| Pin | type  | Function | Description          |
|-----|-------|----------|----------------------|
| 1   | I     | TX_D1    | Transmit Data        |
| 2   | I     | TXEN     | Transmit Enable      |
| 3   | O     | RX_D0    | Receive Data         |
| 4   | I     | REFCLK   | 50MHz clock          |
| 5   |       | GND      |                      |
| 6   |       | VCC      | 3.3V rail            |
| 7   | I     | TX_D0    | Transmit Data        |
| 8   | O     | RX_DV    | Receive / Data valid |
| 9   | O     | RX_D1    | Receive Data         |
| 10  | I, PU | RST_T1   | Reset                |
| 11  |       | GND      |                      |
| 12  |       | VCC      | 3.3V rail            |

Legend:
- I: input (ie. output from the host)
- O: output (ie. input from the host)
- PU: Pull-up
