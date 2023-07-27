# int2intv
Intellivision rom converter for the Analogue NT mini noir jailbreak.

command line: int2intv -m X \<input file\> \<output file\>

  Switches: -m X, where X = 0-9,99 rom memory map to encode

To determine what map to use for a specific rom refer to https://docs.google.com/spreadsheet/ccc?key=0Ar_02usomyeqdHFyaGRnNWdLN1FzWTN3ajlacXBPWFE

Map #99 is used to convert the intellivision Executive ROM (CRC32 0xCBCE86F7) to the correct format for the Intellivision core on the NT mini noir jailbreak.

---

This tool uses the Intellivision BIN format as input, Intellivision ROM files must be first converted to BIN using the tools in the prebuilt donloadable toolset for jzintv.

The downloads for the toolset are here: 

http://spatula-city.org/~im14u2c/intv/

When using the `rom2bin` tool on an Intellivision rom, a rom.cfg and rom.bin file will be respectfully generated.

En example config map for a converted game will look similar to this:


`Princess Quest.cfg`

```
[mapping]
$0000 - $0EFF = $2100
$0F00 - $36FF = $4800
$3700 - $55FF = $A000
$5600 - $94FF = $C100
```

Once converted, the memory map values will look like the following in the source code, here.

```
// Princess Quest
case 17:
MapAddress[0] = 0x2100;
DataSize[0] = 0x0F00;

MapAddress[1] = 0x4800;
DataSize[1] = 0x2800;

MapAddress[2] = 0xA000;
DataSize[2] = 0x1F00;

MapAddress[3] = 0xC100;
DataSize[3] = 0x3F00;
```

Documentation on the INTV2 format is here:
https://github.com/SmokeMonsterPacks/Nt-Mini-Noir-Jailbreak#intellivision-core-release-notes

---

To build from source you can use your favorite flavor of the gnu c++ compiler.

Example:  g++ int2intv.cpp -s -static -o int2intv

Build this on Mac OSX: `g++ int2intv.cpp -o int2intv`

