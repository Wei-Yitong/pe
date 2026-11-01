# Z-Boat Wire Connections

## Contents

- [Diagram index](#diagram-index)
- [1. Overview](#1-overview)
- [2. Central components](#2-central-components)
- [3. CCM connection index](#3-ccm-connection-index)
- [4. CCM front: 24 V input](#4-ccm-front-24-v-input)
- [5. CCM rear: E-stop](#5-ccm-rear-e-stop)
- [6. CCM top panel](#6-ccm-top-panel)
- [7. CCM left side](#7-ccm-left-side)
- [8. CCM right side](#8-ccm-right-side)
- [9. Additional reference photos](#9-additional-reference-photos)
- [10. Image sources and duplicate handling](#10-image-sources-and-duplicate-handling)

## Diagram index

Start with D01 for the main equipment, then use the detailed diagrams to follow individual cables. Photo references below each diagram link to the corresponding views.

| Diagram | Connections shown |
| --- | --- |
| [D01. Main equipment and power](#d01-main-equipment-and-power) | All documented CCM, central-controller, and TDM-E ports, their cable routes, and GPS power from J3. |
| [D02. Central data connections](#d02-central-data-connections) | Autonomy/Hydrolink harness, central controller sockets, TDM-E data connections, and the GPS cable plus J3 power feed. |
| [D03. 24 V supply branches](#d03-24-v-supply-branches) | Battery harness branches to CCM and TDM-E. |
| [D04. E-stop connection](#d04-e-stop-connection) | CCM rear connection and the unrecorded remote termination. |
| [D05. Radio and sounder routes](#d05-radio-and-sounder-routes) | Top-panel 2.4 GHz cable and Sounder port. |
| [D06. Left-side cable routes](#d06-left-side-cable-routes) | Port Motor, P.S., 5 GHz, and AUX12V OUT, including the J3 feed to GPS. |
| [D07. Auxiliary 12 V branches](#d07-auxiliary-12-v-branches) | AUX12V OUT split to J2, J3, and J4; J3 powers the GPS module. |
| [D08. Right-side cable routes](#d08-right-side-cable-routes) | Starboard Motor, S.S., and Servo. |

**Reading the diagrams:** Solid lines show cable connections or routes documented in the revised notes and photos. Dashed lines show a continuation whose exact route or destination is not recorded. Lines describe physical connections; they do not specify signal direction or pin assignments. A harness node represents a cable assembly, and a group box represents an enclosure or routing area. Separate lines inside a group remain separate cables. Blue identifies equipment/ports, green identifies harnesses or connectors, orange with a dashed border identifies an unresolved route or endpoint, and grey identifies capped ports. Cable colours are written on the lines.

The Markdown edition renders these diagrams with Mermaid. The ASCII text edition includes equivalent text diagrams with the same D01-D08 identifiers.

## 1. Overview

This document records the boat layout, central components, and cable connections around the **Control and Communications Module (CCM)**, incorporating the revised connection notes and renamed photos. Figures F01-F03 show the overall, front, and back views respectively. The photographs provide layout references; no numerical boat dimensions are supplied.

### D01. Main equipment and power

```mermaid
%% D01
%%{init: {"flowchart": {"nodeSpacing": 18, "rankSpacing": 24, "padding": 10}}}%%
flowchart LR
    batteries["Three-battery<br/>supply"]
    power["24 V supply<br/>harness"]

    subgraph ccm["CCM"]
        subgraph ccm_front["Front face"]
            ccm_power["24VOLT IN"]
        end
        subgraph ccm_rear["Rear face"]
            estop["E-stop"]
        end
        subgraph ccm_top["Top panel"]
            autonomy["Autonomy"]
            hydro_ccm["Hydrolink"]
            gps_port["GPS"]
            radio24["2.4 GHz"]
            sounder["Sounder"]
        end
        subgraph ccm_left["Left face"]
            port_motor["Port Motor"]
            ps["P.S."]
            radio5["5 GHz"]
            aux["AUX12V OUT"]
        end
        subgraph ccm_right["Right face"]
            starboard_motor["Starboard Motor"]
            ss["S.S."]
            servo["Servo"]
        end
    end

    data_harness["Branched CCM<br/>harness"]
    subgraph central["Central controller"]
        central_ccm["CCM<br/>socket"]
        central_hydro["Hydrolink<br/>socket"]
    end
    subgraph tdm["TDM-E"]
        tdm_power["24 V input"]
        serial_a1["Serial port A-1"]
        serial_a2["Serial port A-2<br/>Yellow cap"]
        ethernet["Ethernet<br/>Cable attached"]
        ethernet_cap_a["Ethernet<br/>Capped"]
        ethernet_cap_b["Ethernet<br/>Capped"]
        usb["USB<br/>Capped"]
    end
    aux_harness["12V cable<br/>Three-branch assembly"]
    j2["J2<br/>Load unspecified"]
    j3["J3"]
    j4["J4<br/>Load unspecified"]
    gps_module["GPS module<br/>on boat lid"]

    estop_end["E-stop termination<br/>Not recorded"]
    radio24_end["External white stick / 2J<br/>Exact route unrecorded"]
    sounder_end["Sounder route<br/>Not documented"]
    port_motor_end["Left-wall route<br/>Motor end untraced"]
    ps_end["Left wall toward boat end<br/>P.S. end unrecorded"]
    radio5_end["5 GHz endpoint<br/>Not specified"]
    starboard_end["Right-wall route<br/>Motor end untraced"]
    ss_end["Right-wall route<br/>S.S. end unmapped"]
    servo_end["Right-wall route<br/>Servo end unmapped"]
    ethernet_end["Ethernet far end<br/>Not identified"]

    batteries --- power
    power ---|"24 V"| ccm_power
    power ---|"24 V"| tdm_power
    autonomy ---|"White:<br/>CCM AUTONOMY"| data_harness
    hydro_ccm ---|"Black:<br/>CCM HYDROLINK"| data_harness
    data_harness --- central_ccm
    central_hydro ---|"Black:<br/>TDM label"| serial_a1
    gps_port ---|"White:<br/>GPS cable"| gps_module
    aux ---|"12 V cable"| aux_harness
    aux_harness --- j2
    aux_harness --- j3
    aux_harness --- j4
    j3 ---|"12 V power<br/>to GPS"| gps_module
    estop -.- estop_end
    radio24 -.-|"Black:<br/>2.4GHZ / 2J"| radio24_end
    sounder -.- sounder_end
    port_motor -.-|"Black:<br/>Left port motor"| port_motor_end
    ps -.-|"Yellow:<br/>Left P.S."| ps_end
    radio5 -.-|"Black: 5G"| radio5_end
    starboard_motor -.-|"Black:<br/>motor lead"| starboard_end
    ss -.-|"Yellow:<br/>S.S. lead"| ss_end
    servo -.-|"Yellow:<br/>Servo lead"| servo_end
    ethernet -.- ethernet_end

    classDef equipment fill:#eff6ff,stroke:#2563eb,color:#172554;
    classDef harness fill:#ecfdf5,stroke:#047857,color:#064e3b;
    classDef unknown fill:#fff7ed,stroke:#9a3412,color:#7c2d12,stroke-dasharray:5 4;
    classDef capped fill:#f1f5f9,stroke:#64748b,color:#334155;
    class batteries,ccm_power,estop,autonomy,hydro_ccm,gps_port,radio24,sounder,port_motor,ps,radio5,aux,starboard_motor,ss,servo,central_ccm,central_hydro,tdm_power,serial_a1,ethernet,gps_module equipment;
    class power,data_harness,aux_harness,j3 harness;
    class serial_a2,ethernet_cap_a,ethernet_cap_b,usb capped;
    class j2,j4,estop_end,radio24_end,sounder_end,port_motor_end,ps_end,radio5_end,starboard_end,ss_end,servo_end,ethernet_end unknown;
```

This overall map includes **all 14 CCM connections**, grouped by face, both sockets on the central controller, and the TDM-E ports. The TDM-E box shows its 24 V input, A-1, capped A-2, three Ethernet sockets, and capped USB port. Each cable connects to its named port. The GPS module has both the white cable from **CCM GPS** and a **12 V power feed from AUX12V OUT branch J3**. J2 and J4 loads remain unspecified.

The grey ports are capped in the photos. The controller's power connection and the interconnection of the three batteries are not specified in the notes. D02-D08 expand the individual routes shown here.

**Photo references:** [F01](#figure-f01), [F02](#figure-f02), [F03](#figure-f03), [F04](#figure-f04), [F07](#figure-f07), [F09](#figure-f09), [F15](#figure-f15), [F16](#figure-f16), [F20](#figure-f20), [F25](#figure-f25), [F27](#figure-f27), and [S05](#figure-s05).

<a id="figure-f01"></a>

![F01: Overall boat layout](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/boat%20overview.jpeg)

*Figure F01. Overall boat layout.*

The full-boat view locates the open equipment compartment within the yellow hull. The CCM, central controller, and TDM-E sit inside the compartment; the deck antennas and two rear motor assemblies provide orientation for the closer wiring views.

<a id="figure-f02"></a>

![F02: Front overview of the equipment compartment](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/boat%20overview%20front.jpeg)

*Figure F02. Front overview of the equipment compartment.*

This view shows the CCM beside the central controller on its circular mounting cover, with the TDM-E adjacent to it. The crossing white and black leads provide context for the separate Autonomy, GPS, and Hydrolink routes described below.

<a id="figure-f03"></a>

![F03: Back overview of the equipment compartment](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/boat%20overview%20back.jpeg)

*Figure F03. Back overview of the equipment compartment.*

The blue TDM-E is visible on its foam support with a retaining strap, next to the central controller. Its serial and Ethernet connections, the nearby power leads, and the cabling around the compartment can be compared with the close-ups in Section 2.

## 2. Central components

### 2.1 Central component: CCM / Hydrolink

The central component is the yellow-faced **MSubs Z-Boat Autonomy Controller** mounted on the circular cover between the CCM and TDM-E. Its two labelled connections are **CCM** and **Hydrolink**.

| Central controller connection | Cable route in the revised notes | Photo reference |
| --- | --- | --- |
| CCM | A branched harness links this socket to both **Autonomy** and **Hydrolink** on the Control and Communications Module. The branches are labelled **CCM AUTONOMY** and **CCM HYDROLINK**. | F05; S12 |
| Hydrolink | A separate black lead connects this socket to **TDM-E Serial port A-1**. The TDM-E end is labelled **TDM**. | F06; S13 |

The CCM module's Hydrolink connection is therefore part of the harness entering the central controller's **CCM** socket. The controller's own **Hydrolink** socket continues to TDM-E. Figures S11-S13 provide additional connector and routing views.

#### D02. Central data connections

```mermaid
%% D02
flowchart TB
    subgraph ccm_top["CCM top panel"]
        autonomy["Autonomy"]
        hydro_ccm["Hydrolink"]
        gps_port["GPS"]
    end
    subgraph ccm_gps_power["CCM left face"]
        aux_gps["AUX12V OUT"]
    end
    j3_gps["J3<br/>12 V harness branch"]
    harness["Branched CCM harness"]
    subgraph central["Central autonomy controller"]
        central_ccm["CCM socket"]
        central_hydro["Hydrolink socket"]
    end
    subgraph tdm_panel["TDM-E data ports"]
        serial["Serial port A-1"]
        ethernet["Connected Ethernet port"]
    end
    gps["GPS module<br/>on boat lid"]
    network["Ethernet far-end device<br/>not identified"]

    autonomy ---|"White:<br/>CCM AUTONOMY"| harness
    hydro_ccm ---|"Black:<br/>CCM HYDROLINK"| harness
    harness --- central_ccm
    central_hydro ---|"Black lead; TDM label"| serial
    gps_port ---|"White: GPS"| gps
    aux_gps ---|"12V cable / branch assembly"| j3_gps
    j3_gps ---|"12 V power"| gps
    ethernet -.-|"Attached Ethernet lead"| network

    classDef equipment fill:#eff6ff,stroke:#2563eb,color:#172554;
    classDef harnessStyle fill:#ecfdf5,stroke:#047857,color:#064e3b;
    classDef unknown fill:#fff7ed,stroke:#9a3412,color:#7c2d12,stroke-dasharray:5 4;
    class autonomy,hydro_ccm,gps_port,central_ccm,central_hydro,serial,ethernet,gps,aux_gps equipment;
    class harness,j3_gps harnessStyle;
    class network unknown;
```

The two CCM module leads share a branched cable assembly ending at the central controller's **CCM socket**. Its **Hydrolink socket** has a separate cable to TDM-E A-1. The controller group shows both sockets without assigning an internal electrical connection between them. TDM-E A-2 and USB are capped in the photos; they have no attached cable shown here. See D03 for TDM-E power.

The **GPS module receives 12 V power from J3** on the AUX12V OUT harness, alongside its white GPS cable connection to the CCM top panel. See D07 for all three 12 V branches.

**Photo references:** [F05](#figure-f05), [F06](#figure-f06), [F07](#figure-f07), [F17](#figure-f17), [F19](#figure-f19), [F25](#figure-f25), [F26](#figure-f26), [S05](#figure-s05), [S11](#figure-s11), [S12](#figure-s12), [S13](#figure-s13), and [S15](#figure-s15).

<a id="figure-f04"></a>

![F04: Central component overview](https://raw.githubusercontent.com/Wei-Yitong/pe/main/docs/wire-connections/assets/word-image09.jpg)

*Figure F04. Central component overview.*

The original Word overview shows the yellow-faced central controller between the CCM and TDM-E, with a labelled 24 V lead crossing the circular cover. It establishes the relative positions of the three units before the individual cable routes are traced.

<a id="figure-f05"></a>

![F05: Central component CCM cable routing](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/central%20component%20CCM.jpg)

*Figure F05. Central component CCM cable routing.*

The lifted branched harness connects the central controller's CCM socket to the CCM module's Autonomy and Hydrolink connections. The pale branch carries the CCM AUTONOMY label and the black branch carries CCM HYDROLINK; the controller end uses a right-angle plug with a metal locking collar.

<a id="figure-f06"></a>

![F06: Central component Hydrolink cable routing](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/central%20component%20Hydrolink.jpg)

*Figure F06. Central component Hydrolink cable routing.*

The controller's Hydrolink connection is shown beside its CCM connection. The black Hydrolink lead loops toward TDM-E Serial port A-1, where the cable is labelled TDM; this is a separate route from the branched harness in F05.

### 2.2 TDM-E

The blue TDM-E sits beside the central controller on a foam support. The revised notes and panel photographs identify these connections:

| Connection | Description / routing | Photo reference |
| --- | --- | --- |
| Ethernet | Three panel positions are visible, with one cable attached. The far-end device is not identified. | F07; S14; S15 |
| Serial port A-1 | Connected to **Hydrolink on the central controller** through the black lead labelled **TDM**. | F06; F07 |
| Serial port A-2 | Covered by a yellow cap in the photographs. | F07; S14 |
| USB | Covered by a black tethered cap in the photographs. | F08; S14 |
| 24 V input | Supplied by one branch of the 24 V harness from the three batteries. Red and green conductors enter through the enclosure's side gland beside the ON/OFF switch. | F08; F13 |

See Section 4 for the battery supply and the two branches to TDM-E and the CCM.

<a id="figure-f07"></a>

![F07: TDM-E connection panel](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/TDM%20-E%20top%20view.jpeg)

*Figure F07. TDM-E connection panel.*

The top view shows three Ethernet positions, a capped USB connection, Serial port A-1 with the TDM-labelled cable attached, and Serial port A-2 under a yellow cap. One Ethernet cable is connected, and the unit is held against its foam support by a black strap.

<a id="figure-f08"></a>

![F08: TDM-E power-entry detail](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/TDM%20-%20E%20powering.jpeg)

*Figure F08. TDM-E power-entry detail.*

The close-up shows red and green conductors entering the side of the TDM-E through a cable gland, beside the ON/OFF switch. The 24V INPUT marking, TDM-labelled serial cable, capped USB port, and adjacent Ethernet connector identify the power-entry area.

## 3. CCM connection index

“Front,” “rear,” “top,” “left,” and “right” follow the source document's face labels. Only the motor names use the explicit port/starboard terminology from the source.

| CCM face | Port / connection | Cable label(s) | Reported routing / notes |
| --- | --- | --- | --- |
| Front | 24Volt IN | 24 V cable assembly | Receives one branch of the battery supply; the other branch supplies TDM-E. See Section 4. |
| Rear | E-stop | Not specified | Identified in the revised notes as the connection used to stop the propellers. |
| Top | Autonomy | CCM AUTONOMY | White lead; joins the branched harness to the central controller's CCM socket. |
| Top | GPS | GPS | White cable to the GPS module on the boat lid; the module also receives 12 V power from AUX12V OUT branch J3. |
| Top | Hydrolink | CCM HYDROLINK | Black lead; joins the branched harness to the central controller's CCM socket. |
| Top | 2.4 GHz | 2.4GHZ; 2J | Black cable; reported route to the external white stick and external 2J. |
| Top | Sounder | Not specified | Listed; routing not documented. |
| Left | 5 GHz | 5G | Black cable; endpoint not specified. |
| Left | Port Motor | Left port motor | Black cable; follows the left-side wall. |
| Left | P.S. | Left P.S. | Yellow cable; follows the left-side wall toward the end of the boat. See the label note in Section 7.3. |
| Left | AUX12V OUT | 12V; J2; J3; J4 | Three branches with green/red connector ends. J3 supplies 12 V power to the GPS module; J2 and J4 loads are unspecified. |
| Right | Starboard Motor | Not specified | Black cable; follows the right-side wall. |
| Right | S.S. | Not specified | Yellow cable; follows the right-side wall. |
| Right | Servo | Not specified | Yellow cable; follows the right-side wall. |

## 4. CCM front: 24 V input

The CCM front face carries the **24VOLT IN** connection. Figure F09 identifies the face; F10 shows the input leads and inline connections more closely.

<a id="figure-f09"></a>

![F09: CCM front face and 24 V input](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/CCM%20Front%20view%20.jpeg)

*Figure F09. CCM front face and 24 V input.*

The annotated front view identifies the CCM face marked 24VOLT IN. The red and black power leads enter through the front cable gland, providing the starting point for tracing the CCM supply branch in F10.

### 4.1 Cable branching

The revised notes describe a 24 V supply harness from the **three batteries**, with two branches:

1. One branch supplies **TDM-E**.
2. The other branch supplies **24VOLT IN on the Control and Communications Module**.

#### D03. 24 V supply branches

```mermaid
%% D03
flowchart LR
    batteries["Three batteries<br/>Interconnection not specified"]
    supply["24 V supply harness<br/>Two documented branches"]
    tdm_power["TDM-E 24 V input<br/>Side cable gland by ON/OFF switch"]
    ccm_power["CCM 24VOLT IN<br/>Front-face cable gland"]

    batteries --- supply
    supply ---|"Branch to TDM-E<br/>24 V cable 1 in F13"| tdm_power
    supply ---|"Branch to CCM<br/>Input leads in F09-F10"| ccm_power

    classDef equipment fill:#eff6ff,stroke:#2563eb,color:#172554;
    classDef harness fill:#ecfdf5,stroke:#047857,color:#064e3b;
    class batteries,tdm_power,ccm_power equipment;
    class supply harness;
```

F11, F12, F14, and S08 document the battery-area wiring. F13 identifies the branch toward TDM-E, and F08 shows its power-entry end. The diagram records the two reported destinations; it does not specify how the three batteries are interconnected.

**Photo references:** [F08](#figure-f08), [F09](#figure-f09), [F10](#figure-f10), [F11](#figure-f11), [F12](#figure-f12), [F13](#figure-f13), [F14](#figure-f14), and [S08](#figure-s08).

### 4.2 Connection photos

<a id="figure-f10"></a>

![F10: CCM 24 V input cable detail](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/DC%2024V%20front%20view.jpeg)

*Figure F10. CCM 24 V input cable detail.*

The closer annotated view follows the red and black leads at the CCM front face and their inline connectors. The 24 V label and Forward annotation distinguish this supply connection from the nearby data and antenna cables.

<a id="figure-f11"></a>

![F11: 24 V wiring near the batteries](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/DC%2024V%20wirings.jpeg)

*Figure F11. 24 V wiring near the batteries.*

This view records the power-cable connections in the battery area. Use it with the annotated battery view in F14 to follow the 24 V harness between the batteries and the branches supplying the CCM and TDM-E.

<a id="figure-f12"></a>

![F12: Battery power-connection close-up](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/DC%2024%20wirings%20%283%29.jpeg)

*Figure F12. Battery power-connection close-up.*

The close view supplements F11 by showing the battery-area power wiring in more detail. It is a reference for matching the leads and connector positions to the wider battery view; the photographs do not establish the batteries' series or parallel arrangement.

<a id="figure-f13"></a>

![F13: 24 V cable branch toward TDM-E](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/DC%2024V%20TDM-E%20powering.jpeg)

*Figure F13. 24 V cable branch toward TDM-E.*

The lead identified as 24 V cable 1 is lifted above the central controller's circular cover. The red and black pair and its red/green connector housings show the branch identified in the revised notes as supplying TDM-E; F08 shows the device's power-entry end.

<a id="figure-f14"></a>

![F14: Battery connections and 24 V cable 2](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/DC%2024V%20battery%20connections.jpeg)

*Figure F14. Battery connections and 24 V cable 2.*

The annotated battery view shows the strapped battery assembly and several paired power connectors. The 24 V cable 2 annotation and the Charge Terminal and Discharge Terminal tags help distinguish the battery connections from the branch toward TDM-E.

## 5. CCM rear: E-stop

**Connection:** E-stop cable. The revised notes identify this as the connection used to stop the propellers. F15 and S09 show the CCM rear face and cable exit; the notes do not specify the remote termination or pin assignment.

### D04. E-stop connection

```mermaid
%% D04
flowchart LR
    rear["CCM rear face<br/>E-stop connection"]
    cable["Cable identified as E-stop"]
    termination["Remote termination<br/>not recorded"]
    rear --- cable
    cable -.- termination

    classDef equipment fill:#eff6ff,stroke:#2563eb,color:#172554;
    classDef harness fill:#ecfdf5,stroke:#047857,color:#064e3b;
    classDef unknown fill:#fff7ed,stroke:#9a3412,color:#7c2d12,stroke-dasharray:5 4;
    class rear equipment;
    class cable harness;
    class termination unknown;
```

The notes give the E-stop's function as stopping the propellers. Its remote termination and switching circuit are not recorded, so the diagram ends at that unresolved connection.

**Photo references:** [F15](#figure-f15) and [S09](#figure-s09).

<a id="figure-f15"></a>

![F15: CCM rear face and E-stop cable](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/CCM%20rear%20view.jpeg)

*Figure F15. CCM rear face and E-stop cable.*

This rear view locates the CCM connection identified as E-stop and shows its cable leaving the enclosure. The revised notes describe its role in stopping the propellers; the remote termination and pin assignment are not shown in this view.

## 6. CCM top panel

The source lists **2.4 GHz, Sounder, Autonomy, GPS, and Hydrolink** on the top face.

### D05. Radio and sounder routes

Autonomy, GPS, and Hydrolink are shown in [D02](#d02-central-data-connections). This diagram covers the other two listed top-panel connections.

```mermaid
%% D05
flowchart LR
    subgraph top["CCM top panel"]
        radio["2.4 GHz"]
        sounder["Sounder"]
    end
    radio_lead["Black cable<br/>2.4GHZ / 2J labels"]
    external["Reported: external white stick<br/>and external 2J<br/>Exact route not recorded"]
    sounder_end["Sounder cable / endpoint<br/>not documented"]
    radio --- radio_lead
    radio_lead -.- external
    sounder -.- sounder_end

    classDef equipment fill:#eff6ff,stroke:#2563eb,color:#172554;
    classDef harness fill:#ecfdf5,stroke:#047857,color:#064e3b;
    classDef unknown fill:#fff7ed,stroke:#9a3412,color:#7c2d12,stroke-dasharray:5 4;
    class radio,sounder equipment;
    class radio_lead harness;
    class external,sounder_end unknown;
```

The external references are kept together because the notes do not describe a splitter or map separate branches to the white stick and 2J. The Sounder continuation marks missing routing information.

**Photo references:** [F16](#figure-f16), [S02](#figure-s02), and [S06](#figure-s06).

<a id="figure-f16"></a>

![F16: CCM top panel with connection annotations](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/CCM%20top%20view%20with%20wording.jpeg)

*Figure F16. CCM top panel with connection annotations.*

The annotated top view provides the panel reference for 2.4 GHz, Sounder, Autonomy, GPS, and Hydrolink. Use the individual cable labels in F19 and S06 to distinguish the data leads from the radio connection.

### 6.1 Autonomy, GPS, and Hydrolink

The original heading is **“HDMI Outputs.”** That interface-type description has not been verified and is not assumed here.

| Port | Cable label and route |
| --- | --- |
| Autonomy | White lead labelled **CCM AUTONOMY**; joins the harness to the central controller's **CCM** socket. |
| GPS | White lead labelled **GPS**; runs to the white GPS module on the boat lid, shown in S05. The module's 12 V power comes from **J3** on the AUX12V OUT harness. |
| Hydrolink | Black lead labelled **CCM HYDROLINK**; joins the same central **CCM** harness as Autonomy. The original transcription spells this label CCM HYDRLINK. |

<a id="figure-f17"></a>

![F17: GPS cable route at the CCM](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/GPS%20module%20wiring.jpeg)

*Figure F17. GPS cable route at the CCM.*

This photo records the white GPS cable at the CCM and its route to the module on the boat lid, shown in S05. The module also receives 12 V power from J3 on the AUX12V OUT harness; D02 shows both connections and D07 expands the power branches.

<a id="figure-f19"></a>

![F19: CCM top-panel connectors and cable labels](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/CCM%204%20Inputs.jpeg)

*Figure F19. CCM top-panel connectors and cable labels.*

This close view groups the top-panel connections and their cable labels so they can be compared with F16. The Autonomy and Hydrolink leads join the central controller's CCM harness, while the GPS lead follows the separate route described in F17.

See F05 and S12 for the branched Autonomy/Hydrolink harness, and F06 for the separate connection from the central controller to TDM-E.

### 6.2 2.4 GHz

The source describes a black cable labelled **2.4GHZ** and **2J**, ultimately connecting to the external **white stick** and **2J**. The meaning of “2J” and the exact endpoints are not explained.

Figure S06 provides the dedicated 2.4 GHz cable-label photo. The original Word document repeated the battery photo F14 under this heading; that image remains in the power section.

### 6.3 Sounder

Sounder is listed on the top panel; the source provides no separate cable-label or routing description.

## 7. CCM left side

Connections listed: **5 GHz, Port Motor, P.S., and AUX12V OUT**.

### D06. Left-side cable routes

```mermaid
%% D06
flowchart LR
    subgraph left_ports["CCM left face"]
        motor["Port Motor"]
        ps["P.S."]
        radio5["5 GHz"]
        aux["AUX12V OUT"]
    end
    subgraph left_wall["Along the left-side wall<br/>Separate cable runs"]
        motor_run["Black: Left port motor"]
        ps_run["Yellow: Left P.S."]
    end
    radio_lead["Black cable: 5G"]
    aux_branches["12V cable / three branches<br/>J2, J3, J4"]
    gps_module["GPS module on boat lid"]
    motor_end["Motor cable endpoint<br/>not traced"]
    ps_end["Reported: toward end of boat<br/>Exact termination not recorded"]
    radio_end["5 GHz endpoint<br/>not specified"]

    motor --- motor_run
    ps --- ps_run
    motor_run -.- motor_end
    ps_run -.- ps_end
    radio5 --- radio_lead
    radio_lead -.- radio_end
    aux --- aux_branches
    aux_branches ---|"J3: 12 V power"| gps_module

    classDef equipment fill:#eff6ff,stroke:#2563eb,color:#172554;
    classDef harness fill:#ecfdf5,stroke:#047857,color:#064e3b;
    classDef unknown fill:#fff7ed,stroke:#9a3412,color:#7c2d12,stroke-dasharray:5 4;
    class motor,ps,radio5,aux,gps_module equipment;
    class motor_run,ps_run,radio_lead,aux_branches harness;
    class motor_end,ps_end,radio_end unknown;
```

All four left-face connections are shown, including **AUX12V OUT**. Its 12 V cable splits into J2, J3, and J4, and **J3 powers the GPS module**; [D07](#d07-auxiliary-12-v-branches) expands the individual branches. The Port Motor and P.S. cables follow the left side of the hull as separate runs. The **Right P.S.** wording in the revised notes has no separate port mapping; Section 7.3 retains that distinction.

**Photo references:** [F18](#figure-f18), [F20](#figure-f20), [F21](#figure-f21), [F22](#figure-f22), [F23](#figure-f23), [F24](#figure-f24), [F25](#figure-f25), [F26](#figure-f26), [S03](#figure-s03), [S04](#figure-s04), and [S05](#figure-s05).

<a id="figure-f20"></a>

![F20: CCM left-side connection panel](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/CCM%20left%20view.jpeg)

*Figure F20. CCM left-side connection panel.*

The annotated left-side view locates the 5 GHz, Port Motor, P.S., and AUX12V OUT connections on the same enclosure face. The following close-ups identify their cable labels and separate the motor and P.S. leads from the auxiliary power branches.

### 7.1 Port Motor

The Port Motor connection is attached to the black cable labelled **Left port motor**. The revised notes place its route along the left-side wall. F21 identifies the local connector and label; the photographs do not trace the complete connection to the motor.

<a id="figure-f21"></a>

![F21: Port Motor connection and cable label](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/Left%20port%20motor%20labelling.jpeg)

*Figure F21. Port Motor connection and cable label.*

The close-up identifies the black cable labelled Left port motor at the CCM Port Motor connection. The revised notes place its onward route along the left-side wall; the label provides the reference for distinguishing it from the adjacent yellow P.S. cable.

### 7.2 5 GHz

The 5 GHz connection is attached to a black cable labelled **5G**. F22 identifies the cable at the CCM; the notes do not specify its remote endpoint.

<a id="figure-f22"></a>

![F22: 5 GHz connection and cable label](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/5G%20labelling.jpeg)

*Figure F22. 5 GHz connection and cable label.*

The photo identifies the black lead labelled 5G at the CCM's 5 GHz connection. It records the local connector and cable identification; the complete route to its remote endpoint is not established by this close-up.

### 7.3 P.S.

A yellow cable labelled **Left P.S.** connects to the P.S. port and follows the left-side wall toward the end of the boat. Figure F23 shows the **Left P.S.** tag. The revised text also mentions **Right P.S.**, but does not map that label to a separate connector; it is not assigned to this left-side port. Figures F18, F24, and S04 provide the surrounding routing views.

<a id="figure-f23"></a>

![F23: P.S. connection and Left P.S. label](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/P.S%20labelling.jpeg)

*Figure F23. P.S. connection and Left P.S. label.*

The yellow cable enters the small connector below the P.S. marking, and the held tag reads Left P.S. The adjacent 5 GHz connector and larger black plug help locate it on the left face of the CCM.

<a id="figure-f18"></a>

![F18: Cable routing beside the CCM](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/CCM%20P.S%20connections.jpeg)

*Figure F18. Cable routing beside the CCM.*

The wider routing view shows cables passing beside the CCM and continuing along the compartment wall. The renamed photo identifies this as a P.S. connection reference; F23 shows the labelled P.S. connector, and F24 provides another view of the routing area.

<a id="figure-f24"></a>

![F24: P.S. route, second reference view](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/P.s%20route%202.jpeg)

*Figure F24. P.S. route, second reference view.*

This second routing view complements the P.S. label close-up in F23 and the first route view in S04. Together they document the cable area associated with the left-side route toward the end of the boat.

### 7.4 AUX12V OUT

The AUX12V OUT connection is attached to a cable labelled **12V**. The source describes a split into **three smaller wires**, each with green and red connector ends, labelled **J2, J3, and J4**.

**J3 supplies 12 V power to the GPS module on the boat lid.** The module also has the white GPS cable connection to the CCM top panel. The connected loads on J2 and J4 are not specified in the notes.

#### D07. Auxiliary 12 V branches

```mermaid
%% D07
flowchart LR
    aux["CCM left face<br/>AUX12V OUT"]
    split["Three-branch cable assembly"]
    j2["J2<br/>Red / green connector ends"]
    j3["J3<br/>Red / green connector ends"]
    j4["J4<br/>Red / green connector ends"]
    gps_module["GPS module on boat lid"]
    aux ---|"Cable labelled 12V"| split
    split --- j2
    split --- j3
    split --- j4
    j3 ---|"12 V power"| gps_module

    classDef equipment fill:#eff6ff,stroke:#2563eb,color:#172554;
    classDef harness fill:#ecfdf5,stroke:#047857,color:#064e3b;
    class aux,gps_module equipment;
    class split,j2,j3,j4 harness;
```

J2, J3, and J4 identify the three branch connectors. **J3 powers the GPS module**; J2 and J4 loads remain unspecified. Connector pin polarity is not documented.

**Photo references:** [F17](#figure-f17), [F25](#figure-f25), [F26](#figure-f26), [S01](#figure-s01), and [S05](#figure-s05).

<a id="figure-f25"></a>

![F25: AUX12V OUT cable split with annotations](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/DC%2012V%20wiring%20with%20words.jpeg)

*Figure F25. AUX12V OUT cable split with annotations.*

The annotated view identifies the auxiliary 12 V harness and its J2, J3, and J4 branches with red and green connector ends. J3 supplies the GPS module's 12 V power; F26 provides the branch-label detail, and S05 shows the powered module.

<a id="figure-f26"></a>

![F26: AUX12V OUT branch labels and connectors](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/DC%2012v%20wiring%20labelled.jpeg)

*Figure F26. AUX12V OUT branch labels and connectors.*

This close-up records the 12V, J2, J3, and J4 identifiers and the branch connector ends. J3 is the GPS module's 12 V supply branch; match its label here to the harness split in F25 and the destination module in S05.

## 8. CCM right side

Connections listed: **Starboard Motor, S.S., and Servo**.

The source says that the connected cables lead to cables fixed along the right-side wall. It does not provide separate cable labels or destination mappings for these three connections, and it does not define S.S.

### D08. Right-side cable routes

```mermaid
%% D08
flowchart LR
    subgraph right_ports["CCM right face"]
        motor["Starboard Motor"]
        ss["S.S."]
        servo["Servo"]
    end
    subgraph right_wall["Along the right-side wall<br/>Separate cable runs"]
        motor_run["Black motor lead"]
        ss_run["Yellow S.S. lead"]
        servo_run["Yellow Servo lead"]
    end
    motor_end["Motor cable endpoint<br/>not traced"]
    ss_end["S.S. endpoint<br/>not mapped"]
    servo_end["Servo endpoint<br/>not mapped"]
    motor --- motor_run
    ss --- ss_run
    servo --- servo_run
    motor_run -.- motor_end
    ss_run -.- ss_end
    servo_run -.- servo_end

    classDef equipment fill:#eff6ff,stroke:#2563eb,color:#172554;
    classDef harness fill:#ecfdf5,stroke:#047857,color:#064e3b;
    classDef unknown fill:#fff7ed,stroke:#9a3412,color:#7c2d12,stroke-dasharray:5 4;
    class motor,ss,servo equipment;
    class motor_run,ss_run,servo_run harness;
    class motor_end,ss_end,servo_end unknown;
```

Each port has its own cable run along the right-side wall. The route grouping does not join the motor, S.S., and Servo cables, and the remote devices remain unmapped.

**Photo references:** [F27](#figure-f27), [S07](#figure-s07), and [S10](#figure-s10).

<a id="figure-f27"></a>

![F27: CCM right-side connection panel](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/CCM%20right%20view.jpeg)

*Figure F27. CCM right-side connection panel.*

The annotated right-side view locates Starboard Motor, S.S., and Servo. The revised notes identify a black motor lead and yellow S.S. and Servo leads continuing along the right-side wall; S07 and S10 provide additional connector views.

The second photo under this heading in the original source repeats F18, which is retained in Section 7.3 as a wider routing reference. Figures S07 and S10 show additional views of the right-side connectors.

## 9. Additional reference photos

These photos supplement the main connection views with cable-label close-ups, unannotated originals, and additional angles. S11-S15 cover the newly supplied central-controller and TDM-E details. Descriptions follow the revised notes and visible features; endpoints that are not identified remain unspecified.

<a id="figure-s01"></a>

![S01: AUX12V OUT wiring without annotations](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/DC%2012V%20wiring.jpeg)

*Figure S01. AUX12V OUT wiring without annotations.*

This is the unannotated version of the wiring view used for F25. It preserves the unobscured cable and connector detail for comparison with the added 12 V branch markings.

<a id="figure-s02"></a>

![S02: CCM top panel without annotations](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/CCM%20top%20view.jpeg)

*Figure S02. CCM top panel without annotations.*

The unannotated top-panel view complements F16. It provides an additional reference for locating the top connectors and following the cables leaving the CCM.

<a id="figure-s03"></a>

![S03: CCM left-side connector detail](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/CCM%20left%20view%20%282%29.jpeg)

*Figure S03. CCM left-side connector detail.*

This additional left-side view complements F20 and the individual Port Motor, 5 GHz, and P.S. label photos. It records the local connector arrangement where several cables leave the same enclosure face.

<a id="figure-s04"></a>

![S04: P.S. route, first reference view](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/P.S%20route%201.jpeg)

*Figure S04. P.S. route, first reference view.*

The held yellow P.S. lead sits beside a large black inline connector and the cables secured along the compartment wall. Red and black power pairs and a red/green connector are also visible, providing context for separating the P.S. route from the adjacent power wiring.

<a id="figure-s05"></a>

![S05: GPS module on the boat lid](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/GPS%20module.jpeg)

*Figure S05. GPS module on the boat lid.*

The photo shows the white GPS module on the boat lid. It connects to the CCM top-panel GPS port through the white GPS cable and receives 12 V power from J3 on the AUX12V OUT harness. F17 shows the CCM cable route, and F25-F26 show the power-branch references.

<a id="figure-s06"></a>

![S06: 2.4 GHz cable-label detail](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/2.4%20GHz%20labelling.jpeg)

*Figure S06. 2.4 GHz cable-label detail.*

This close-up is the cable-identification reference for the CCM's 2.4 GHz connection. The notes associate the black lead with the 2.4GHZ and 2J labels and the external white antenna; the complete external route is not shown here.

<a id="figure-s07"></a>

![S07: CCM right-side detail, second view](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/CCM%20right%20view%20%282%29.jpeg)

*Figure S07. CCM right-side detail, second view.*

This angle supplements the annotated right-side panel in F27. It provides a closer reference for the connectors and outgoing cables associated with Starboard Motor, S.S., and Servo.

<a id="figure-s08"></a>

![S08: Battery wiring, second reference view](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/DC%2024V%20wirings%20%282%29%20.jpeg)

*Figure S08. Battery wiring, second reference view.*

The additional battery-area view complements F11, F12, and F14. It records the power harness and cable-label context used to identify the 24 V supply connections.

<a id="figure-s09"></a>

![S09: CCM rear panel, additional view](https://raw.githubusercontent.com/Wei-Yitong/pe/main/IMG_1468.jpeg)

*Figure S09. CCM rear panel, additional view.*

This additional angle shows the CCM rear face and its outgoing cable in the surrounding compartment. It complements F15 when locating the E-stop connection relative to the enclosure and nearby wiring.

<a id="figure-s10"></a>

![S10: CCM right-side detail, third view](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/CCM%20right%20view%20%283%29.jpeg)

*Figure S10. CCM right-side detail, third view.*

The STARBOARD MOTOR label sits above the large black plug, with the yellow S.S. and Servo leads attached to smaller adjacent connectors. The cables crossing the panel are held aside to expose the labels, making this a close reference for the connector order shown in F27.

<a id="figure-s11"></a>

![S11: Central controller connector close-up](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/Central%20component%20supplement%201.jpeg)

*Figure S11. Central controller connector close-up.*

The close view shows the CCM and Hydrolink right-angle plugs with their metal locking collars at the edge of the central controller. The yellow face carries the Forward and This Side Up orientation markings, with the TDM-E connection area nearby.

<a id="figure-s12"></a>

![S12: Central controller and branched CCM harness](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/Central%20component%20supplement%202.jpeg)

*Figure S12. Central controller and branched CCM harness.*

The harness is lifted to show its split in relation to the CCM and the central controller on the circular cover. This wider view supplements F05 by preserving the surrounding equipment and deck context.

<a id="figure-s13"></a>

![S13: Central Hydrolink and TDM-E routing detail](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/Central%20component%20supplement%203.jpeg)

*Figure S13. Central Hydrolink and TDM-E routing detail.*

This side view places the controller's Hydrolink lead and the TDM-E Serial port A-1 area in the same frame. Nearby inline power connectors and the CCM enclosure provide reference points for following the separate data and power cables.

<a id="figure-s14"></a>

![S14: TDM-E top panel, second view](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/TDM%20-%20E%20top%20view%202.jpeg)

*Figure S14. TDM-E top panel, second view.*

The second top view shows the TDM-labelled cable attached at Serial port A-1, the yellow cap on A-2, the Ethernet positions, and the capped USB connection. It also shows the 24V INPUT marking and the power conductors at the enclosure edge.

<a id="figure-s15"></a>

![S15: TDM-E Ethernet cable in the equipment compartment](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/TDM%20-%20E%20Ethernet.jpeg)

*Figure S15. TDM-E Ethernet cable in the equipment compartment.*

The wider view shows the connected Ethernet lead extending above the compartment, with TDM-E, the central controller, and the deck antennas in context. The cable's far-end device is outside the documented view, so its destination remains unspecified.

## 10. Image sources and duplicate handling

All photo links use absolute HTTPS image URLs, including the renamed files in the repository's `photo detailed` folder. Spaces, parentheses, and spaces immediately before a file extension are encoded in the URLs to preserve the exact filenames.

The reading copy contains **27 main figures and 15 supplementary figures**: all **40 photos** in `photo detailed`, the original Word component overview in F04, and the additional rear view in S09. F01 is the overall boat view, F02 the front overview, and F03 the back overview, matching the revised captions. F05-F08 use the newly supplied central-controller and TDM-E photos.

- [Photo inventory](sources/photo-inventory.csv): figure IDs, absolute image URLs, captions, descriptions, dimensions, and SHA-256 hashes. Repeated Word occurrences share the selected reading-copy figure.
- [Original Word transcription](sources/original-transcription.md): original wording and image order, including the earlier Word photos corresponding to F05-F08. Its historical TODOs and routing text have not been rewritten to match the revised notes.
- [Duplicate report](sources/duplicate-report.md): original repeated-photo groups and the current selection of renamed and additional photos.
