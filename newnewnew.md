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
- [10. Image sources](#10-image-sources)

## Diagram index

| Diagram | Connections shown |
| --- | --- |
| [D01. Main equipment and power](#d01-main-equipment-and-power) | Bow-to-stern equipment layout, all documented equipment ports, cable routes, and GPS power from J3. |
| [D02. Central data connections](#d02-central-data-connections) | Autonomy/Hydrolink harness, central controller, TDM-E, GPS cable, and J3 power feed. |
| [D03. 24 V supply branches](#d03-24-v-supply-branches) | Battery supply branches to CCM and TDM-E. |
| [D04. E-stop connection](#d04-e-stop-connection) | CCM rear connection and its undocumented remote termination. |
| [D05. Radio and sounder routes](#d05-radio-and-sounder-routes) | CCM top-panel 2.4 GHz and Sounder connections. |
| [D06. Left-side cable routes](#d06-left-side-cable-routes) | Port Motor, P.S., 5 GHz, and AUX12V OUT. |
| [D07. Auxiliary 12 V branches](#d07-auxiliary-12-v-branches) | J2, J3, and J4, including J3 supplying GPS power. |
| [D08. Right-side cable routes](#d08-right-side-cable-routes) | Starboard Motor, S.S., and Servo. |

**Reading the diagrams:** Solid lines show documented cable connections or routes. Dashed lines indicate a continuation whose exact route or destination is not recorded. Lines describe physical connections without specifying signal direction or pin assignments.

Blue identifies equipment and ports, green identifies harnesses and connectors, orange with a dashed border identifies unresolved routes or endpoints, and grey identifies capped ports. Harness nodes represent cable assemblies. Separate cables within a group remain separate cables.

## 1. Overview

The boat contains a Control and Communications Module (**CCM**), a central autonomy controller, a **TDM-E**, a GPS module, and their power and cable assemblies.

### D01. Main equipment and power

**Boat orientation:** Read from **bow / forward at the top** to **stern / aft at the bottom**, with **port on the left** and **starboard on the right** when looking toward the bow.

The overview photos show the CCM at the forward end of the equipment compartment. The central controller sits aft of the CCM on the circular cover, near the centreline. TDM-E sits farther aft on the controller’s starboard side.

```mermaid
%% D01
%%{init: {"flowchart": {"nodeSpacing": 18, "rankSpacing": 24, "padding": 10}}}%%
flowchart TB
    bow["BOW / FORWARD<br/>Top view: port left, starboard right"]
    stern["STERN / AFT<br/>Twin motor assemblies"]
    batteries["Three-battery supply<br/>Position schematic"]
    power["24 V supply<br/>harness"]

    subgraph ccm["CCM - forward compartment"]
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

    subgraph central["Central controller - circular cover / mid compartment"]
        central_ccm["CCM<br/>socket"]
        central_hydro["Hydrolink<br/>socket"]
    end

    subgraph tdm["TDM-E - aft / starboard"]
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
    gps_module["GPS module on hatch lid<br/>Lid position varies"]

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

    %% Invisible links control layout only; they are not cables.
    bow ~~~ ccm_power
    ccm_power ~~~ autonomy
    autonomy ~~~ hydro_ccm
    hydro_ccm ~~~ gps_port
    gps_port ~~~ radio24
    radio24 ~~~ sounder
    sounder ~~~ port_motor
    port_motor ~~~ ps
    ps ~~~ radio5
    radio5 ~~~ aux
    aux ~~~ starboard_motor
    starboard_motor ~~~ ss
    ss ~~~ servo
    servo ~~~ estop
    estop ~~~ central_ccm
    central_ccm ~~~ central_hydro
    central_hydro ~~~ tdm_power
    tdm_power ~~~ serial_a1
    serial_a1 ~~~ serial_a2
    serial_a2 ~~~ ethernet
    ethernet ~~~ ethernet_cap_a
    ethernet_cap_a ~~~ ethernet_cap_b
    ethernet_cap_b ~~~ usb
    usb ~~~ stern

    classDef equipment fill:#eff6ff,stroke:#2563eb,color:#172554;
    classDef harness fill:#ecfdf5,stroke:#047857,color:#064e3b;
    classDef unknown fill:#fff7ed,stroke:#9a3412,color:#7c2d12,stroke-dasharray:5 4;
    classDef capped fill:#f1f5f9,stroke:#64748b,color:#334155;
    classDef orientation fill:#f8fafc,stroke:#94a3b8,color:#334155;

    class batteries,ccm_power,estop,autonomy,hydro_ccm,gps_port,radio24,sounder,port_motor,ps,radio5,aux,starboard_motor,ss,servo,central_ccm,central_hydro,tdm_power,serial_a1,ethernet,gps_module equipment;
    class power,data_harness,aux_harness,j3 harness;
    class serial_a2,ethernet_cap_a,ethernet_cap_b,usb capped;
    class j2,j4,estop_end,radio24_end,sounder_end,port_motor_end,ps_end,radio5_end,starboard_end,ss_end,servo_end,ethernet_end unknown;
    class bow,stern orientation;
```

This map includes all **14 CCM connections**, both central-controller sockets, and the TDM-E’s **seven port positions**.

The equipment order follows the overview photos. Enclosures and port rows are expanded for readability and are **not to scale**. CCM port rows identify enclosure faces rather than forming a measured projection of those faces. Unresolved endpoint boxes are routing callouts, not fixed installation positions.

The GPS is mounted on a movable hatch lid. The overview photos do not establish the battery assembly’s exact hull position. The controller’s power connection and the interconnection of the three batteries are not specified in the notes.

**Photo references:** [F01](#figure-f01), [F02](#figure-f02), [F03](#figure-f03), and [F04](#figure-f04).

<a id="figure-f01"></a>

![F01: Overall boat layout](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/boat%20overview.jpeg)

*Figure F01. Overall boat layout.*

The full-boat view locates the open equipment compartment within the yellow hull. The CCM is forward in the compartment, the central controller occupies the circular cover, and TDM-E sits aft on its starboard side. The deck antennas and twin rear motor assemblies provide orientation.

<a id="figure-f02"></a>

![F02: Front overview of the equipment compartment](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/boat%20overview%20front.jpeg)

*Figure F02. Front overview of the equipment compartment.*

This view shows the CCM beside the central controller and the crossing white and black leads. It provides context for the separate Autonomy, GPS, and Hydrolink cable routes.

<a id="figure-f03"></a>

![F03: Back overview of the equipment compartment](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/boat%20overview%20back.jpeg)

*Figure F03. Back overview of the equipment compartment.*

TDM-E is visible on its foam support with a retaining strap, adjacent to the central controller. Its serial and Ethernet connections can be compared with the close-ups below.

## 2. Central components

### 2.1 Central component: CCM / Hydrolink

The central component is the yellow-faced **MSubs Z-Boat Autonomy Controller**, mounted on the circular cover between the CCM and TDM-E. Its two labelled connections are **CCM** and **Hydrolink**.

| Central controller connection | Cable route | Photo reference |
| --- | --- | --- |
| CCM | A branched harness links this socket to both Autonomy and Hydrolink on the CCM module. Its branches are labelled CCM AUTONOMY and CCM HYDROLINK. | F05; S12 |
| Hydrolink | A separate black lead connects this socket to TDM-E Serial port A-1. The TDM-E end is labelled TDM. | F06; S13 |

The CCM module’s Hydrolink connection is part of the harness entering the central controller’s **CCM socket**. The controller’s own **Hydrolink socket** continues separately to TDM-E.

### D02. Central data connections

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

    gps["GPS module<br/>on hatch lid"]
    network["Ethernet far-end device<br/>Not identified"]

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

The central-controller group shows both sockets without assigning an internal electrical connection between them.

The **GPS module receives 12 V power from J3**, alongside its white GPS cable connection to the CCM top panel. See D07 for all three auxiliary power branches.

<a id="figure-f04"></a>

![F04: Central component overview](https://raw.githubusercontent.com/Wei-Yitong/pe/main/docs/wire-connections/assets/word-image09.jpg)

*Figure F04. Central component overview.*

The original Word overview shows the central controller between the CCM and TDM-E, with a labelled 24 V lead crossing the circular cover.

<a id="figure-f05"></a>

![F05: Central component CCM cable routing](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/central%20component%20CCM.jpg)

*Figure F05. Central component CCM cable routing.*

The lifted branched harness links the controller’s CCM socket to the CCM module’s Autonomy and Hydrolink connections. The pale branch carries CCM AUTONOMY and the black branch carries CCM HYDROLINK. The controller end uses a right-angle plug with a metal locking collar.

<a id="figure-f06"></a>

![F06: Central component Hydrolink cable routing](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/central%20component%20Hydrolink.jpg)

*Figure F06. Central component Hydrolink cable routing.*

The black lead from the controller’s Hydrolink socket loops toward TDM-E Serial port A-1. The cable at the TDM-E end is labelled TDM.

### 2.2 TDM-E

TDM-E sits beside the central controller on a foam support.

| Connection | Description / routing | Photo reference |
| --- | --- | --- |
| Ethernet | Three panel positions are visible, with one cable attached and two capped. The far-end device is unidentified. | F07; S14; S15 |
| Serial port A-1 | Connected to the central controller’s Hydrolink socket through the black lead labelled TDM. | F06; F07 |
| Serial port A-2 | Covered by a yellow cap. | F07; S14 |
| USB | Covered by a black tethered cap. | F08; S14 |
| 24 V input | Supplied by a branch of the battery supply harness. Red and green conductors enter through the side gland beside the ON/OFF switch. | F08; F13 |

<a id="figure-f07"></a>

![F07: TDM-E connection panel](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/TDM%20-E%20top%20view.jpeg)

*Figure F07. TDM-E connection panel.*

The panel shows three Ethernet positions, capped USB, Serial A-1 with the TDM-labelled lead attached, and Serial A-2 under a yellow cap. A black strap secures the unit against its foam support.

<a id="figure-f08"></a>

![F08: TDM-E power-entry detail](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/TDM%20-%20E%20powering.jpeg)

*Figure F08. TDM-E power-entry detail.*

Red and green conductors enter the enclosure through its side gland beside the ON/OFF switch. The 24V INPUT marking and adjacent serial, USB, and Ethernet connections identify the power-entry area.

## 3. CCM connection index

“Front,” “rear,” “top,” “left,” and “right” follow the enclosure-face labels in the source notes. Motor names use the source’s port/starboard terminology.

| CCM face | Port / connection | Cable label(s) | Routing / notes |
| --- | --- | --- | --- |
| Front | 24Volt IN | 24 V cable assembly | Receives a branch of the battery supply; the other branch supplies TDM-E. |
| Rear | E-stop | Not specified | Identified in the notes as the connection used to stop the propellers. |
| Top | Autonomy | CCM AUTONOMY | White lead; joins the harness to the central controller’s CCM socket. |
| Top | GPS | GPS | White cable to the GPS module on the hatch lid. The module also receives 12 V power from J3. |
| Top | Hydrolink | CCM HYDROLINK | Black lead; joins the same central-controller CCM harness as Autonomy. |
| Top | 2.4 GHz | 2.4GHZ; 2J | Black cable; reported route to the external white stick and external 2J. |
| Top | Sounder | Not specified | Listed; routing is undocumented. |
| Left | 5 GHz | 5G | Black cable; remote endpoint unspecified. |
| Left | Port Motor | Left port motor | Black cable; follows the left-side wall. |
| Left | P.S. | Left P.S. | Yellow cable; follows the left-side wall toward the end of the boat. |
| Left | AUX12V OUT | 12V; J2; J3; J4 | Three branches. J3 supplies 12 V to GPS; J2 and J4 loads are unspecified. |
| Right | Starboard Motor | Not specified | Black cable; follows the right-side wall. |
| Right | S.S. | Not specified | Yellow cable; follows the right-side wall. |
| Right | Servo | Not specified | Yellow cable; follows the right-side wall. |

## 4. CCM front: 24 V input

The CCM front face carries **24VOLT IN**.

<a id="figure-f09"></a>

![F09: CCM front face and 24 V input](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/CCM%20Front%20view%20.jpeg)

*Figure F09. CCM front face and 24 V input.*

The annotated view identifies the front face and its power entry. Red and black leads pass through the front cable gland.

### 4.1 Cable branching

The notes describe a 24 V supply harness from the three batteries, with branches to:

1. TDM-E’s 24 V input.
2. The CCM’s front-face 24VOLT IN connection.

### D03. 24 V supply branches

```mermaid
%% D03
flowchart LR
    batteries["Three batteries<br/>Interconnection not specified"]
    supply["24 V supply harness<br/>Two documented branches"]
    tdm_power["TDM-E 24 V input<br/>Side gland by ON/OFF switch"]
    ccm_power["CCM 24VOLT IN<br/>Front-face gland"]

    batteries --- supply
    supply ---|"Branch to TDM-E<br/>24 V cable 1 in F13"| tdm_power
    supply ---|"Branch to CCM<br/>Input leads in F09-F10"| ccm_power

    classDef equipment fill:#eff6ff,stroke:#2563eb,color:#172554;
    classDef harness fill:#ecfdf5,stroke:#047857,color:#064e3b;

    class batteries,tdm_power,ccm_power equipment;
    class supply harness;
```

The diagram records the two reported destinations. It does not specify how the three batteries are interconnected.

### 4.2 Connection photos

<a id="figure-f10"></a>

![F10: CCM 24 V input cable detail](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/DC%2024V%20front%20view.jpeg)

*Figure F10. CCM 24 V input cable detail.*

This closer annotated view follows the red and black input leads and their inline connectors. The 24 V label and Forward annotation identify the supply connection.

<a id="figure-f11"></a>

![F11: 24 V wiring near the batteries](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/DC%2024V%20wirings.jpeg)

*Figure F11. 24 V wiring near the batteries.*

The view records power-cable connections in the battery area. Compare it with F14 when following the supply harness toward the CCM and TDM-E branches.

<a id="figure-f12"></a>

![F12: Battery power-connection close-up](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/DC%2024%20wirings%20%283%29.jpeg)

*Figure F12. Battery power-connection close-up.*

This close-up supplements F11 by showing battery-area leads and connector positions in greater detail. The photograph does not establish a series or parallel battery arrangement.

<a id="figure-f13"></a>

![F13: 24 V cable branch toward TDM-E](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/DC%2024V%20TDM-E%20powering.jpeg)

*Figure F13. 24 V cable branch toward TDM-E.*

The lead identified as 24 V cable 1 is lifted above the circular cover. Its red/black pair and red/green connector housings identify the branch reported as supplying TDM-E. F08 shows the device’s power-entry end.

<a id="figure-f14"></a>

![F14: Battery connections and 24 V cable 2](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/DC%2024V%20battery%20connections.jpeg)

*Figure F14. Battery connections and 24 V cable 2.*

The annotated view shows the strapped battery assembly and paired power connectors. The 24 V cable 2 annotation and Charge Terminal / Discharge Terminal tags distinguish the battery-area connections.

## 5. CCM rear: E-stop

The notes identify the rear E-stop connection as being used to stop the propellers. Its remote termination and pin assignment are not recorded.

### D04. E-stop connection

```mermaid
%% D04
flowchart LR
    rear["CCM rear face<br/>E-stop connection"]
    cable["Cable identified as E-stop"]
    termination["Remote termination<br/>Not recorded"]

    rear --- cable
    cable -.- termination

    classDef equipment fill:#eff6ff,stroke:#2563eb,color:#172554;
    classDef harness fill:#ecfdf5,stroke:#047857,color:#064e3b;
    classDef unknown fill:#fff7ed,stroke:#9a3412,color:#7c2d12,stroke-dasharray:5 4;

    class rear equipment;
    class cable harness;
    class termination unknown;
```

<a id="figure-f15"></a>

![F15: CCM rear face and E-stop cable](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/CCM%20rear%20view.jpeg)

*Figure F15. CCM rear face and E-stop cable.*

The rear view locates the E-stop connection and its cable exit. S09 provides another angle of this area.

## 6. CCM top panel

The listed top-panel connections are **2.4 GHz, Sounder, Autonomy, GPS, and Hydrolink**.

### D05. Radio and sounder routes

Autonomy, GPS, and Hydrolink are expanded in D02.

```mermaid
%% D05
flowchart LR
    subgraph top["CCM top panel"]
        radio["2.4 GHz"]
        sounder["Sounder"]
    end

    radio_lead["Black cable<br/>2.4GHZ / 2J labels"]
    external["Reported: external white stick<br/>and external 2J<br/>Exact route not recorded"]
    sounder_end["Sounder cable / endpoint<br/>Not documented"]

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

The white-stick and 2J references are kept together because the notes do not describe a splitter or map individual branches to those destinations.

<a id="figure-f16"></a>

![F16: CCM top panel with connection annotations](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/CCM%20top%20view%20with%20wording.jpeg)

*Figure F16. CCM top panel with connection annotations.*

The annotated panel provides the location reference for the listed top connections. F19 and S06 supply closer cable-identification views.

### 6.1 Autonomy, GPS, and Hydrolink

| Port | Cable label and route |
| --- | --- |
| Autonomy | White lead labelled CCM AUTONOMY; joins the central controller’s CCM harness. |
| GPS | White lead labelled GPS; connects to the module on the hatch lid. The module’s 12 V power comes from J3. |
| Hydrolink | Black lead labelled CCM HYDROLINK; joins the same central-controller CCM harness as Autonomy. |

The original source heading “HDMI Outputs” has not been verified as an interface-type description.

<a id="figure-f17"></a>

![F17: GPS cable route at the CCM](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/GPS%20module%20wiring.jpeg)

*Figure F17. GPS cable route at the CCM.*

This view records the white GPS cable at the CCM and its route toward the module on the lid. The module also receives 12 V from J3 on the AUX12V OUT harness; D02 shows both connections.

<a id="figure-f19"></a>

![F19: CCM top-panel connectors and cable labels](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/CCM%204%20Inputs.jpeg)

*Figure F19. CCM top-panel connectors and cable labels.*

This close-up groups the top connectors and labels. Autonomy and Hydrolink join the central controller’s CCM harness; GPS follows its separate module connection.

### 6.2 2.4 GHz

The notes describe a black cable labelled **2.4GHZ** and **2J**, associated with an external white stick and external 2J. The exact routing and meaning of 2J are not established.

S06 is the dedicated cable-label reference. The original Word document repeated the battery photo F14 beneath this heading; that placement does not establish a radio connection.

### 6.3 Sounder

Sounder is listed on the top panel. A separate cable-label and routing description is not available.

## 7. CCM left side

The four left-face connections are **5 GHz, Port Motor, P.S., and AUX12V OUT**.

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
    gps_module["GPS module on hatch lid"]

    motor_end["Motor cable endpoint<br/>Not traced"]
    ps_end["Reported: toward end of boat<br/>Exact termination not recorded"]
    radio_end["5 GHz endpoint<br/>Not specified"]

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

Port Motor and P.S. follow the left side as separate cable runs. AUX12V OUT divides into J2, J3, and J4; **J3 powers the GPS module**.

<a id="figure-f20"></a>

![F20: CCM left-side connection panel](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/CCM%20left%20view.jpeg)

*Figure F20. CCM left-side connection panel.*

The annotated view locates all four left-face connections. The following close-ups identify their cable labels.

### 7.1 Port Motor

The black cable labelled **Left port motor** follows the left-side wall. The complete connection to its remote motor endpoint is not traced in the photographs.

<a id="figure-f21"></a>

![F21: Port Motor connection and cable label](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/Left%20port%20motor%20labelling.jpeg)

*Figure F21. Port Motor connection and cable label.*

The close-up identifies the black motor lead and its local connector, distinguishing it from the adjacent yellow P.S. cable.

### 7.2 5 GHz

The 5 GHz connection uses a black cable labelled **5G**. Its remote endpoint is unspecified.

<a id="figure-f22"></a>

![F22: 5 GHz connection and cable label](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/5G%20labelling.jpeg)

*Figure F22. 5 GHz connection and cable label.*

This view records the local 5 GHz connector and 5G cable identification.

### 7.3 P.S.

The yellow cable labelled **Left P.S.** connects to the P.S. port and follows the left-side wall toward the end of the boat.

The revised notes also mention **Right P.S.**, but do not assign that label to a separate connector. It is not assigned to this left-face port.

<a id="figure-f23"></a>

![F23: P.S. connection and Left P.S. label](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/P.S%20labelling.jpeg)

*Figure F23. P.S. connection and Left P.S. label.*

The yellow lead enters the small connector beneath the P.S. marking, and its held tag reads Left P.S. The adjacent 5 GHz connector helps locate it on the enclosure.

<a id="figure-f18"></a>

![F18: Cable routing beside the CCM](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/CCM%20P.S%20connections.jpeg)

*Figure F18. Cable routing beside the CCM.*

The wider view records cables passing beside the CCM and continuing along the compartment wall. Compare it with the labelled P.S. connector in F23.

<a id="figure-f24"></a>

![F24: P.S. route, second reference view](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/P.s%20route%202.jpeg)

*Figure F24. P.S. route, second reference view.*

This angle complements the label close-up and the first route view S04, documenting the cable area along the left-side route.

### 7.4 AUX12V OUT

The cable labelled **12V** splits into **J2, J3, and J4**, with red and green connector ends.

**J3 supplies 12 V power to the GPS module on the hatch lid.** The same GPS module also has the white GPS cable connection to the CCM top panel. J2 and J4 loads are unspecified.

### D07. Auxiliary 12 V branches

```mermaid
%% D07
flowchart LR
    aux["CCM left face<br/>AUX12V OUT"]
    split["Three-branch cable assembly"]
    j2["J2<br/>Red / green connector ends"]
    j3["J3<br/>Red / green connector ends"]
    j4["J4<br/>Red / green connector ends"]
    gps_module["GPS module on hatch lid"]

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

J2, J3, and J4 identify branch connectors. J3 powers GPS; the connected loads on J2 and J4 remain unspecified. Connector pin polarity is not documented.

<a id="figure-f25"></a>

![F25: AUX12V OUT cable split with annotations](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/DC%2012V%20wiring%20with%20words.jpeg)

*Figure F25. AUX12V OUT cable split with annotations.*

The annotated view identifies the auxiliary power harness and its three branches. J3 supplies GPS power; F26 provides branch-label detail and S05 shows the module.

<a id="figure-f26"></a>

![F26: AUX12V OUT branch labels and connectors](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/DC%2012v%20wiring%20labelled.jpeg)

*Figure F26. AUX12V OUT branch labels and connectors.*

This close-up records the 12V, J2, J3, and J4 identifiers and connector ends. Match J3’s label to the split in F25 and its GPS destination in S05.

## 8. CCM right side

The right-face connections are **Starboard Motor, S.S., and Servo**. Their cables follow the right-side wall as separate runs.

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

    motor_end["Motor cable endpoint<br/>Not traced"]
    ss_end["S.S. endpoint<br/>Not mapped"]
    servo_end["Servo endpoint<br/>Not mapped"]

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

The route grouping does not join the three cables. Their remote device mappings and the meaning of S.S. are not specified in the notes.

<a id="figure-f27"></a>

![F27: CCM right-side connection panel](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/CCM%20right%20view.jpeg)

*Figure F27. CCM right-side connection panel.*

The annotated panel locates Starboard Motor, S.S., and Servo. S07 and S10 provide additional connector views.

## 9. Additional reference photos

These views supplement the principal connection photos with unannotated originals, cable-label details, and additional equipment angles.

<a id="figure-s01"></a>

![S01: AUX12V OUT wiring without annotations](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/DC%2012V%20wiring.jpeg)

*Figure S01. AUX12V OUT wiring without annotations.*

The unannotated version of F25 preserves unobscured cable and connector details.

<a id="figure-s02"></a>

![S02: CCM top panel without annotations](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/CCM%20top%20view.jpeg)

*Figure S02. CCM top panel without annotations.*

This view complements F16 when locating top connectors and following outgoing leads.

<a id="figure-s03"></a>

![S03: CCM left-side connector detail](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/CCM%20left%20view%20%282%29.jpeg)

*Figure S03. CCM left-side connector detail.*

The additional angle records the local arrangement where multiple cables leave the left face.

<a id="figure-s04"></a>

![S04: P.S. route, first reference view](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/P.S%20route%201.jpeg)

*Figure S04. P.S. route, first reference view.*

The held yellow lead sits beside a large black inline connector and wall-secured cables. Nearby red/black power pairs distinguish the P.S. route from adjacent power wiring.

<a id="figure-s05"></a>

![S05: GPS module on the hatch lid](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/GPS%20module.jpeg)

*Figure S05. GPS module on the hatch lid.*

The GPS module connects to the CCM top GPS port through the white lead and receives 12 V power from AUX12V OUT branch J3. Its lid-mounted position moves when the hatch is opened.

<a id="figure-s06"></a>

![S06: 2.4 GHz cable-label detail](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/2.4%20GHz%20labelling.jpeg)

*Figure S06. 2.4 GHz cable-label detail.*

The close-up identifies the cable associated with the 2.4GHZ and 2J references. Its complete external route is not shown.

<a id="figure-s07"></a>

![S07: CCM right-side detail, second view](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/CCM%20right%20view%20%282%29.jpeg)

*Figure S07. CCM right-side detail, second view.*

This angle supplements F27 with closer views of the right-face connectors and outgoing leads.

<a id="figure-s08"></a>

![S08: Battery wiring, second reference view](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/DC%2024V%20wirings%20%282%29%20.jpeg)

*Figure S08. Battery wiring, second reference view.*

The additional battery-area view records power-harness and cable-label context for the 24 V connections.

<a id="figure-s09"></a>

![S09: CCM rear panel, additional view](https://raw.githubusercontent.com/Wei-Yitong/pe/main/IMG_1468.jpeg)

*Figure S09. CCM rear panel, additional view.*

Another angle shows the rear face and outgoing cable in the surrounding compartment. It complements the E-stop view in F15.

<a id="figure-s10"></a>

![S10: CCM right-side detail, third view](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/CCM%20right%20view%20%283%29.jpeg)

*Figure S10. CCM right-side detail, third view.*

The STARBOARD MOTOR label sits above the large black plug, beside the smaller connectors with yellow S.S. and Servo leads. Crossing cables are held aside to expose the labels.

<a id="figure-s11"></a>

![S11: Central controller connector close-up](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/Central%20component%20supplement%201.jpeg)

*Figure S11. Central controller connector close-up.*

The view shows CCM and Hydrolink right-angle plugs and their metal locking collars. Forward and This Side Up markings establish the controller’s orientation.

<a id="figure-s12"></a>

![S12: Central controller and branched CCM harness](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/Central%20component%20supplement%202.jpeg)

*Figure S12. Central controller and branched CCM harness.*

The lifted harness exposes its split relative to the CCM module and central controller. This wider view supplements F05.

<a id="figure-s13"></a>

![S13: Central Hydrolink and TDM-E routing detail](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/Central%20component%20supplement%203.jpeg)

*Figure S13. Central Hydrolink and TDM-E routing detail.*

The controller’s Hydrolink lead and TDM-E Serial A-1 area appear in the same frame. Nearby power connectors provide reference points for separating the data and power routes.

<a id="figure-s14"></a>

![S14: TDM-E top panel, second view](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/TDM%20-%20E%20top%20view%202.jpeg)

*Figure S14. TDM-E top panel, second view.*

This angle shows the attached TDM-labelled A-1 cable, yellow A-2 cap, Ethernet positions, capped USB, and 24V INPUT marking.

<a id="figure-s15"></a>

![S15: TDM-E Ethernet cable in the equipment compartment](https://raw.githubusercontent.com/Wei-Yitong/pe/main/photo%20detailed/TDM%20-%20E%20Ethernet.jpeg)

*Figure S15. TDM-E Ethernet cable in the equipment compartment.*

The wider view shows the Ethernet lead extending above the compartment, with TDM-E, the central controller, and deck antennas in context. The far-end device is not identified.

## 10. Image sources

All photo references use absolute HTTPS URLs from the `Wei-Yitong/pe` repository. Spaces, parentheses, and spaces immediately before file extensions are URL-encoded to preserve the exact filenames.

The document contains **27 main figures and 15 supplementary figures**, including all **40 photos** in the `photo detailed` folder. The two other images are the original Word component overview F04 and the original repository rear view S09.

Annotated versions, unannotated originals, and distinct camera angles are retained where they provide additional information. The diagrams combine the revised connection notes with the photo references; unresolved routes remain explicitly marked.
