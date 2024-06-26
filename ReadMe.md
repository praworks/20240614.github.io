# Coil Information

## Description

The provided code processes a string containing information about a coil and extracts key-value pairs representing various characteristics of the coil. Each line of the input string corresponds to a specific attribute of the coil, and the code splits these lines into key-value pairs based on a predefined pattern. The keys represent the attributes of the coil, such as type, dimensions, current density, etc., while the values represent the corresponding data associated with each attribute.

## Output

```javascript
[
  { key: '<span style="color: blue;">Type of Coil......</span>', data: '<span style="color: green;">AL-Layer-Rect</span>' },
  { key: '<span style="color: blue;">Coil-Length.......</span>', data: '<span style="color: green;">316.000 mm</span>' },
  { key: '<span style="color: blue;">Cond Mec/ELEC LGTH</span>', data: '<span style="color: green;">292.000 x  280.800</span>' },
  ...
]

Contents:
Section 1: GENERAL INFORMATION
Section 2: STACKED CORE
Section 3: LOW VOLTAGE WINDING
Section 4: HIGH VOLTAGE WINDING
Section 5: ELECTRICAL CLEARANCES
Section 6: BASIS FOR CALCULATIONS & MATERIAL PRICES
Section 7: WEIGHTS, DIMENSIONS, AND COOLING
Section 8: PRICE & COST
Section 9: PERFORMANCE DATA
Section 10: NOTES

https://praworks.github.io/TrafoPro.github.io/

-----------------------------------------------------------------------------------------------------------------------
Description:
The provided code processes a string containing information about a coil and extracts key-value pairs representing various characteristics of the coil. Each line of the input string corresponds to a specific attribute of the coil, and the code splits these lines into key-value pairs based on a predefined pattern. The keys represent the attributes of the coil, such as type, dimensions, current density, etc., while the values represent the corresponding data associated with each attribute.

const inputString = 
`| Type of Coil......:   AL-Layer-Rect     | Coil-Length.......:          316.000 mm | Cond Mec/ELEC LGTH:  292.000 x  280.800 |
     | TURNS PER COIL....:       72.0          | Inside Dimensions.: 131.000 x188.732 mm | Cond Dim: Rad/Ax..:   4.500 x 11.500 mm |
     | CURRENT DENSITY...:        1.351 A/mm2  | Outside Dimensions: 160.814 x218.546 mm | Cond/Lead Weight..:   17.00 /   0.23 kg |
     |                                         | Inner Perimeter...:      526.0 mm       |                                         |
     | Cooling Ducts Tk/#:    0.000 mm / 0.00  | Rad Blds (H,Leg,L): 14.91/ 14.91/ 14.91 | Lay/Trn/Duc Wts...:  0.24/  0.34/  0.00 |
     | Eff No Cool Ducts.: HV: 0 Leg: 0 LV: 0  | Axial Allowance...:            0.000 mm | Total Insul Weight:             0.59 kg |
     | Short-Circuit Curr:           3150 Amp. | Num Support Sticks:           12        |                                         |
     | Mean Turn Length..:         572.845 mm  | Lead:    Wd / Tk..:  11.700 /  4.700 mm | Total Coil Weight.:            17.82 kg |
     | Max Turn Lth Buckl:         4834.992 mm | Bus Bar: Wd / Tk..:  25.000 /  3.000 mm |                                         |
     | # Lay: Max/Min tpl:    3 : 24.0/ 24.0   | Layer/Turn Ins Bd.:   0.180/   0.200 mm | No Strs-Rad x Ax..:       1 x    1      |
     | T-RISE/GRADIENT...:     26.0/ 9.9 deg C | Watts/sq m .......:          529.788    | Resistance (Coil).: 0.028058 @ 75 C     |
     | Turn CSA .........:          50.892 mm2 |                                         | Conductor Dims....: Specified Size      |`;

// Split the input string into an array of values
const values = inputString.split('|').map(value => value.trim()).filter(value => value !== '');

// Extract relevant information and store them in an array
const coilInfoArray = values.map(value => {
    const parts = value.match(/(.{1,18}):\s*(.+)/); // Adjusting the regular expression to properly capture key and data
    const key = parts[1].trim();
    const data = parts[2].trim();
    
    let individualValues;
    if (data.includes('/')) {
        individualValues = data.split(':')[1].trim().split('/').map(value => value.trim());
    } else {
        individualValues = [data.trim()];
    }

    return { key, data: individualValues };
});

console.log(coilInfoArray);

[
  { key: 'Type of Coil......', data: 'AL-Layer-Rect' },
  { key: 'Coil-Length.......', data: '316.000 mm' },
  { key: 'Cond Mec/ELEC LGTH', data: '292.000 x  280.800' },
  { key: 'TURNS PER COIL....', data: '72.0' },
  { key: 'Inside Dimensions.', data: '131.000 x188.732 mm' },
  { key: 'Cond Dim: Rad/Ax..', data: '4.500 x 11.500 mm' },
  { key: 'CURRENT DENSITY...', data: '1.351 A/mm2' },
  { key: 'Outside Dimensions', data: '160.814 x218.546 mm' },
  { key: 'Cond/Lead Weight..', data: '17.00 /   0.23 kg' },
  { key: 'Inner Perimeter...', data: '526.0 mm' },
  { key: 'Cooling Ducts Tk/#', data: '0.000 mm / 0.00' },
  { key: 'Rad Blds (H,Leg,L)', data: '14.91/ 14.91/ 14.91' },
  { key: 'Lay/Trn/Duc Wts...', data: '0.24/  0.34/  0.00' },
  { key: 'Eff No Cool Ducts.', data: 'HV: 0 Leg: 0 LV: 0' },
  { key: 'Axial Allowance...', data: '0.000 mm' },
  { key: 'Total Insul Weight', data: '0.59 kg' },
  { key: 'Short-Circuit Curr', data: '3150 Amp.' },
  { key: 'Num Support Sticks', data: '12' },
  { key: 'Mean Turn Length..', data: '572.845 mm' },
  { key: 'Lead:    Wd / Tk..', data: '11.700 /  4.700 mm' },
  { key: 'Total Coil Weight.', data: '17.82 kg' },
  { key: 'Max Turn Lth Buckl', data: '4834.992 mm' },
  { key: 'Bus Bar: Wd / Tk..', data: '25.000 /  3.000 mm' },
  { key: '# Lay: Max/Min tpl', data: '3 : 24.0/ 24.0' },
  { key: 'Layer/Turn Ins Bd.', data: '0.180/   0.200 mm' },
  { key: 'No Strs-Rad x Ax..', data: '1 x    1' },
  { key: 'T-RISE/GRADIENT...', data: '26.0/ 9.9 deg C' },
  { key: 'Watts/sq m .......', data: '529.788' },
  { key: 'Resistance (Coil).', data: '0.028058 @ 75 C' },
  { key: 'Turn CSA .........', data: '50.892 mm2' },
  { key: 'Conductor Dims....', data: 'Specified Size' }
]
-----------------------------------------------------------------------------------------------------------------------


const inputString = 
`     Data File Name: D:\LTLTrafoDesign\ReportVB.dat
 
     *** Using Standard Data from Files;   Using New LTL Core Loss Calculations ***
 
     DATE: 2024.03.05                           LIQUID TYPE TRANSFORMER CALCULATION (Version 6.10.0)               Time: 13:18:50
     
     ORDER : 5011420       DESIGN: Data Set 1    ENGINEER: Navodya         CUSTOMER NAME: KPLC 2022                               
     KVA -     50  Liquid Type      ONAN Cooling    52 C Rise     Three Phase     50 Hz     Style Number: None                    
     HV : 11000 + 2- 2x 2.50 %  TC: Off-Load Tap Changer                  BIL:  95 (Delta)   Line/Coil Amps:    2.624/   1.515
     LV :   420                                                           BIL:   3  (Wye)    Line/Coil Amps:   68.732/  68.732
     |------------------------------------------------ S T A C K E D    C O R E -------------------- Width -- Build ----- Weight --|
     | Core Design.......:  OVAL-IY  Mitered   | Diagonal Dimension:120.000 x 177.232 mm | Step 1:  120.000,  57.232 mm   123.0 kg |
     | Grade/Frame Type..: 23ZDKH / 3-Leg      | Window Height.....:          336.000 mm | Step 2:  100.000,  66.470 mm   116.1 kg |
     | INDUCTION.........:        1.000 Tesla  | Center to Center..:          265.641 mm | Step 3:   70.000,  31.050 mm    38.0 kg |
     | VPT, W/kg, PBase..:  3.368, 0.332, 0.248| Gross/Net CSA.....:   156.9 / 151.7 cm2 | Step 4:    0.000,   0.000 mm     0.0 kg |
     | 100 % Exc Current.:        0.6395       | Weight of Core-Leg:            149.0 kg | Step 5:    0.000,   0.000 mm     0.0 kg |
     | Sound/Natural Freq:  35.3 db /  1296 Hz | Weight of Yoke....:            117.0 kg | Step 6:    0.000,   0.000 mm     0.0 kg |
     | Peak HV Inrush Cur:       16 amp        | Core Net Weight...:            264.4 kg | Step 7:    0.000,   0.000 mm     0.0 kg |
     | Utilization Factor:        0.8631       | Core Scrap Weight.:             11.0 kg | Step 8:    0.000,   0.000 mm     0.0 kg |
     | Standard Core No..:  NONE STANDARD      | Core Gross Weight.:            275.5 kg | Step 9:    0.000,   0.000 mm     0.0 kg |
     | Ovality Factor....:         1.290       |    Use Max Steel Width (Steps minus 1)  |         Using Std Steel Widths          |
     | Core Perimeter....:         491.5 mm    | Delta Build.......:             57.2 mm |                                         |
     |------------------------------------------  L O W   V O L T A G E   W I N D I N G   -----------------------------------------|
     | Type of Coil......:   AL-Layer-Rect     | Coil-Length.......:          316.000 mm | Cond Mec/ELEC LGTH:  292.000 x  280.800 |
     | TURNS PER COIL....:       72.0          | Inside Dimensions.: 131.000 x188.732 mm | Cond Dim: Rad/Ax..:   4.500 x 11.500 mm |
     | CURRENT DENSITY...:        1.351 A/mm2  | Outside Dimensions: 160.814 x218.546 mm | Cond/Lead Weight..:   17.00 /   0.23 kg |
     |                                         | Inner Perimeter...:      526.0 mm       |                                         |
     | Cooling Ducts Tk/#:    0.000 mm / 0.00  | Rad Blds (H,Leg,L): 14.91/ 14.91/ 14.91 | Lay/Trn/Duc Wts...:  0.24/  0.34/  0.00 |
     | Eff No Cool Ducts.: HV: 0 Leg: 0 LV: 0  | Axial Allowance...:            0.000 mm | Total Insul Weight:             0.59 kg |
     | Short-Circuit Curr:           3150 Amp. | Num Support Sticks:           12        |                                         |
     | Mean Turn Length..:         572.845 mm  | Lead:    Wd / Tk..:  11.700 /  4.700 mm | Total Coil Weight.:            17.82 kg |
     | Max Turn Lth Buckl:         4834.992 mm | Bus Bar: Wd / Tk..:  25.000 /  3.000 mm |                                         |
     | # Lay: Max/Min tpl:    3 : 24.0/ 24.0   | Layer/Turn Ins Bd.:   0.180/   0.200 mm | No Strs-Rad x Ax..:       1 x    1      |
     | T-RISE/GRADIENT...:     26.0/ 9.9 deg C | Watts/sq m .......:          529.788    | Resistance (Coil).: 0.028058 @ 75 C     |
     | Turn CSA .........:          50.892 mm2 |                                         | Conductor Dims....: Specified Size      |
     |----------------------------------------- H I G H   V O L T A G E   W I N D I N G   -----------------------------------------|
     | Type of Coil......: Layer-Wound Coil    | Coil-Length.......:          316.000 mm | Cond Mec/Elec Lgth:  280.800 /  279.276 |
     | Conductor.........:    CU-Round         | Inside Dimensions.:   184.814 x 242.546 | Cond-Dim Per Turn.:  1x1x 1.400 x 1.400 |
     | Turns Tot./Nominal:      3429/   3266   | Outside Dimensions:   250.641 x 308.373 | Cond Area Per Turn:         1.53938 mm2 |
     | Cooling Ducts Tk/#:    0.000 mm /  0.00 | Rad Blds (H,Leg,L): 32.91/ 32.91/ 32.91 | HV Conductor Wt...:           113.29 kg |
     | Eff No Cool Ducts.: HV: 0 Leg: 0 LV: 0  | Add Rad Allowance.:            0.000 mm | Lay/Trn/Duc Wts...:  3.41/  0.00/  0.00 |
     | Mean Turn Length..:            798.5 mm | Layer/Turn Ins Bd.:    0.200/  0.124 mm | Insulation Weight.:             3.41 kg |
     | LayIns Tk.........: (18 Full)  0.200 mm | LayIns RB W/OvBld.:             3.06 mm | Average LayIns Tk.:    (Strip) 0.165 mm |
     | CURRENT DENSITY...:        0.984 A/mm2  | # Sup Pts/Ax All..:      12 /  0.000 mm | Total Coil Weight.:           116.70 kg |
     | # Lay: Max/Min tpl: 19# 183.00/135.00 * | Axial Sections....:       1             | Layer-Layer Volts.:           1234.3    |
     | T-RISE/GRADIENT...:     22.2/ 6.0 deg C | Watts/sq m .......:        202.816      | Resistance (Coil).:  35.5077 @ 75 C     |
     |                                         |                                         | Conductor Dims....: Standard Size       |
     |----------------------------------------- E L E C T R I C A L   C L E A R A N C E S -----------------------------------------|
     | LV to Core Leg(mm):  5.50x  5.50x  6.00 | LV Cond to Yoke...:           22.000 mm | Total HV-LV Offset:            0.000 mm |
     | Eff Hi-Lo ElecSpan:           12.000 mm | Ph-Ph Elec Spacing:           15.000 mm | Max LV Sup Span...:           81.000 mm |
     | HV-HSide/HV-LSide.:    40.00 / 40.00 mm | HV-Ends...........:           40.000 mm | Yoke-Case Top/Bot.:   196.00 / 31.00 mm |
     | HV Fixed Gap......:            0.000 mm |                                         |                                         |
     |--------- BASIS FOR CALCULATIONS --------|---------------------- MATERIAL  PRICES IN USD/KG (17-08-01  ) --------------------|
     | Netw.Short Cir.Cap:        500.0  MVA   | E Rnd Wire: AL/CU.:  4.56 / 11.73       | Core Cost.........:           3.88      |
     | Wdg Rise Limit....:         52.0 deg C  | Rect Wire : Al/Cu.:  5.63 /  7.37       | Turn/Lay/DD Insul.:  2.18 /  3.28 / 4.14|
     | Top Oil Rise Limit:         47.0 deg C  | Foil Cond: AL/CU..:  3.59 / 11.73       | Mineral/Silicone..:   0.98 /  6.12      |
     | Max No Load/Load..:       90 /     714  | LME/1000 (CU/AL)..:        0 /        0 | Case Steel/Cooling:   0.78 /  1.71      |
     |------------------------------------------ WEIGHTS, DIMENSIONS, AND COOLING (RIBS) ------------------------------------------|
     | Active Part Weight:              404 kg |                                         | C&C Dim: Ht/Lgth..:   576.00/ 781.92 mm |
     | Clamp & Brace Wt..:               40 kg | H-L Barrier Weight:             4.91 kg |                                         |
     | Mineral Oil Weight:              188 kg | Ribs-Press/Weight.:   0.18 kp/cm2    59 | Rib Height:1,2,3,4:  600/ 600/ 600/ 600 |
     | Bus bar/TC Weight.:         0/     0 kg | Rib Pitch: 1,2,3,4:  100/ 100/ 100/ 100 | No of Ribs:1,2,3,4:    9/   4/   9/   4 |
     | Cov/Case & Cooling:        16/    79 kg | Rib Depth: 1,2,3,4:  200/  50/ 200/  50 | Rib Pan Wd:1,2,3,4:  862/ 393/ 862/ 393 |
     | Total Weight......:              728 kg | Rib Thick: 1,2,3,4: 1.20/1.20/1.20/1.20 | Case: Lt/Wd/Ht(mm): 861.9x 392.9x 803.0 |
     |-------------------------------------------------PRICE & COST IN USD UNITS --------------------------------------------------|
     | Core Cost.........:         1026        | HV / LV Coil Cost.:      1379/       99 | Labor & VOH/Hours.:            0 /   0  |
     | Case/Cooling Cost.:        16/     101  | Bracing Cost......:           32        | Design Matl-Cost..:         2984        |
     | Mineral Oil.......:          184        | Assy and Misc.....:          148        | Variable Cost.....:         2984        |
     | EVALUATED LOSSES..:            0        | EVALUATED COST....:         2984        | RECOMMENDED PRICE.:         5967        |
     |----------------------------------------------------- PERFORMANCE DATA ------------------------------------------------------|
     | HV Wdg DC Losses..:        245  Watts   | LV Wdg DC Losses..:        398  Watts   |                                         |
     | HV Watts (% Eddy).:        246 ( 0.7)   | LV Watts (% Eddy).:        409 ( 1.5)   | LV Bus Bar / Stray:          3 /     30 |
     | No Load Losses....:         88  Watts   | Tot-Ld Watts(%Ed).:        689 ( 6.0)   | Total Losses(ONAN):        777 @  75 C  |
     | % X / % R / % Lead:   3.78/1.38/0.00 %  | % Z (HV-LV-Lead)..:         4.030 %     | TOP OIL RISE......:       20.2 deg C    |
     |                                         | % Z Guaranteed....:         4.000 %     |                                         |
     |-----------------------------------------------------------------------------------------------------------------------------|
     NOTES:  HV Axial & Rad Factors -  1.000,  0.970     LV Rad Factor -   0.970     OPT By: (Min Evaluated Cost )   
             MARG/MULT.: <Rise>: Top Oil=  0 H=  0 L=  0 T=  0 <Loss>: Core= 1.000 BusB=   1.0 Eddy H=   1.0 L=   1.0 Stray=   1.0
             CORE: Std(NO ) Wds(YES) C-C(NO ) Diag(NO ),  COND: Foil Tk(NO ),  CLEAR: Wdg(NO ),  CASE: Std(NO )  CALC: Sh Cir(YES)
             Circuit Load Factors:  HV= 1.000,   LV= 1.000,   TV= 1.000
             Circuit Load Factors:  HV= 1.000,   LV= 1.000,   TV= 1.000
              
             Using LTL Core Loss Calculation Technical Standard: < YES >
             Using LTL Load Loss Calculation Technical Standard: < NO  >
             
             Impedance Model: Convensional
              
             Tapping Turns @.......: 1 - 3429, 2 - 3347, 3 - 3266, 4 - 3184, 5 - 3103
      
      
`;

// Split the input string into an array of values
const values = inputString.split('|').map(value => value.trim()).filter(value => value !== '');

// Extract relevant information and store them in an array
const coilInfoArray = values.map(value => {
    const parts = value.match(/(.{1,18}):\s*(.+)/); // Adjusting the regular expression to properly capture key and data
    const key = parts[1].trim();
    const data = parts[2].trim();
    
    let individualValues;
    if (data.includes('/')) {
        individualValues = data.split(':')[1].trim().split('/').map(value => value.trim());
    } else {
        individualValues = [data.trim()];
    }

    return { key, data: individualValues };
});

console.log(coilInfoArray);