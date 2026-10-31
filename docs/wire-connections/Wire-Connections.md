# Z-Boat Wire Connections
## Contents

- [1. Overview](#1-overview)
- [2. Central components](#2-central-components)
- [3. CCM connection index](#3-ccm-connection-index)
- [4. CCM front: 24 V input](#4-ccm-front-24-v-input)
- [5. CCM rear: E-stop](#5-ccm-rear-e-stop)
- [6. CCM top panel](#6-ccm-top-panel)
- [7. CCM left side](#7-ccm-left-side)
- [8. CCM right side](#8-ccm-right-side)
- [9. Items to verify](#9-items-to-verify)
- [10. Additional reference photos](#10-additional-reference-photos)
- [11. Image sources and duplicate handling](#11-image-sources-and-duplicate-handling)

## 1. Overview

The source document records the boat layout, central components, and cable connections around the **Control and Communications Module (CCM)**. Its “overall dimensions” section contains photographs; no numerical measurements are provided.

![F01: Overall component layout, view overall](#put website here)

*Figure F01. Overall component layout, view overall.*

![F02: Overall component layout, view overall front](#put website here)

*Figure F02. Overall component layout, view overall front.*

![F03: Overall boat layout, view overall back](#put website here)

*Figure F03. Overall component layout, view overall back.*

## 2. Central components

### 2.1 Central component: CCM / Hydrolink

Central component is a yellow box which consists of two inputs, one is **CCM** one **Hydrolink**, the CCM is input is connected to a wire which linkts to the Hydrolink and Autonomy output of the control and communications module.The Hydrolink ouput is connected to TDM-E Serial port A-1. 

![F04: Component overview](#website)

*Figure F04. Component overview.*

![F05: Central component CCM](#website)

*Figure F05. Central component CCM cable routing.*

![F06: Central component Hydrolink](#website)

*Figure F06. Central component Hydrolink cable routing.*

### 2.2 TDM-E

The source lists the following TDM-E connections:

| Connection | Source description / status |
| --- | --- |
| Ethernet | Listed; destination not specified. |
| Serial port A-1 | Hydrolink in Central Component |
| 24 V input | Connected to one of the 24 V input cables derived from the 3 batteries |

![F07: TDM-E connection panel](#website)

*Figure F07. TDM-E connection panel.*

![F08: TDM-E power and cable detail](#website)

*Figure F08. TDM-E power and cable detail.*


## 3. CCM connection index

“Front,” “rear,” “top,” “left,” and “right” follow the source document's face labels. Only the motor names use the explicit port/starboard terminology from the source.

| CCM face | Port / connection | Cable label(s) | Reported routing / notes |
| --- | --- | --- | --- |
| Front | 24Volt IN | 24 V cable assembly | Branches toward TDM-E and the front-of-boat battery; see Section 4. |
| Rear | E-stop | Not specified | Cable identified as E-stop; used to cut down the connection of the propellors. |
| Top | Autonomy | CCM AUTONOMY | White cable; endpoint Central component CCM. |
| Top | GPS | GPS | White cable; endpoint white gps module on the lid of Z-boat. |
| Top | Hydrolink | CCM HYDROLINK | Black cable; endpoint Central component CCM. |
| Top | 2.4 GHz | 2.4GHZ; 2J | Black cable; reported route to the external white stick and external 2J. |
| Top | Sounder | Not specified | Listed; routing not documented. |
| Left | 5 GHz | 5G | Black cable; endpoint not specified. |
| Left | Port Motor | Left port motor | Black cable; route fixed along the left-side wall |
| Left | P.S. | Left P.S. | Yellow cable; route fixed along left-side wall|
| Left | AUX12V OUT | 12V; J2; J3; J4 | Reported split into three branches with green/red connector ends. |
| Right | Starboard Motor | Not specified | Black cable; Reported route to cables fixed along the right-side wall. |
| Right | S.S. | Not specified | Yellow cable; Reported route to cables fixed along the right-side wall. |
| Right | Servo | Not specified | Yellow cable; Reported route to cables fixed along the right-side wall. |

## 4. CCM front: 24 V input

### 4.1 Cable branching
#### 4.1.1 24 v connections
The original description says that the 24 V cable assembly splits into two smaller cables:

1. One branch connects to **TDM-E**.
2. The other branch connects to **24-input coontrol and communication module**

```text
24 V cable assembly described in the source
|
+-- Branch 1 ---- TDM-E
|
`-- Branch 2 ---- 24-input coontrol and communication module
```


### 4.2 Connection photos

![F10: 24 V cable branch, annotated view](../../IMG_1462.jpeg)

*Figure F10. 24 V cable branch, annotated view.*

![F11: 24 V connection near the battery](../../IMG_1463.jpeg)

*Figure F11. 24 V connection near the battery.*

![F12: 24 V battery connection close-up](../../IMG_1467.jpeg)

*Figure F12. 24 V battery connection close-up.*

![F13: 24 V cable routing, annotated view](../../IMG_1464.jpeg)

*Figure F13. 24 V cable routing, annotated view.*

![F14: 24 V cable 2, annotated view](../../IMG_1465.jpeg)

*Figure F14. 24 V cable 2, annotated view.*

## 5. CCM rear: E-stop

**Connection:** E-stop cable. The source does not describe the cable label, remote endpoint, or pin assignment.

![F15: CCM rear face and E-stop cable](../../IMG_1469.jpeg)

*Figure F15. CCM rear face and E-stop cable.*

## 6. CCM top panel

The source lists **2.4 GHz, Sounder, Autonomy, GPS, and Hydrolink** on the top face.

![F16: CCM top panel, annotated view](../../IMG_1446.jpeg)

*Figure F16. CCM top panel, annotated view.*

### 6.1 Autonomy, GPS, and Hydrolink

The original heading is **“HDMI Outputs.”** That interface-type description has not been verified and is not assumed here.

| Port | Cable description from the source |
| --- | --- |
| Autonomy | White cable labelled CCM AUTONOMY. |
| GPS | White cable labelled GPS. |
| Hydrolink | Cable labelled CCM HYDRLINK. |

![F17: Top-panel cable routing](../../IMG_1457.jpeg)

*Figure F17. Top-panel cable routing.*

![F18: Cable routing along the boat side](../../IMG_1471.jpeg)

*Figure F18. Cable routing along the boat side.*

![F19: Top-panel cable labels and connectors](../../IMG_1459.jpeg)

*Figure F19. Top-panel cable labels and connectors.*

The other routing view in the Word document duplicates Figure F05; see Section 2.1.

### 6.2 2.4 GHz

The source describes a black cable labelled **2.4GHZ** and **2J**, ultimately connecting to the external **white stick** and **2J**. The meaning of “2J” and the exact endpoints are not explained.

The photo placed under this subsection in the source duplicates the annotated “24 V cable 2” view, Figure F14. It is retained once in Section 4.2; its placement is not treated as proof of the 2.4 GHz route.

### 6.3 Sounder

Sounder is listed on the top panel; the source provides no separate cable-label or routing description.

## 7. CCM left side

Connections listed: **5 GHz, Port Motor, P.S., and AUX12V OUT**.

![F20: CCM left-side connection panel](../../IMG_1447.jpeg)

*Figure F20. CCM left-side connection panel.*

### 7.1 Port Motor

The Port Motor connection is attached to a cable labelled **Left port motor**. The source suggests that it may power the motor; this remains unconfirmed.

![F21: Port Motor connection and cable label](../../IMG_1455.jpeg)

*Figure F21. Port Motor connection and cable label.*

### 7.2 5 GHz

The 5 GHz connection is attached to a cable labelled **5G**. 

![F22: 5 GHz connection and 5G cable label](../../IMG_1454.jpeg)

*Figure F22. 5 GHz connection and 5G cable label.*

### 7.3 P.S.

A yellow cable labelled **Left P.S.** **Right P.S** connects to the P.S. port and is reported to run to the end of the boat. 

![F23: P.S. connection and cable label](../../IMG_1452.jpeg)

*Figure F23. P.S. connection and cable label.*

![F24: P.S. cable-routing reference](../../IMG_1451.jpeg)

*Figure F24. P.S. cable-routing reference.*

### 7.4 AUX12V OUT

The AUX12V OUT connection is attached to a cable labelled **12V**. The source describes a split into **three smaller wires**, each with green and red connector ends, labelled **J2, J3, and J4**. 

![F25: AUX12V OUT cable split, annotated view](../../IMG_1444.jpeg)

*Figure F25. AUX12V OUT cable split, annotated view.*

![F26: AUX12V OUT branch connector detail](../../IMG_1453.jpeg)

*Figure F26. AUX12V OUT branch connector detail.*

## 8. CCM right side

Connections listed: **Starboard Motor, S.S., and Servo**.

The source says that the connected cables lead to cables fixed along the right-side wall. It does not provide separate cable labels or destination mappings for these three connections, and it does not define S.S.

![F27: CCM right-side connection panel, annotated view](../../IMG_1448.jpeg)

*Figure F27. CCM right-side connection panel, annotated view.*

The second photo under this heading in the source duplicates Figure F18; see Section 6.1 for that routing view.


## 9. Additional reference photos

These distinct GitHub photos supplement the Word document. They are not used to infer new connections. An unannotated original and an annotated version are kept separately when the annotation adds information.

![S01: AUX12V OUT: unannotated full-resolution original of the annotated F25 view](../../IMG_1443.jpeg)

*Figure S01. AUX12V OUT: unannotated full-resolution original of the annotated F25 view.*

![S02: CCM top panel: additional full-resolution view](../../IMG_1445.jpeg)

*Figure S02. CCM top panel: additional full-resolution view.*

![S03: Left-side connector and cable-label detail: additional view](../../IMG_1449.jpeg)

*Figure S03. Left-side connector and cable-label detail: additional view.*

![S04: AUX12V OUT branch connector: additional view](../../IMG_1450.jpeg)

*Figure S04. AUX12V OUT branch connector: additional view.*

![S05: External device on the boat deck: additional reference view](../../IMG_1456.jpeg)

*Figure S05. External device on the boat deck: additional reference view.*

![S06: CCM top-panel connector: additional detail](../../IMG_1460.jpeg)

*Figure S06. CCM top-panel connector: additional detail.*

![S07: CCM right-side panel: additional view](../../IMG_1461.jpeg)

*Figure S07. CCM right-side panel: additional view.*

![S08: Battery wiring and cable label: additional view](../../IMG_1466.jpeg)

*Figure S08. Battery wiring and cable label: additional view.*

![S09: CCM rear panel and cable: additional view](../../IMG_1468.jpeg)

*Figure S09. CCM rear panel and cable: additional view.*

![S10: CCM rear-panel connector: additional detail](../../IMG_1470.jpeg)

*Figure S10. CCM rear-panel connector: additional detail.*


