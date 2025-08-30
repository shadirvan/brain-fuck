
### DISKO2
- To check the partitions in a disk image:
```
$ mmls disko-2.dd
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

      Slot      Start        End          Length       Description
000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)
001:  -------   0000000000   0000002047   0000002048   Unallocated
002:  000:000   0000002048   0000053247   0000051200   Linux (0x83)
003:  000:001   0000053248   0000118783   0000065536   Win95 FAT32 (0x0b)
004:  -------   0000118784   0000204799   0000086016   Unallocated
```
- The Linux partition contains the flag. so we need to extract it : `dd if=disko-2.dd of=linux.img bs=512 skip=2048 count=51200`
- The values for the arguments of above command are from the `mmls` command.
- This extract the Linux partition into linux.img
- using the `strings` command and grepping for **picoCTF** we get the flag.
