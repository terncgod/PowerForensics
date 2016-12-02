# Copy-ForensicFile

## SYNOPSIS
{{Fill in the Synopsis}}

## SYNTAX

### ByPath
```
Copy-ForensicFile [-Path] <String> [-Destination] <String>
```

### ByIndex
```
Copy-ForensicFile [-VolumeName <String>] [-Index] <Int32> [-Destination] <String>
```

## DESCRIPTION
{{Fill in the Description}}

## EXAMPLES

### Example 1
```
PS C:\> {{ Add example code here }}
```

{{ Add example description here }}

## PARAMETERS

### -Destination
{{Fill Destination Description}}

```yaml
Type: String
Parameter Sets: (All)
Aliases: 

Required: True
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Index
{{Fill Index Description}}

```yaml
Type: Int32
Parameter Sets: ByIndex
Aliases: 

Required: True
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Path
{{Fill Path Description}}

```yaml
Type: String
Parameter Sets: ByPath
Aliases: FullName

Required: True
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -VolumeName
{{Fill VolumeName Description}}

```yaml
Type: String
Parameter Sets: ByIndex
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### None


## OUTPUTS

### System.Object

## NOTES

## RELATED LINKS


# Get-ForensicAlternateDataStream

## SYNOPSIS
Gets the NTFS Alternate Data Streams on the specified volume.

## SYNTAX

### ByVolume
```
Get-ForensicAlternateDataStream [[-VolumeName] <String>]
```

### ByPath
```
Get-ForensicAlternateDataStream -Path <String>
```

## DESCRIPTION
The Get-ForensicAlternateDataStream cmdlet parses the Master File Table and returns AlternateDataStream objects for files that contain more than one $DATA attribute.

NTFS stores file contents in $DATA attributes. The file system allows a single file to maintain multiple $DATA
attributes. When a file has more than one $DATA attribute the additional attributes are referred to as "Alternate Data
Streams".

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-ForensicAlternateDataStream
```

This example shows Get-ForensicAlternateDataStream getting all ADS on the C:\ logical volume.

## PARAMETERS

### -Path
The path of a file that should be checked for alternate data streams.

```yaml
Type: String
Parameter Sets: ByPath
Aliases: FullName

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -VolumeName
Specifies the name of the volume or logical partition.

Enter the volume name in one of the following formats: \\.\C:, C:, or C.

```yaml
Type: String
Parameter Sets: ByVolume
Aliases: 

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### None


## OUTPUTS

### PowerForensics.Artifacts.AlternateDataStream

## NOTES

## RELATED LINKS


# Get-ForensicAmcache

## SYNOPSIS
Gets previously run commands from the Amcache.hve registry hive.

## SYNTAX

### ByVolume
```
Get-ForensicAmcache [[-VolumeName] <String>]
```

### ByPath
```
Get-ForensicAmcache -HivePath <String>
```

## DESCRIPTION
The Get-Amcache cmdlet parses the Amcache.hve registry hive to derive applications that were recently used. If you don&apos;t specify a hive path (-HivePath), the cmdlet parses the C:\Windows\AppCompat\Programs\Amcache.hve.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-Amcache
```

This example shows Get-Amcache being run against the default Amcache.hve (C:\Windows\AppCompat\Programs\Amcache.hve)

### Example 2
```
[ADMIN]: PS C:\> Get-Amcache -HivePath C:\Windows\AppCompat\Programs\Amcache.hve
```

This is an example of Get-Amcache taking a Amcache.hve as an argument.

## PARAMETERS

### -HivePath
Registry hive to parse.

```yaml
Type: String
Parameter Sets: ByPath
Aliases: Path

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -VolumeName
Specifies the name of the volume or logical partition.

Enter the volume name in one of the following formats: \\.\C:, C:, or C.

```yaml
Type: String
Parameter Sets: ByVolume
Aliases: 

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### None


## OUTPUTS

### PowerForensics.Artifacts.Amcache

## NOTES

## RELATED LINKS


# Get-ForensicAttrDef

## SYNOPSIS
Gets information about all the Master File Table (MFT) file attributes usable in a volume.

## SYNTAX

### ByVolume
```
Get-ForensicAttrDef [[-VolumeName] <String>]
```

### ByPath
```
Get-ForensicAttrDef -Path <String>
```

## DESCRIPTION
The Get-AttrDef cmdlet parses the $AttrDef file on the specified volume and returns information about all MFT file
attributes usable in the volume.

By default, the cmdlet parses the $AttrDef file on the C:\ drive. To change the target drive, use the VolumeName parameter or use the Path parameter to specify an exported $AttrDef file.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-AttrDef -VolumeName \\.\C:

Name                      Type   MinSize MaxSize
----                      ----   ------- -------
$STANDARD_INFORMATION     16     48      72
$ATTRIBUTE_LIST           32     0       18446744073709551615
$FILE_NAME                48     68      578
$OBJECT_ID                64     0       256
$SECURITY_DESCRIPTOR      80     0       18446744073709551615
$VOLUME_NAME              96     2       256
$VOLUME_INFORMATION       112    12      12
$DATA                     128    0       18446744073709551615
$INDEX_ROOT               144    0       18446744073709551615
$INDEX_ALLOCATION         160    0       18446744073709551615
$BITMAP                   176    0       18446744073709551615
$REPARSE_POINT            192    0       16384
$EA_INFORMATION           208    8       8
$EA                       224    0       65536
$LOGGED_UTILITY_STREAM    256    0       65536
```

This example shows returning the MFT Attribute definitions for the C Volume.

### Example 2
```
[ADMIN]: PS C:\> Get-AttrDef -Path 'C:\$AttrDef'

Name                      Type   MinSize MaxSize
----                      ----   ------- -------
$STANDARD_INFORMATION     16     48      72
$ATTRIBUTE_LIST           32     0       18446744073709551615
$FILE_NAME                48     68      578
$OBJECT_ID                64     0       256
$SECURITY_DESCRIPTOR      80     0       18446744073709551615
$VOLUME_NAME              96     2       256
$VOLUME_INFORMATION       112    12      12
$DATA                     128    0       18446744073709551615
$INDEX_ROOT               144    0       18446744073709551615
$INDEX_ALLOCATION         160    0       18446744073709551615
$BITMAP                   176    0       18446744073709551615
$REPARSE_POINT            192    0       16384
$EA_INFORMATION           208    8       8
$EA                       224    0       65536
$LOGGED_UTILITY_STREAM    256    0       65536
```

This example shows Get-AttrDef being run against an exported file.

## PARAMETERS

### -Path
Path to file to be parsed.

```yaml
Type: String
Parameter Sets: ByPath
Aliases: FullName

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -VolumeName
Specifies the name of the volume or logical partition.

Enter the volume name in one of the following formats: \\.\C:, C:, or C.

```yaml
Type: String
Parameter Sets: ByVolume
Aliases: 

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### System.String


## OUTPUTS

### PowerForensics.Ntfs.AttrDef

## NOTES

## RELATED LINKS


# Get-ForensicBitmap

## SYNOPSIS
Determines whether the specified cluster is allocated.

## SYNTAX

### ByVolume
```
Get-ForensicBitmap [[-VolumeName] <String>] -Cluster <Int64>
```

### ByPath
```
Get-ForensicBitmap -Path <String> -Cluster <Int64>
```

## DESCRIPTION
The Get-Bitmap cmdlet parses the $Bitmap file to determine whether or not the specified cluster is allocated.

By default, the cmdlet parses the $Bitmap file on the C:\ drive. To change the target drive, use the
VolumeName parameter or use the Path parameter to specify an exported $Bitmap file.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-Bitmap -Cluster 1000

Cluster InUse
------- -----
   1000  True
```

This example shows Get-Bitmap being used to check Cluster 1000's allocation status.

### Example 2
```
[ADMIN]: PS C:\> Get-Bitmap -Cluster 1000 -Path 'C:\$Bitmap'

Cluster InUse
------- -----
   1000  True
```

This example shows Get-Bitmap checking cluster 1000 of the exported C:\$Bitmap file.

## PARAMETERS

### -Cluster
The cluster number to check for allocation.

```yaml
Type: Int64
Parameter Sets: (All)
Aliases: 

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Path
Path to file to be parsed.

```yaml
Type: String
Parameter Sets: ByPath
Aliases: FullName

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -VolumeName
Specifies the name of the volume or logical partition.

Enter the volume name in one of the following formats: \\.\C:, C:, or C.

```yaml
Type: String
Parameter Sets: ByVolume
Aliases: 

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### System.String


## OUTPUTS

### PowerForensics.Ntfs.Bitmap

## NOTES

## RELATED LINKS


# Get-ForensicBootSector

## SYNOPSIS
Gets the Boot Sector (Master Boot Record or Guid Partition Table) for the specified physical drive.

## SYNTAX

```
Get-ForensicBootSector [-Path] <String> [-AsBytes]
```

## DESCRIPTION
The Get-ForensicBootSector cmdlet parses Logical Block Address 0 of the specified physical drive, determines whether the
disk is formatted using a Master Boot Record or a Guid Partition Table, and returns a MasterBootRecord or GuidPartitionTable object. 

You can also use the AsBytes switch parameter to return the raw bytes of the Boot Sector.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

Use this cmdlet instead of Get-MasterBootRecord or Get-GuidPartitionTable when the disk's partitioning scheme is unknown.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-ForensicBootSector -Path \\.\PHYSICALDRIVE0

MBRSignature    DiskSignature    BootCode                  PartitionTable
------------    -------------    --------                  --------------
Windows 6.1+    82D4BA7D         {51, 192, 142, 208...}    {NTFS}
```

This example shows Get-ForensicBootSector being used to return the MasterBootRecord object from \\.\PHYSICALDRIVE0.

### Example 2
```
[ADMIN]: PS C:\> Get-ForensicBootSector -Path \\.\PHYSICALDRIVE1

Revision                 : 0.1
HeaderSize               : 92
MyLBA                    : 1
AlternateLBA             : 20971519
FirstUsableLBA           : 34
LastUsableLBA            : 20971486
DiskGUID                 : f913e110-0835-4cf1-96c7-380b5db4a42d
PartitionEntryLBA        : 2
NumberOfPartitionEntries : 128
SizeOfPartitionEntry     : 128
PartitionTable           : {Microsoft reserved partition, Basic data partition, Basic data partition}
```

This example shows Get-ForensicBootSector being used to return the GPT object from \\.\PHYSICALDRIVE1.

### Example 3
```
[ADMIN]: PS C:\> Get-ForensicBootSector -Path \\.\PHYSICALDRIVE2 -AsBytes | Format-Hex

Offset     _00_01_02_03_04_05_06_07_08_09_0A_0B_0C_0D_0E_0F  Ascii           
------     ------------------------------------------------  -----           
0x00000000  33 C0 8E D0 BC 00 7C 8E C0 8E D8 BE 00 7C BF 00  3.....|......|..
0x00000010  06 B9 00 02 FC F3 A4 50 68 1C 06 CB FB B9 04 00  .......Ph.......
0x00000020  BD BE 07 80 7E 00 00 7C 0B 0F 85 0E 01 83 C5 10  ....~..|........
0x00000030  E2 F1 CD 18 88 56 00 55 C6 46 11 05 C6 46 10 00  .....V.U.F...F..
0x00000040  B4 41 BB AA 55 CD 13 5D 72 0F 81 FB 55 AA 75 09  .A..U..]r...U.u.
0x00000050  F7 C1 01 00 74 03 FE 46 10 66 60 80 7E 10 00 74  ....t..F.f`.~..t
0x00000060  26 66 68 00 00 00 00 66 FF 76 08 68 00 00 68 00  &amp;fh....f.v.h..h.
0x00000070  7C 68 01 00 68 10 00 B4 42 8A 56 00 8B F4 CD 13  |h..h...B.V.....
0x00000080  9F 83 C4 10 9E EB 14 B8 01 02 BB 00 7C 8A 56 00  ............|.V.
0x00000090  8A 76 01 8A 4E 02 8A 6E 03 CD 13 66 61 73 1C FE  .v..N..n...fas..
0x000000A0  4E 11 75 0C 80 7E 00 80 0F 84 8A 00 B2 80 EB 84  N.u..~..........
0x000000B0  55 32 E4 8A 56 00 CD 13 5D EB 9E 81 3E FE 7D 55  U2..V...]...&gt;.}U
0x000000C0  AA 75 6E FF 76 00 E8 8D 00 75 17 FA B0 D1 E6 64  .un.v....u.....d
0x000000D0  E8 83 00 B0 DF E6 60 E8 7C 00 B0 FF E6 64 E8 75  ......`.|....d.u
0x000000E0  00 FB B8 00 BB CD 1A 66 23 C0 75 3B 66 81 FB 54  .......f#.u;f..T
0x000000F0  43 50 41 75 32 81 F9 02 01 72 2C 66 68 07 BB 00  CPAu2....r,fh...
0x00000100  00 66 68 00 02 00 00 66 68 08 00 00 00 66 53 66  .fh....fh....fSf
0x00000110  53 66 55 66 68 00 00 00 00 66 68 00 7C 00 00 66  SfUfh....fh.|..f
0x00000120  61 68 00 00 07 CD 1A 5A 32 F6 EA 00 7C 00 00 CD  ah.....Z2...|...
0x00000130  18 A0 B7 07 EB 08 A0 B6 07 EB 03 A0 B5 07 32 E4  ..............2.
0x00000140  05 00 07 8B F0 AC 3C 00 74 09 BB 07 00 B4 0E CD  ......&lt;.t.......
0x00000150  10 EB F2 F4 EB FD 2B C9 E4 64 EB 00 24 02 E0 F8  ......+..d..$...
0x00000160  24 02 C3 49 6E 76 61 6C 69 64 20 70 61 72 74 69  $..Invalid parti
0x00000170  74 69 6F 6E 20 74 61 62 6C 65 00 45 72 72 6F 72  tion table.Error
0x00000180  20 6C 6F 61 64 69 6E 67 20 6F 70 65 72 61 74 69   loading operati
0x00000190  6E 67 20 73 79 73 74 65 6D 00 4D 69 73 73 69 6E  ng system.Missin
0x000001A0  67 20 6F 70 65 72 61 74 69 6E 67 20 73 79 73 74  g operating syst
0x000001B0  65 6D 00 00 00 63 7B 9A B3 64 EE 2F 00 00 00 20  em...c{..d./... 
0x000001C0  21 00 07 65 24 41 00 08 00 00 00 00 10 00 00 65  !..e$A.........e
0x000001D0  25 41 0B AA 28 82 00 08 10 00 00 00 10 00 00 AA  %A..(...........
0x000001E0  29 82 0B EF 2C C3 00 08 20 00 00 00 10 00 00 EF  )...,... .......
0x000001F0  2D C3 0F FE FF 90 00 08 30 00 00 F0 AF 00 55 AA  -.......0.....U.
```

This example shows how the AsBytes parameter returns the Boot Sector as a byte array.

## PARAMETERS

### -AsBytes
Specifies that the Guid Partition Table is returned as raw bytes instead of as a custom object.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Path
Specifies the physical drive to investigate. (Ex. \\.\PHYSICALDRIVE0)

```yaml
Type: String
Parameter Sets: (All)
Aliases: DrivePath

Required: True
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### None


## OUTPUTS

### PowerForensics.MasterBootRecord

### PowerForensics.GuidPartitionTable

### System.Byte[]

## NOTES

## RELATED LINKS


# Get-ForensicChildItem

## SYNOPSIS
{{Fill in the Synopsis}}

## SYNTAX

```
Get-ForensicChildItem [[-Path] <String>]
```

## DESCRIPTION
{{Fill in the Description}}

## EXAMPLES

### Example 1
```
PS C:\> {{ Add example code here }}
```

{{ Add example description here }}

## PARAMETERS

### -Path
{{Fill Path Description}}

```yaml
Type: String
Parameter Sets: (All)
Aliases: FullName

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### None


## OUTPUTS

### System.Object

## NOTES

## RELATED LINKS


# Get-ForensicContent

## SYNOPSIS
{{Fill in the Synopsis}}

## SYNTAX

### ByPath
```
Get-ForensicContent [-Path] <String> [-Encoding <FileSystemCmdletProviderEncoding>] [-TotalCount <Int64>]
 [-Tail <Int64>]
```

### ByIndex
```
Get-ForensicContent [-VolumeName <String>] -Index <Int32> [-Encoding <FileSystemCmdletProviderEncoding>]
 [-TotalCount <Int64>] [-Tail <Int64>]
```

## DESCRIPTION
{{Fill in the Description}}

## EXAMPLES

### Example 1
```
PS C:\> {{ Add example code here }}
```

{{ Add example description here }}

## PARAMETERS

### -Encoding
{{Fill Encoding Description}}

```yaml
Type: FileSystemCmdletProviderEncoding
Parameter Sets: (All)
Aliases: 
Accepted values: Unknown, String, Unicode, Byte, BigEndianUnicode, UTF8, UTF7, UTF32, Ascii, Default, Oem, BigEndianUTF32

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Index
{{Fill Index Description}}

```yaml
Type: Int32
Parameter Sets: ByIndex
Aliases: 

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Path
{{Fill Path Description}}

```yaml
Type: String
Parameter Sets: ByPath
Aliases: FullName

Required: True
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Tail
{{Fill Tail Description}}

```yaml
Type: Int64
Parameter Sets: (All)
Aliases: Last

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -TotalCount
{{Fill TotalCount Description}}

```yaml
Type: Int64
Parameter Sets: (All)
Aliases: First, Head

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -VolumeName
{{Fill VolumeName Description}}

```yaml
Type: String
Parameter Sets: ByIndex
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### None


## OUTPUTS

### System.Object

## NOTES

## RELATED LINKS


# Get-ForensicEventLog

## SYNOPSIS
Gets the events in an event log or in all event logs.

## SYNTAX

### ByVolume
```
Get-ForensicEventLog [[-VolumeName] <String>]
```

### ByPath
```
Get-ForensicEventLog -Path <String>
```

## DESCRIPTION
The Get-ForensicEventLog cmdlet parses the specified event Log file and returns an array of EventRecord objects. If you don't specify an event log, Get-ForensicEventLog parses all event logs in the C:\Windows\system32\winevt\Logs directory.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-ForensicEventLog
```

This command runs Get-ForensicEventLog to parse all event logs in the C:\windows\system32\winevt\logs\ directory.

### Example 2
```
[ADMIN]: PS C:\> Get-EventLog -Path C:\evidence\Application.evtx
```

This command uses Get-EventLog to parse an exported Application event log

## PARAMETERS

### -Path
Specifies the path of the file to be parsed.

```yaml
Type: String
Parameter Sets: ByPath
Aliases: FullName

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -VolumeName
Specifies the name of the volume or logical partition (Ex. \\.\C:, \\.\HARDDISKVOLUME1, or C).

```yaml
Type: String
Parameter Sets: ByVolume
Aliases: 

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### None


## OUTPUTS

### PowerForensics.EventLog.EventRecord

## NOTES

## RELATED LINKS


# Get-ForensicExplorerTypedPath

## SYNOPSIS
Gets the file paths that have been typed into the Windows Explorer application.

## SYNTAX

### ByVolume
```
Get-ForensicExplorerTypedPath [[-VolumeName] <String>]
```

### ByPath
```
Get-ForensicExplorerTypedPath -HivePath <String>
```

## DESCRIPTION
The Get-ForensicExplorerTypedPath cmdlet parses a user&apos;s NTUSER.DAT file to derive the file paths that have been typed into the Windows Explorer application.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-ForensicExplorerTypedPath -VolumeName \\.\C:
```

This command gets the URLs typed into Internet Explorer from all user's NTUSER.DAT hives on the C: logical volume.

### Example 2
```
[ADMIN]: PS C:\> Get-ForensicExplorerTypedPath -HivePath C:\Users\Public\NTUSER.DAT}
```

This command gets the URLs typed into Internet Explorer from the C:\Users\Public\NTUSER.DAT hive.

## PARAMETERS

### -HivePath
Registry hive to parse.

```yaml
Type: String
Parameter Sets: ByPath
Aliases: Path

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -VolumeName
Specifies the name of the volume or logical partition.

Enter the volume name in one of the following formats: \\.\C:, C:, or C.

```yaml
Type: String
Parameter Sets: ByVolume
Aliases: 

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### None


## OUTPUTS

### System.String

## NOTES

## RELATED LINKS


# Get-ForensicFileRecord

## SYNOPSIS
Gets the file records from the Master File Table of the specified volume.

## SYNTAX

### ByIndex
```
Get-ForensicFileRecord [-VolumeName <String>] [[-Index] <Int32>] [-AsBytes]
```

### ByPath
```
Get-ForensicFileRecord [-Path] <String> [-AsBytes]
```

### ByMftPath
```
Get-ForensicFileRecord -MftPath <String>
```

## DESCRIPTION
The Get-ForensicFileRecord cmdlet parses the $MFT file and returns an array of FileRecord entries.

By default, this cmdlet parses the $MFT file on the C:\ drive. To change the target drive, use the VolumeName parameter or use the Path parameter to specify an exported $MFT file.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> $mft = Get-ForensicFileRecord
```

This command uses Get-ForensicFileRecord to return all records from the Master File Table on the default C:\ logical volume.

### Example 2
```
[ADMIN]: PS C:\> Get-ForensicFileRecord -VolumeName C: -Index 0


FullName             : C:\$MFT
Name                 : $MFT
SequenceNumber       : 1
RecordNumber         : 0
ParentSequenceNumber : 5
ParentRecordNumber   : 5
Directory            : False
Deleted              : False
ModifiedTime         : 8/13/2015 9:35:13 PM
AccessedTime         : 8/13/2015 9:35:13 PM
ChangedTime          : 8/13/2015 9:35:13 PM
BornTime             : 8/13/2015 9:35:13 PM
FNModifiedTime       : 8/13/2015 9:35:13 PM
FNAccessedTime       : 8/13/2015 9:35:13 PM
FNChangedTime        : 8/13/2015 9:35:13 PM
FNBornTime           : 8/13/2015 9:35:13 PM
```

This command uses Get-ForensicFileRecord to get the Master File Table record at index 0 on the C:\ logical volume.

### Example 3
```
[ADMIN]: PS C:\> Get-ForensicFileRecord -Path C:\Windows\system32\cmd.exe


FullName             : C:\Windows\System32\cmd.exe
Name                 : cmd.exe
SequenceNumber       : 1
RecordNumber         : 38224
ParentSequenceNumber : 1
ParentRecordNumber   : 4061
Directory            : False
Deleted              : False
ModifiedTime         : 7/10/2015 10:59:58 AM
AccessedTime         : 7/10/2015 10:59:58 AM
ChangedTime          : 10/21/2015 2:07:46 PM
BornTime             : 7/10/2015 10:59:58 AM
FNModifiedTime       : 8/13/2015 9:35:46 PM
FNAccessedTime       : 8/13/2015 9:35:46 PM
FNChangedTime        : 8/13/2015 9:35:46 PM
FNBornTime           : 8/13/2015 9:35:46 PM<
```

This command uses Get-ForensicFileRecord to get the Master File Table record for C:\Windows\system32\cmd.exe.

### Example 4
```
[ADMIN]: PS C:\> $mft = Get-ForensicFileRecord -MftPath C:\evidence\MFT
```

This command uses Get-ForensicFileRecord to return all Master File Table records from the exported MFT at C:\evidence\MFT.

### Example 5
```
[ADMIN]: PS C:\> Get-ForensicFileRecord -Path C:\Windows\notepad.exe -AsBytes | Format-Hex

Offset     _00_01_02_03_04_05_06_07_08_09_0A_0B_0C_0D_0E_0F  Ascii
------     ------------------------------------------------  -----
0x00000000  46 49 4C 45 30 00 03 00 73 2B 77 13 00 00 00 00  FILE0...s+w.....
0x00000010  01 00 02 00 38 00 01 00 00 03 00 00 00 04 00 00  ....8...........
0x00000020  00 00 00 00 00 00 00 00 0E 00 00 00 F0 5F 01 00  ............._..
0x00000030  0B 00 72 00 00 00 00 00 10 00 00 00 60 00 00 00  ..r.........`...
0x00000040  00 00 00 00 00 00 00 00 48 00 00 00 18 00 00 00  ........H.......
0x00000050  28 FE C1 84 F0 D5 D0 01 20 47 DB 80 8A CD D0 01  (....... G......
0x00000060  DB 9C 17 87 F7 D5 D0 01 28 FE C1 84 F0 D5 D0 01  ........(.......
0x00000070  20 00 04 00 00 00 00 00 00 00 00 00 00 00 00 00   ...............
0x00000080  00 00 00 00 15 02 00 00 00 00 00 00 00 00 00 00  ................
0x00000090  B0 05 DB 02 00 00 00 00 30 00 00 00 70 00 00 00  ........0...p...
0x000000A0  00 00 00 00 00 00 0B 00 58 00 00 00 18 00 01 00  ........X.......
0x000000B0  B9 05 00 00 00 00 01 00 28 FE C1 84 F0 D5 D0 01  ........(.......
0x000000C0  20 47 DB 80 8A CD D0 01 3C 40 96 B8 F0 D5 D0 01   G......&lt;@......
0x000000D0  28 FE C1 84 F0 D5 D0 01 00 50 03 00 00 00 00 00  (........P......
0x000000E0  00 48 03 00 00 00 00 00 20 00 00 00 00 00 00 00  .H...... .......
0x000000F0  0B 00 6E 00 6F 00 74 00 65 00 70 00 61 00 64 00  ..n.o.t.e.p.a.d.
0x00000100  2E 00 65 00 78 00 65 00 30 00 00 00 70 00 00 00  ..e.x.e.0...p...
0x00000110  00 00 00 00 00 00 09 00 58 00 00 00 18 00 01 00  ........X.......
0x00000120  FC 50 01 00 00 00 02 00 28 FE C1 84 F0 D5 D0 01  .P......(.......
0x00000130  20 47 DB 80 8A CD D0 01 63 33 61 B6 F0 D5 D0 01   G......c3a.....
0x00000140  28 FE C1 84 F0 D5 D0 01 00 50 03 00 00 00 00 00  (........P......
0x00000150  00 48 03 00 00 00 00 00 20 00 00 00 00 00 00 00  .H...... .......
0x00000160  0B 03 6E 00 6F 00 74 00 65 00 70 00 61 00 64 00  ..n.o.t.e.p.a.d.
0x00000170  2E 00 65 00 78 00 65 00 80 00 00 00 48 00 00 00  ..e.x.e.....H...
0x00000180  01 00 00 00 00 00 04 00 00 00 00 00 00 00 00 00  ................
0x00000190  34 00 00 00 00 00 00 00 40 00 00 00 00 00 00 00  4.......@.......
0x000001A0  00 50 03 00 00 00 00 00 00 48 03 00 00 00 00 00  .P.......H......
0x000001B0  00 48 03 00 00 00 00 00 31 35 18 9A 27 00 00 00  .H......15..&apos;...
0x000001C0  D0 00 00 00 20 00 00 00 00 00 00 00 00 00 0C 00  .... ...........
0x000001D0  08 00 00 00 18 00 00 00 8D 00 00 00 94 00 00 00  ................
0x000001E0  E0 00 00 00 B0 00 00 00 00 00 00 00 00 00 0D 00  ................
0x000001F0  94 00 00 00 18 00 00 00 94 00 00 00 00 16 72 00  ..............r.
0x00000200  24 4B 45 52 4E 45 4C 2E 50 55 52 47 45 2E 45 53  $KERNEL.PURGE.ES
0x00000210  42 43 41 43 48 45 00 72 00 00 00 03 00 02 0C 42  BCACHE.r.......B
0x00000220  73 2C DB 07 D6 D0 01 00 C7 9B 0B C7 89 D0 01 02  s,..............
0x00000230  00 00 00 54 00 27 01 0C 80 00 00 20 1C FE AD 81  ...T.&apos;..... ....
0x00000240  46 39 9A 4D FE 67 59 E9 30 3C 30 C5 21 CF F3 83  F9.M.gY.0&lt;0.!...
0x00000250  0E 71 77 E8 7E 64 02 1D C3 DA 49 31 1B 00 04 80  .qw.~d....I1....
0x00000260  00 00 14 B4 F8 DF 0F CF 38 8F 82 08 41 92 26 4C  ........8...A.&amp;L
0x00000270  8B 81 D0 25 5F 31 77 12 03 80 F6 10 83 6B 95 CF  ...%_1w......k..
0x00000280  01 80 B6 D8 39 88 FC D0 01 00 00 00 00 00 00 00  ....9...........
0x00000290  00 01 00 00 68 00 00 00 00 09 18 00 00 00 0A 00  ....h...........
0x000002A0  38 00 00 00 30 00 00 00 24 00 54 00 58 00 46 00  8...0...$.T.X.F.
0x000002B0  5F 00 44 00 41 00 54 00 41 00 00 00 00 00 00 00  _.D.A.T.A.......
0x000002C0  05 00 00 00 00 00 05 00 01 00 00 00 01 00 00 00  ................
0x000002D0  C1 10 00 00 00 00 00 00 03 72 0A 00 02 00 00 00  .........r......
0x000002E0  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x000002F0  02 00 00 00 4F 1A 00 00 FF FF FF FF 82 79 47 11  ....O........yG.
0x00000300  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x00000310  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x00000320  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x00000330  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x00000340  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x00000350  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x00000360  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x00000370  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x00000380  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x00000390  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x000003A0  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x000003B0  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x000003C0  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x000003D0  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x000003E0  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x000003F0  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
```

This command uses Get-ForensicFileRecord to get the Master File Table record for C:\Windows\notepad.exe as a byte array.

## PARAMETERS

### -AsBytes
Returns Master File Table Entry as byte array instead of as FileRecord object.

```yaml
Type: SwitchParameter
Parameter Sets: ByIndex, ByPath
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Index
The index number of the desired Master File Table entry.

```yaml
Type: Int32
Parameter Sets: ByIndex
Aliases: 

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -MftPath
Path to an exported Master File Table.

```yaml
Type: String
Parameter Sets: ByMftPath
Aliases: 

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Path
The path of the desired Master File Table entry.

```yaml
Type: String
Parameter Sets: ByPath
Aliases: FullName

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -VolumeName
Specifies the name of the volume or logical partition.

Enter the volume name in one of the following formats: \\.\C:, C:, or C.

```yaml
Type: String
Parameter Sets: ByIndex
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### System.String


## OUTPUTS

### PowerForensics.Ntfs.FileRecord

### System.Byte

## NOTES

## RELATED LINKS


# Get-ForensicFileRecordIndex

## SYNOPSIS
Gets the MFT Record Index for the specified file.

## SYNTAX

```
Get-ForensicFileRecordIndex [-Path] <String>
```

## DESCRIPTION
The Get-ForensicFileRecordIndex cmdlet returns the Master File Table Record Index Number for the specified file.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-ForensicFileRecordIndex C:\Windows\Notepad.exe
```

This command uses Get-ForensicFileRecordIndex to get the Master File Table Record Index for C:\Windows\Notepad.exe.

## PARAMETERS

### -Path
The path of the file to return the Master File Table record index for.

```yaml
Type: String
Parameter Sets: (All)
Aliases: FullName

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

## INPUTS

### System.String


## OUTPUTS

### System.UInt64

## NOTES

## RELATED LINKS


# Get-ForensicFileSlack

## SYNOPSIS
Gets the specified volume's slack space.

## SYNTAX

### ByIndex
```
Get-ForensicFileSlack [-VolumeName <String>] [[-Index] <Int32>]
```

### ByPath
```
Get-ForensicFileSlack [-Path] <String>
```

## DESCRIPTION
The Get-ForensicFileSlack cmdlet gets the specified volume&apos;s slack space as a byte array.

&quot;Slack space&quot; is the difference between the true size of a file&apos;s contents and the allocated size of a file on disk.

When NTFS stores data in a file, the data must be allocated in cluster-sized chunks (commonly 4096 bytes), which creates slack space.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-ForensicFileSlack -VolumeName \\.\C: -Index 0
```

This command uses Get-ForensicFileSlack to get the slack space from the file that is MFT record index 0 on the C:\ logical volume.

### Example 2
```
[ADMIN]: PS C:\> Get-ForensicFileSlack -Path C:\windows\notepad.exe
```

This command uses Get-ForensicFileSlack to return the slack space for Notepad.exe.

## PARAMETERS

### -Index
The index number of the file to return slack space for.

```yaml
Type: Int32
Parameter Sets: ByIndex
Aliases: 

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Path
The path of the file to return slack space for.

```yaml
Type: String
Parameter Sets: ByPath
Aliases: FullName

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -VolumeName
Specifies the name of the volume or logical partition.

Enter the volume name in one of the following formats: \\.\C:, C:, or C.

```yaml
Type: String
Parameter Sets: ByIndex
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### System.String


## OUTPUTS

### System.Byte[]

## NOTES

## RELATED LINKS


# Get-ForensicGuidPartitionTable

## SYNOPSIS
Gets the Guid Partition Table for the specified physical drive.

## SYNTAX

```
Get-ForensicGuidPartitionTable [-Path] <String> [-AsBytes]
```

## DESCRIPTION
The Get-ForensicGuidPartitionTable cmdlet gets the Guid Partition Table for the specified physical drive.

By default, Get-ForensicGuidPartitionTable returns a GuidPartitionTable object. You can also use the AsBytes switch parameter to return the raw bytes of the Guid Partition Table.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-ForensicGuidPartitionTable -Path \\.\PHYSICALDRIVE1

Revision                 : 0.1
HeaderSize               : 92
MyLBA                    : 1
AlternateLBA             : 20971519
FirstUsableLBA           : 34
LastUsableLBA            : 20971486
DiskGuid                 : f913e110-0835-4cf1-96c7-380b5db4a42d
PartitionEntryLBA        : 2
NumberOfPartitionEntries : 128
SizeOfPartitionEntry     : 128
PartitionTable           : {Microsoft reserved partition, Basic data partition, Basic data partition}
```

This is an example of Get-GuidPartitionTable being run against \\.\PHYSICALDRIVE1

### Example 2
```
[ADMIN]: PS C:\> Get-ForensicGuidPartitionTable -Path \\.\PHYSICALDRIVE1 -AsBytes | Format-Hex

Offset     _00_01_02_03_04_05_06_07_08_09_0A_0B_0C_0D_0E_0F  Ascii
------     ------------------------------------------------  -----
0x00000000  45 46 49 20 50 41 52 54 00 00 01 00 5C 00 00 00  EFI PART....\...
0x00000010  F3 73 9F 97 00 00 00 00 01 00 00 00 00 00 00 00  .s..............
0x00000020  FF FF 3F 01 00 00 00 00 22 00 00 00 00 00 00 00  ..?.....&quot;.......
0x00000030  DE FF 3F 01 00 00 00 00 10 E1 13 F9 35 08 F1 4C  ..?.........5..L
0x00000040  96 C7 38 0B 5D B4 A4 2D 02 00 00 00 00 00 00 00  ..8.]..-........
0x00000050  80 00 00 00 80 00 00 00 3B 04 A4 F8 00 00 00 00  ........;.......
0x00000060  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x00000070  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x00000080  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x00000090  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x000000A0  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x000000B0  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x000000C0  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x000000D0  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x000000E0  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x000000F0  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x00000100  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x00000110  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x00000120  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x00000130  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x00000140  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x00000150  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x00000160  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x00000170  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x00000180  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x00000190  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x000001A0  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x000001B0  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x000001C0  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x000001D0  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x000001E0  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x000001F0  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
```

This command uses Get-ForensicGuidPartitionTable and its AsBytes parameter to return the GPT as a byte array.

## PARAMETERS

### -AsBytes
Returns Guid Partition Table as byte array instead of as GuidPartitionTable object.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Path
Specified the physical drive to investigate. (Ex. \\.\PHYSICALDRIVE0)

```yaml
Type: String
Parameter Sets: (All)
Aliases: DrivePath

Required: True
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### None


## OUTPUTS

### PowerForensics.GuidPartitionTable

### System.Byte[]

## NOTES

## RELATED LINKS


# Get-ForensicMasterBootRecord

## SYNOPSIS
Gets the Master Boot Record for the specified physical drive.

## SYNTAX

```
Get-ForensicMasterBootRecord [-Path] <String> [-AsBytes]
```

## DESCRIPTION
The Get-ForensicMasterBootRecord cmdlet gets the Master Boot Record for the specified physical drive and analyzes the MBR's boot code for anomalies.

By default, Get-ForensicMasterBootRecord returns a MasterBootRecord object that has detailed information about the drive&apos;s boot code and partition table. You can also use the AsBytes switch parameter to return the raw bytes of the Master Boot Record.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-MasterBootRecord -Path \\.\PHYSICALDRIVE0

MBRSignature   DiskSignature   PartitionTable
------------   -------------   --------------
Windows 6.1+   82D4BA7D        {NTFS}
```

This is an example of Get-MasterBootRecord being run against \\.\PHYSICALDRIVE0

### Example 2
```
[ADMIN]: PS C:\> Get-MasterBootRecord -Path \\.\PHYSICALDRIVE0 -AsBytes | Format-Hex

Offset     _00_01_02_03_04_05_06_07_08_09_0A_0B_0C_0D_0E_0F  Ascii
------     ------------------------------------------------  -----
0x00000000  33 C0 8E D0 BC 00 7C 8E C0 8E D8 BE 00 7C BF 00  3.....|......|..
0x00000010  06 B9 00 02 FC F3 A4 50 68 1C 06 CB FB B9 04 00  .......Ph.......
0x00000020  BD BE 07 80 7E 00 00 7C 0B 0F 85 0E 01 83 C5 10  ....~..|........
0x00000030  E2 F1 CD 18 88 56 00 55 C6 46 11 05 C6 46 10 00  .....V.U.F...F..
0x00000040  B4 41 BB AA 55 CD 13 5D 72 0F 81 FB 55 AA 75 09  .A..U..]r...U.u.
0x00000050  F7 C1 01 00 74 03 FE 46 10 66 60 80 7E 10 00 74  ....t..F.f`.~..t
0x00000060  26 66 68 00 00 00 00 66 FF 76 08 68 00 00 68 00  &amp;fh....f.v.h..h.
0x00000070  7C 68 01 00 68 10 00 B4 42 8A 56 00 8B F4 CD 13  |h..h...B.V.....
0x00000080  9F 83 C4 10 9E EB 14 B8 01 02 BB 00 7C 8A 56 00  ............|.V.
0x00000090  8A 76 01 8A 4E 02 8A 6E 03 CD 13 66 61 73 1C FE  .v..N..n...fas..
0x000000A0  4E 11 75 0C 80 7E 00 80 0F 84 8A 00 B2 80 EB 84  N.u..~..........
0x000000B0  55 32 E4 8A 56 00 CD 13 5D EB 9E 81 3E FE 7D 55  U2..V...]...&gt;.}U
0x000000C0  AA 75 6E FF 76 00 E8 8D 00 75 17 FA B0 D1 E6 64  .un.v....u.....d
0x000000D0  E8 83 00 B0 DF E6 60 E8 7C 00 B0 FF E6 64 E8 75  ......`.|....d.u
0x000000E0  00 FB B8 00 BB CD 1A 66 23 C0 75 3B 66 81 FB 54  .......f#.u;f..T
0x000000F0  43 50 41 75 32 81 F9 02 01 72 2C 66 68 07 BB 00  CPAu2....r,fh...
0x00000100  00 66 68 00 02 00 00 66 68 08 00 00 00 66 53 66  .fh....fh....fSf
0x00000110  53 66 55 66 68 00 00 00 00 66 68 00 7C 00 00 66  SfUfh....fh.|..f
0x00000120  61 68 00 00 07 CD 1A 5A 32 F6 EA 00 7C 00 00 CD  ah.....Z2...|...
0x00000130  18 A0 B7 07 EB 08 A0 B6 07 EB 03 A0 B5 07 32 E4  ..............2.
0x00000140  05 00 07 8B F0 AC 3C 00 74 09 BB 07 00 B4 0E CD  ......&lt;.t.......
0x00000150  10 EB F2 F4 EB FD 2B C9 E4 64 EB 00 24 02 E0 F8  ......+..d..$...
0x00000160  24 02 C3 49 6E 76 61 6C 69 64 20 70 61 72 74 69  $..Invalid parti
0x00000170  74 69 6F 6E 20 74 61 62 6C 65 00 45 72 72 6F 72  tion table.Error
0x00000180  20 6C 6F 61 64 69 6E 67 20 6F 70 65 72 61 74 69   loading operati
0x00000190  6E 67 20 73 79 73 74 65 6D 00 4D 69 73 73 69 6E  ng system.Missin
0x000001A0  67 20 6F 70 65 72 61 74 69 6E 67 20 73 79 73 74  g operating syst
0x000001B0  65 6D 00 00 00 63 7B 9A 82 D4 BA 7D 00 00 80 20  em...c{....}...
0x000001C0  21 00 07 FE FF FF 00 08 00 00 00 F0 7F 07 00 00  !...............
0x000001D0  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x000001E0  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x000001F0  00 00 00 00 00 00 00 00 00 00 00 00 00 00 55 AA  ..............U.
```

This command uses the AsBytes parameter of Get-MasterBootRecord to get the MBR as a byte array.

## PARAMETERS

### -AsBytes
Returns Master Boot Record as byte array instead of as MasterBootRecord object.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Path
Specified the physical drive to investigate. (Ex. \\.\PHYSICALDRIVE0)

```yaml
Type: String
Parameter Sets: (All)
Aliases: DrivePath

Required: True
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### None


## OUTPUTS

### PowerForensics.MasterBootRecord

### System.Byte

## NOTES

## RELATED LINKS


# Get-ForensicMftSlack

## SYNOPSIS
Gets the Master File Table (MFT) slack space for the specified volume.

## SYNTAX

### ByIndex
```
Get-ForensicMftSlack [-VolumeName <String>] [[-Index] <Int32>]
```

### ByPath
```
Get-ForensicMftSlack [-Path] <String>
```

### ByMftPath
```
Get-ForensicMftSlack -MftPath <String>
```

## DESCRIPTION
The Get-ForensicMftSlack cmdlet returns a byte array representing the slack space found in Master File Table (MFT) records.

Each MFT File Record is 1024 bytes long. When a file record does not allocate all 1024 bytes, the remaining bytes are considered "slack". To compute slack space, compare the AllocatedSize and RealSize properties of a FileRecord object.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-ForensicMftSlack -VolumeName C:
```

This command uses Get-ForensicMftSlack to get slack space from the $MFT file on the C:\ logical volume.

### Example 2
```
[ADMIN]: PS C:\> Get-ForensicMftSlack  -VolumeName C: -Index 24212
```

This command uses Get-ForensicMftSlack to get the slack space from the MFT record at index 24212 on the C:\ logical volume.

### Example 3
```
[ADMIN]: PS C:\> Get-ForensicMftSlack -Path C:\Windows\system32\cmd.exe
```

This command uses Get-ForensicMftSlack to get the slack space on the Cmd.exe MFT record.

### Example 4
```
[ADMIN]: PS C:\> Get-ForensicMftSlack -MftPath C:\evidence\MFT
```

This command uses Get-ForensicMftSlack to get the MFT slack space from an exported Master File Table.

## PARAMETERS

### -Index
The index of the MFT entry to return MFT slack space for.

```yaml
Type: Int32
Parameter Sets: ByIndex
Aliases: 

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -MftPath
Path to an exported Master File Table.

```yaml
Type: String
Parameter Sets: ByMftPath
Aliases: 

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Path
The path to the file to return MFT slack space for.

```yaml
Type: String
Parameter Sets: ByPath
Aliases: FullName

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -VolumeName
Specifies the name of the volume or logical partition.

Enter the volume name in one of the following formats: \\.\C:, C:, or C.

```yaml
Type: String
Parameter Sets: ByIndex
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### System.String


## OUTPUTS

### System.Byte[]

## NOTES

## RELATED LINKS


# Get-ForensicNetworkList

## SYNOPSIS
Gets a list of networks that the system has previously been connected to.

## SYNTAX

### ByVolume
```
Get-ForensicNetworkList [[-VolumeName] <String>]
```

### ByPath
```
Get-ForensicNetworkList -HivePath <String>
```

## DESCRIPTION
The Get-ForensicNetworkList cmdlet parses the SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList key to derive a list of previously connected networks.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-ForensicNetworkList
```

This command uses Get-ForensicNetworkList to parse the SOFTWARE hive on the C:\ logical volume.

### Example 2
```
[ADMIN]: PS C:\> Get-ForensicNetworkList -HivePath C:\evidence\SOFTWARE
```

This command uses Get-ForensicNetworkList on an exported SOFTWARE hive.

## PARAMETERS

### -HivePath
Registry hive to parse.

```yaml
Type: String
Parameter Sets: ByPath
Aliases: Path

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -VolumeName
Specifies the name of the volume or logical partition.

Enter the volume name in one of the following formats: \\.\C:, C:, or C.

```yaml
Type: String
Parameter Sets: ByVolume
Aliases: 

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### None


## OUTPUTS

### PowerForensics.Artifacts.NetworkList

## NOTES

## RELATED LINKS


# Get-ForensicOfficeFileMru

## SYNOPSIS
Gets files that have recently been used in Microsoft Office.

## SYNTAX

### ByVolume
```
Get-ForensicOfficeFileMru [[-VolumeName] <String>]
```

### ByPath
```
Get-ForensicOfficeFileMru -HivePath <String>
```

## DESCRIPTION
The Get-ForensicOfficeFileMru cmdlet parses NTUSER.DAT registry hives to determine what files have recently been used by Microsoft Office applications.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-ForensicOfficeFileMru
```

This example shows Get-ForensicOfficeFileMru parsing all user's NTUSER.DAT hives.

### Example 2
```
[ADMIN]: PS C:\> Get-ForensicOfficeFileMru -HivePath C:\Users\tester\NTUSER.DAT
```

This command uses the HivePath parameter of Get-ForensicOfficeFileMru to specify an exported NTUSER.DAT hive to parse.

## PARAMETERS

### -HivePath
Registry hive to parse.

```yaml
Type: String
Parameter Sets: ByPath
Aliases: Path

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -VolumeName
Specifies the name of the volume or logical partition.

Enter the volume name in one of the following formats: \\.\C:, C:, or C.

```yaml
Type: String
Parameter Sets: ByVolume
Aliases: 

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### None


## OUTPUTS

### PowerForensics.Artifacts.MicrosoftOffice.FileMRU

## NOTES

## RELATED LINKS


# Get-ForensicOfficeOutlookCatalog

## SYNOPSIS
Gets the location of Microsoft Outlook catalog (pst/ost) files.

## SYNTAX

### ByVolume
```
Get-ForensicOfficeOutlookCatalog [[-VolumeName] <String>]
```

### ByPath
```
Get-ForensicOfficeOutlookCatalog -HivePath <String>
```

## DESCRIPTION
The Get-ForensicOfficeOutlookCatalog cmdlet parses NTUSER.DAT registry hives to determine the location of Microsoft Outlook catalog files.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-ForensicOfficeOutlookCatalog
```

This example shows Get-ForensicOfficeOutlookCatalog parsing all user's NTUSER.DAT hives.

### Example 2
```
[ADMIN]: PS C:\> Get-ForensicOfficeOutlookCatalog -HivePath C:\Users\tester\NTUSER.DAT
```

This command uses the HivePath parameter of Get-ForensicOfficeOutlookCatalog to specify an exported NTUSER.DAT hive to parse.

## PARAMETERS

### -HivePath
Registry hive to parse.

```yaml
Type: String
Parameter Sets: ByPath
Aliases: Path

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -VolumeName
Specifies the name of the volume or logical partition.

Enter the volume name in one of the following formats: \\.\C:, C:, or C.

```yaml
Type: String
Parameter Sets: ByVolume
Aliases: 

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### None


## OUTPUTS

### PowerForensics.Artifacts.MicrosoftOffice.OutlookCatalog

## NOTES

## RELATED LINKS


# Get-ForensicOfficeTrustRecord

## SYNOPSIS
Gets files that have been explicity trusted by users of Microsoft Offfice applications.

## SYNTAX

### ByVolume
```
Get-ForensicOfficeTrustRecord [[-VolumeName] <String>]
```

### ByPath
```
Get-ForensicOfficeTrustRecord -HivePath <String>
```

## DESCRIPTION
The Get-ForensicOfficeFileMru cmdlet parses NTUSER.DAT registry hives to determine what files have been explicitly trusted by users of Microsoft Office applications.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-ForensicOfficeTrustRecord
```

This example shows Get-ForensicOfficeTrustRecord parsing all user's NTUSER.DAT hives.

### Example 2
```
[ADMIN]: PS C:\> Get-ForensicOfficeTrustRecord -HivePath C:\Users\tester\NTUSER.DAT
```

This command uses the HivePath parameter of Get-ForensicOfficeTrustRecord to specify an exported NTUSER.DAT hive to parse.

## PARAMETERS

### -HivePath
Registry hive to parse.

```yaml
Type: String
Parameter Sets: ByPath
Aliases: Path

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -VolumeName
Specifies the name of the volume or logical partition.

Enter the volume name in one of the following formats: \\.\C:, C:, or C.

```yaml
Type: String
Parameter Sets: ByVolume
Aliases: 

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### None


## OUTPUTS

### PowerForensics.Artifacts.MicrosoftOffice.TrustRecords

## NOTES

## RELATED LINKS


# Get-ForensicPartitionTable

## SYNOPSIS
Gets a list of partition objects on the specified disk.

## SYNTAX

```
Get-ForensicPartitionTable [-Path] <String>
```

## DESCRIPTION
The Get-ForensicPartitionTable cmdlet gets one or more Partition objects depending on the specified DrivePath.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-ForensicPartitionTable -DrivePath \\.\PHYSICALDRIVE0


Bootable     SystemID     StartSector     EndSector
--------     --------     -----------     ---------
True         NTFS         2048            125827072
```

This command gets all MBR partitions on the \\.\PHYSICALDRIVE0 disk.

### Example 2
```
[ADMIN]: PS C:\> Get-ForensicPartitionTable -Path \\.\PHYSICALDRIVE1

PartitionTypeGUID   : e3c9e316-0b5c-4db8-817d-f92df00215ae
UniquePartitionGUID : ff1a8a47-08f8-43ab-b410-53697f0b2323
StartingLBA         : 34
EndingLBA           : 65569
Attributes          : 0
PartitionName       : Microsoft reserved partition

PartitionTypeGUID   : ebd0a0a2-b9e5-4433-87c0-68b6b72699c7
UniquePartitionGUID : 6d76ae42-b6c1-4fbe-8d42-20cd366026b4
StartingLBA         : 67584
EndingLBA           : 2164735
Attributes          : 0
PartitionName       : Basic data partition

PartitionTypeGUID   : ebd0a0a2-b9e5-4433-87c0-68b6b72699c7
UniquePartitionGUID : d6795c3a-8a4d-4fb4-91a0-488812cce027
StartingLBA         : 2164736
EndingLBA           : 4261887
Attributes          : 0
PartitionName       : Basic data partition
```

This command gets all GPT partitions on the \\.\PHYSICALDRIVE1 disk.

## PARAMETERS

### -Path
Specified the physical drive to investigate. (Ex. \\.\PHYSICALDRIVE0)

```yaml
Type: String
Parameter Sets: (All)
Aliases: DrivePath

Required: True
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### None


## OUTPUTS

### PowerForensics.GuidPartitionTableEntry[]

## NOTES

## RELATED LINKS


# Get-ForensicPrefetch

## SYNOPSIS
Gets the Prefetch objects from the specified volume or file.

## SYNTAX

### ByVolume
```
Get-ForensicPrefetch [[-VolumeName] <String>] [-Fast]
```

### ByPath
```
Get-ForensicPrefetch -Path <String> [-Fast]
```

## DESCRIPTION
The Get-ForensicPrefetch cmdlet parses the binary structure in the specified Prefetch file. If a file is not specified, Get-Prefetch parses all .pf files in the C:\Windows\Prefetch directory.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-ForensicPrefetch
```

This command gets an array of all Prefetch files in the C:\Windows\Prefetch directory.

### Example 1
```
[ADMIN]: PS C:\> Get-ForensicPrefetch -Path C:\Windows\Prefetch\CMD.EXE-89305D47.pf


Version            : WINDOWS_8
Name               : CMD.EXE
Path               : \DEVICE\HARDDISKVOLUME1\WINDOWS\SYSTEM32\CMD.EXE
PathHash           : 89305D47
DependencyCount    : 25
PrefetchAccessTime : {4/3/2015 4:29:25 AM, 4/3/2015 4:29:18 AM, 3/31/2015 12:33:17 PM, 3/31/2015 
                     12:22:42 PM...}
DeviceCount        : 1
RunCount           : 40
```

This command parses the Prefetch file specified by the Path parameter.

## PARAMETERS

### -Fast
Use the Windows API to list files within the C:\Windows\Prefetch directory. WARNING: Not forensically sound.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Path
Path to file to be parsed.

```yaml
Type: String
Parameter Sets: ByPath
Aliases: FullName

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -VolumeName
Specifies the name of the volume or logical partition.

Enter the volume name in one of the following formats: \\.\C:, C:, or C.

```yaml
Type: String
Parameter Sets: ByVolume
Aliases: 

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### System.String


## OUTPUTS

### PowerForensics.Artifacts.Prefetch

## NOTES

## RELATED LINKS


# Get-ForensicRecentFileCache

## SYNOPSIS
Gets previously run commands from the RecentFileCache.bcf file.

## SYNTAX

### ByVolume
```
Get-ForensicRecentFileCache [[-VolumeName] <String>]
```

### ByPath
```
Get-ForensicRecentFileCache -Path <String>
```

## DESCRIPTION
The Get-ForensicRecentFileCache cmdlet parses the RecentFileCache.bcf file to derive applications that were recently used. If you don&apos;t specify a file path (-Path), the cmdlet parses the C:\Windows\AppCompat\Programs\RecentFileCache.bcf.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-ForensicRecentFileCache
```

This example shows Get-ForensicRecentFileCache being run against the default RecentFileCache.bcf (C:\Windows\AppCompat\Programs\RecentFileCache.bcf)

### Example 2
```
[ADMIN]: PS C:\> Get-ForensicRecentFileCache -Path C:\Windows\AppCompat\Programs\RecentFileCache.bcf
```

This is an example of Get-ForensicRecentFileCache taking a RecentFileCache.bcf file path as an argument.

## PARAMETERS

### -Path
Path to RecentFileCache.bcf file to process.

```yaml
Type: String
Parameter Sets: ByPath
Aliases: FullName

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -VolumeName
Specifies the name of the volume or logical partition.

Enter the volume name in one of the following formats: \\.\C:, C:, or C.

```yaml
Type: String
Parameter Sets: ByVolume
Aliases: 

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### System.String


## OUTPUTS

### System.String

## NOTES

## RELATED LINKS


# Get-ForensicRegistryKey

## SYNOPSIS
Gets the keys of the specified registry hive.

## SYNTAX

### ByKey
```
Get-ForensicRegistryKey -HivePath <String> [-Key <String>]
```

### Recursive
```
Get-ForensicRegistryKey -HivePath <String> [-Recurse]
```

## DESCRIPTION
The Get-ForensicRegistryKey cmdlet parses a registry hive and returns the subkeys of the specified key.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-ForensicRegistryKey -HivePath C:\Windows\system32\config\SOFTWARE -Key Tenable


HivePath                : C:\Windows\system32\config\SOFTWARE
WriteTime               : 8/14/2015 4:18:52 PM
NumberOfSubKeys         : 0
NumberOfVolatileSubKeys : 0
NumberOfValues          : 1
FullName                : Tenable\Nessus
Name                    : Nessus
Allocated               : True
```

This command gets the subkeys of the HKLM:\SOFTWARE\Tenable key.

### Example 1
```
[ADMIN]: PS C:\> $nk = Get-RegistryKey -HivePath C:\Windows\system32\config\SAM -Recurse
```

This gets all keys in the SAM hive.

## PARAMETERS

### -HivePath
The registry hive to parse.

```yaml
Type: String
Parameter Sets: (All)
Aliases: Path

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Key
The key to begin listing subkeys from.

```yaml
Type: String
Parameter Sets: ByKey
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Recurse
Recursively list all keys in the specified hive.

```yaml
Type: SwitchParameter
Parameter Sets: Recursive
Aliases: 

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### None


## OUTPUTS

### PowerForensics.Registry.NamedKey

## NOTES

## RELATED LINKS


# Get-ForensicRegistryValue

## SYNOPSIS
Gets the values of the specified registry key.

## SYNTAX

```
Get-ForensicRegistryValue [-HivePath] <String> [[-Key] <String>] [[-Value] <String>]
```

## DESCRIPTION
The Get-ForensicRegistryValue cmdlet parses a registry hive and returns the values of a specified key.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-ForensicRegistryValue -HivePath C:\Windows\system32\config\SOFTWARE -Key Microsoft\Windows\CurrentVersion\Run
```

This command gets the values of the Run key.

### Example 2
```
[ADMIN]: PS C:\> Get-RegistryValue -HivePath C:\Windows\system32\config\SYSTEM -Key ControlSet001\Serivces\Enum -Value NextParentID.72bb93.8

HivePath   : C:\Windows\system32\config\SYSTEM
Key        : Enum
DataLength : 4
DataType   : REG_DWORD
Name       : NextParentID.72bb93.8
Allocated  : True
```

This command gets the NextParentID.72bb93.8 value of the HKLM:\SYSTEM\ControlSet001\Services\Enum key.

## PARAMETERS

### -HivePath
The registry hive to parse.

```yaml
Type: String
Parameter Sets: (All)
Aliases: Path

Required: True
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Key
The key to list values from.

```yaml
Type: String
Parameter Sets: (All)
Aliases: 

Required: False
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Value
The specific value to return.

```yaml
Type: String
Parameter Sets: (All)
Aliases: 

Required: False
Position: 2
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### None


## OUTPUTS

### PowerForensics.Registry.ValueKey

## NOTES

## RELATED LINKS


# Get-ForensicRunKey

## SYNOPSIS
Gets applications that will autostart due to their inclusion in a "Run" key.

## SYNTAX

### ByVolume
```
Get-ForensicRunKey [[-VolumeName] <String>]
```

### ByPath
```
Get-ForensicRunKey -HivePath <String>
```

## DESCRIPTION
The Get-ForensicRunKey cmdlet parses the SOFTWARE and NTUSER.DAT hives to produce a list of applications that have been added to a "Run" key.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-ForensicRunKey
```

{{ Add example description here }}

### Example 2
```
[ADMIN]: PS C:\> Get-ForensicRunKey -HivePath C:\Windows\System32\config\SOFTWARE
```

{{ Add example description here }}

## PARAMETERS

### -HivePath
Registry hive to parse.

```yaml
Type: String
Parameter Sets: ByPath
Aliases: Path

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -VolumeName
Specifies the name of the volume or logical partition.

Enter the volume name in one of the following formats: \\.\C:, C:, or C.

```yaml
Type: String
Parameter Sets: ByVolume
Aliases: 

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### None


## OUTPUTS

### PowerForensics.Artifacts.Persistence.RunKey

## NOTES

## RELATED LINKS


# Get-ForensicRunMru

## SYNOPSIS
Gets the commands that were issued by the user to the run dialog.

## SYNTAX

### ByVolume
```
Get-ForensicRunMru [[-VolumeName] <String>]
```

### ByPath
```
Get-ForensicRunMru -HivePath <String>
```

## DESCRIPTION
The Get-ForensicRunMru cmdlet parses a user&apos;s NTUSER.DAT file to derive the commands that have been issued to the run dialog.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-ForensicRunMru -VolumeName \\.\C:
```

This command gets the URLs typed into Internet Explorer from all user's NTUSER.DAT hives on the C: logical volume.

### Example 2
```
[ADMIN]: PS C:\> Get-ForensicRunMru -HivePath C:\Users\Public\NTUSER.DAT
```

This command gets the URLs typed into Internet Explorer from the C:\Users\Public\NTUSER.DAT hive.

## PARAMETERS

### -HivePath
Registry hive to parse.

```yaml
Type: String
Parameter Sets: ByPath
Aliases: Path

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -VolumeName
Specifies the name of the volume or logical partition.

Enter the volume name in one of the following formats: \\.\C:, C:, or C.

```yaml
Type: String
Parameter Sets: ByVolume
Aliases: 

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### None


## OUTPUTS

### System.String

## NOTES

## RELATED LINKS


# Get-ForensicScheduledJob

## SYNOPSIS
Gets the scheduled jobs from the specified volume.

## SYNTAX

### ByVolume
```
Get-ForensicScheduledJob [[-VolumeName] <String>]
```

### ByPath
```
Get-ForensicScheduledJob -Path <String>
```

## DESCRIPTION
The Get-ForensicScheduledJob cmdlet parses the binary structure in the specified ScheduledJob file. If a file is not specified, Get-ForensicScheduledJob parses all .job files in the C:\Windows\Tasks directory.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the &apos;Run as administrator&apos; option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-ForensicScheduledJob -Volume C:
```

This example parses the scheduled jobs in the C:\ logical volume.

### Example 2
```
[ADMIN]: PS C:\> Get-ForensicScheduledJob -Path C:\Windows\Tasks\GoogleUpdateTaskMachineUA.job


ProductVersion       : Windows8_1
FileVersion          : 1
Uuid                 : e841ef0f-7b64-45da-a8fb-1c3e05196ce1
ErrorRetryCount      : 0
ErrorRetryInterval   : 0
IdleDeadline         : 60
IdleWait             : 10
MaximumRuntime       : 4294967294
ExitCode             : 0
Status               : SCHED_S_TASK_READY
Flags                : RUN_ONLY_IF_DOCKED, KILL_IF_GOING_ON_BATTERIES, DISABLED
RunTime              : 11/17/2015 8:11:00 PM
RunningInstanceCount : 0
ApplicationName      : C:\Program Files\Google\Update\GoogleUpdate.exe
Parameters           : ?/ua /installsource scheduler
WorkingDirectory     :
Author               : ?WIN-OL5AKAF1OUJ\Uproot
Comment              : GKeeps your Google software up to date. If this task is disabled or stopped, your Google
                       software will not be kept up to date, meaning security vulnerabilities that may arise cannot be
                       fixed and features may not work. This task uninstalls itself when there is no Google software
                       using it.
StartTime            : 10/21/2015 8:11:00 AM
```

This command parses the scheduled jobs in the C:\Windows\Tasks\GoogleUpdateTaskMachineUA.job file.

## PARAMETERS

### -Path
Path to file to be parsed.

```yaml
Type: String
Parameter Sets: ByPath
Aliases: FullName

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -VolumeName
Specifies the name of the volume or logical partition.

Enter the volume name in one of the following formats: \\.\C:, C:, or C.

```yaml
Type: String
Parameter Sets: ByVolume
Aliases: 

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### System.String


## OUTPUTS

### System.String

## NOTES

## RELATED LINKS


# Get-ForensicShellLink

## SYNOPSIS
Gets infromation about Shell Link (.LNK) files on the specified volume.

## SYNTAX

### ByVolume
```
Get-ForensicShellLink [[-VolumeName] <String>]
```

### ByPath
```
Get-ForensicShellLink -Path <String>
```

## DESCRIPTION
The Get-ForensicShellLink cmdlet parses the binary structure in the specified ShellLink (.lnk) file. If you do not specify a file, Get-ShellLink parses all .lnk files in the specified volume.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-ForensicShellLink
```

This command parses all .lnk files on the C:\ logical volume.

### Example 2
```
[ADMIN]: PS C:\> Get-ShellLink -Path C:\test\PowerForensics.dll-Help.xml.lnk


Path                      : PowerForensics.dll-Help.xml.lnk
CreationTime              : 11/6/2015 8:01:39 PM
AccessTime                : 11/16/2015 2:45:45 AM
WriteTime                 : 11/17/2015 10:18:59 PM
FileSize                  : 202700
LocalBasePath             : C:\test\PowerForensics.dll-Help.xml
CommandLineArguments      :
CommonNetworkRelativeLink :
```

This command, which runs Get-ForensicShellLink with a single file path, gets only the corresponding ShellLink object.

## PARAMETERS

### -Path
Path to file to be parsed.

```yaml
Type: String
Parameter Sets: ByPath
Aliases: FullName

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -VolumeName
Specifies the name of the volume or logical partition.

Enter the volume name in one of the following formats: \\.\C:, C:, or C.

```yaml
Type: String
Parameter Sets: ByVolume
Aliases: 

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### None


## OUTPUTS

### PowerForensics.Artifacts.ShellLink

## NOTES

## RELATED LINKS


# Get-ForensicShimcache

## SYNOPSIS
Gets previously run commands from the Shimcache forensic artifact.

## SYNTAX

### ByVolume
```
Get-ForensicShimcache [[-VolumeName] <String>]
```

### ByPath
```
Get-ForensicShimcache -HivePath <String>
```

## DESCRIPTION
The Get-ForensicShimcache cmdlet parses the AppCompatCache (AppCompatibility on XP) registry value to derive applications that were recently used. If you don&apos;t specify a hive path (-HivePath), the cmdlet parses the local System hive.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-ForensicShimcache
```

This example shows Get-ForensicShimcache being run against the default System Hive (C:\Windows\system32\config\SYSTEM)

### Example 2
```
[ADMIN]: PS C:\> Get-ForensicShimcache -HivePath C:\evidence\system
```

This is an example of Get-ForensicShimcache taking an exported SYSTEM hive as an argument.

## PARAMETERS

### -HivePath
Registry hive to parse.

```yaml
Type: String
Parameter Sets: ByPath
Aliases: Path

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -VolumeName
Specifies the name of the volume or logical partition.

Enter the volume name in one of the following formats: \\.\C:, C:, or C.

```yaml
Type: String
Parameter Sets: ByVolume
Aliases: 

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### None


## OUTPUTS

### PowerForensics.Artifacts.Shimcache

## NOTES

## RELATED LINKS


# Get-ForensicSid

## SYNOPSIS
Gets the system's Security Identifier (SID).

## SYNTAX

### ByVolume
```
Get-ForensicSid [[-VolumeName] <String>]
```

### ByPath
```
Get-ForensicSid -HivePath <String>
```

## DESCRIPTION
The Get-ForensicSid cmdlet parses the SAM hive to derive the system's Security Identifier.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-ForensicSid | Format-List

BinaryLength     : 24
AccountDomainSid : S-1-5-21-390730339-1025693957-1587674390
Value            : S-1-5-21-390730339-1025693957-1587674390
```

This command parses the C:\Windows\system32\config\SAM hive and returns the results in a list.

### Example 2
```
[ADMIN]: PS C:\> Get-ForensicSid -HivePath C:\Windows\System32\config\SAM

BinaryLength     : 24
AccountDomainSid : S-1-5-21-390730339-1025693957-1587674390
Value            : S-1-5-21-390730339-1025693957-1587674390
```

This command uses the HivePath parameter of Get-ForensicSid to specify an exported SAM hive to parse.

## PARAMETERS

### -HivePath
Registry hive to parse.

```yaml
Type: String
Parameter Sets: ByPath
Aliases: Path

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -VolumeName
Specifies the name of the volume or logical partition.

Enter the volume name in one of the following formats: \\.\C:, C:, or C.

```yaml
Type: String
Parameter Sets: ByVolume
Aliases: 

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### None


## OUTPUTS

### System.Security.Principal.SecurityIdentifier

## NOTES

## RELATED LINKS


# Get-ForensicTimeline

## SYNOPSIS
Creates a forensic timeline.

## SYNTAX

```
Get-ForensicTimeline [[-VolumeName] <String>]
```

## DESCRIPTION
The Get-ForensicTimeline cmdlet creates a forensic timeline for the selected volume or logical drive. It runs several PowerForensics cmdlets and returns all results as ForensicTimeline objects, instead of objects of different types. The result is a forensic timeline, that is, is a chronology of diagnostic events.

The cmdlets that Invoke-ForensicTimeline runs include:
-- Get-ForensicScheduledJob
-- Get-ForensicShellLink
-- Get-ForensicUsnJrnl
-- Get-ForensicEventLog
-- Get-ForensicRegistryKey

The cmdlet returns data that includes MFT file record, registry keys, Amcache, event logs, and much more.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-ForensicTimeline -VolumeName C
```

This command creates a forensic timeline for the C: volume on the local system.

### Example 2
```
[ADMIN]: PS C:\> $t = Get-ForensicTimeline -VolumeName D:

PS C:\&gt; $t[0]

Date         : 1/1/1999 12:00:00 AM
ActivityType : MACB
Source       : SCHEDULEDJOB
SourceType   :
User         : Server01\User01
FileName     : C:\Program Files (x86)\Dropbox\Update\DropboxUpdate.exe
Description  : [PROGRAM EXECUTION] C:\Program Files (x86)\Dropbox\Update\DropboxUpdate.exe executed
               at 1/1/1999 12:00:00 AM via Scheduled Job
```

This example shows the properties of the ForensicTimeline object. Invoke-ForensicTimeline returns the results of the disparate cmdlets in the same object type.

The first command command creates a forensic timeline for the D: volume on the local system and saves the results in the $t variable.

The second command displays the properties of the first object in $t, which was produced by the Get-ForensicScheduledJob cmdlet.

### Example 3
```
[ADMIN]: PS C:\> Get-ForensicTimeline -VolumeName \\.\C: | Group-Object -Property Source | Format-Table Count, Name

  Count Name
  ----- ----
      4 SCHEDULEDJOB
   1916 ShellLink
1276123 MFT
 293715 USNJRNL
   9319 EVENTLOG
 423900 REGISTRY
```

This command runs Invoke-ForensicTimeline on the C: drive. Then, it groups the objects by the value of their Source property so you can see the cmdlets that were run to produce the data, and it formats the results into a table of Count and Name, so the values of these properties are not truncated.

The output of this command varies based on the system and drive contents.

### Example 4
```
[ADMIN]: PS C:\> Get-ForensicTimeline | Sort-Object -Property Date
```

The command returns the output of Invoke-ForensicTimeline in chronological order to produce a true timeline of the events.

## PARAMETERS

### -VolumeName
Specifies the volume or logical partition that Invoke-ForensicTimeline analyzes. 

Enter the volume name in one of the following formats: \\.\C:, C:, or C.

```yaml
Type: String
Parameter Sets: (All)
Aliases: 

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### None


## OUTPUTS

### PowerForensics.Formats.ForensicTimeline

## NOTES

## RELATED LINKS


# Get-ForensicTimezone

## SYNOPSIS
Gets the system's timezone.

## SYNTAX

### ByVolume
```
Get-ForensicTimezone [[-VolumeName] <String>]
```

### ByPath
```
Get-ForensicTimezone -HivePath <String>
```

## DESCRIPTION
The Get-ForensicTimezone cmdlet parses the SYSTEM hive or a hive that you specify to derive the system's current timezone.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-ForensicTimezone

RegistryTimezone              dotNetStandardTimezone        dotNetDaylightTimezone                 IsDaylightSavingTime
----------------              ----------------------        ----------------------                 --------------------
Eastern Standard Time         Eastern Standard Time         Eastern Daylight Time                                 False
```

This command gets the time zones from the system hive.

### Example 2
```
[ADMIN]: PS C:\> Get-Timezone -HivePath C:\evidence\SYSTEM

RegistryTimezone              dotNetStandardTimezone        dotNetDaylightTimezone                 IsDaylightSavingTime
----------------              ----------------------        ----------------------                 --------------------
Eastern Standard Time         Eastern Standard Time         Eastern Daylight Time                                 False
```

This command gets the time zones from an exported SYSTEM hive.

## PARAMETERS

### -HivePath
Registry hive to parse.

```yaml
Type: String
Parameter Sets: ByPath
Aliases: Path

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -VolumeName
Specifies the name of the volume or logical partition.

Enter the volume name in one of the following formats: \\.\C:, C:, or C.

```yaml
Type: String
Parameter Sets: ByVolume
Aliases: 

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### None


## OUTPUTS

### PowerForensics.Artifacts.Timezone

## NOTES

## RELATED LINKS


# Get-ForensicTypedUrl

## SYNOPSIS
Gets the Universal Resource Locators (URL) that have been typed in the Internet Explorer browser.

## SYNTAX

### ByVolume
```
Get-ForensicTypedUrl [[-VolumeName] <String>]
```

### ByPath
```
Get-ForensicTypedUrl -HivePath <String>
```

## DESCRIPTION
The Get-ForensicTypedUrl cmdlet parses a user's NTUSER.DAT file to derive the Universal Resource Locators (URL) that have been typed into the Internet Explorer browser.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.}

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-ForensicTypedUrl -VolumeName \\.\C:
```

This command gets the URLs typed into Internet Explorer from all user's NTUSER.DAT hives on the C: logical volume.

### Example 2
```
[ADMIN]: PS C:\> Get-ForensicTypedUrl -HivePath C:\Users\Public\NTUSER.DAT
```

This command gets the URLs typed into Internet Explorer from the C:\Users\Public\NTUSER.DAT hive.

## PARAMETERS

### -HivePath
Registry hive to parse.

```yaml
Type: String
Parameter Sets: ByPath
Aliases: Path

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -VolumeName
Specifies the name of the volume or logical partition.

Enter the volume name in one of the following formats: \\.\C:, C:, or C.

```yaml
Type: String
Parameter Sets: ByVolume
Aliases: 

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### None


## OUTPUTS

### System.String

## NOTES

## RELATED LINKS


# Get-ForensicUnallocatedSpace

## SYNOPSIS
Gets the unallocated space on the specified partition/volume.

## SYNTAX

```
Get-ForensicUnallocatedSpace [[-VolumeName] <String>] [-Path <UInt64>]
```

## DESCRIPTION
The Get-ForensicUnallocatedSpace cmdlet parses the $Bitmap file to find clusters that are marked as unallocated (not in use by the file system). Then, the cmdlet returns the unallocated clusters as a byte array.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-ForensicUnallocatedSpace -VolumeName \\.\Z:
```

This command gets a byte array of unallocated clusters in the \\.\Z: volume.

## PARAMETERS

### -Path
Path to $Bitmap file.

```yaml
Type: UInt64
Parameter Sets: (All)
Aliases: FullName

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -VolumeName
Specifies the name of the volume or logical partition.

Enter the volume name in one of the following formats: \\.\C:, C:, or C.

```yaml
Type: String
Parameter Sets: (All)
Aliases: 

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### None


## OUTPUTS

### System.Byte[]

## NOTES

## RELATED LINKS


# Get-ForensicUserAssist

## SYNOPSIS
Gets the UserAssist entries from the specified volume.

## SYNTAX

### ByVolume
```
Get-ForensicUserAssist [[-VolumeName] <String>]
```

### ByPath
```
Get-ForensicUserAssist -HivePath <String>
```

## DESCRIPTION
The Get-ForensicUserAssist cmdlet parses the NTUSER.DAT registry hive to derive applications that were recently used by a particular user.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-ForensicUserAssist -VolumeName \\.\C:
```

This command gets applications that the Public user used from all user's NTUSER.DAT hives on the C: logical volume.

### Example 2
```
[ADMIN]: PS C:\> Get-ForensicUserAssist -HivePath C:\Users\Public\NTUSER.DAT
```

This command gets applications that the Public user used from the C:\Users\Public\NTUSER.DAT hive.

## PARAMETERS

### -HivePath
Registry hive to parse.

```yaml
Type: String
Parameter Sets: ByPath
Aliases: Path

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -VolumeName
Specifies the name of the volume or logical partition.

Enter the volume name in one of the following formats: \\.\C:, C:, or C.

```yaml
Type: String
Parameter Sets: ByVolume
Aliases: 

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### None


## OUTPUTS

### PowerForensics.Artifacts.UserAssist

## NOTES

## RELATED LINKS


# Get-ForensicUsnJrnl

## SYNOPSIS
Gets the UsnJrnl entries from the specified volume.

## SYNTAX

### ByVolume
```
Get-ForensicUsnJrnl [[-VolumeName] <String>] [-Usn <Int64>]
```

### ByPath
```
Get-ForensicUsnJrnl -Path <String> [-Usn <Int64>]
```

## DESCRIPTION
The Get-ForensicUsnJrnl cmdlet parses the $UsnJrnl file&apos;s $J data stream to return UsnJrnl entries. If you do not specify a Usn (Update Sequence Number), it returns all entries in the $UsnJrnl.

The $UsnJrnl file maintains a record of all file system operations that have occurred. Because the file is circular, entries are overwritten.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> $usn = Get-ForensicUsnJrnl
```

This command gets the file system operations on the C:\ logical volume.

### Example 2
```
[ADMIN]: PS C:\> $r = Get-ForensicFileRecord C:\temp\helloworld.txt
[ADMIN]: PS C:\> $r.Attribute[0].UpdateSequenceNumber
713538320

[ADMIN]:PS C:\> Get-ForensicUsnJrnl -Usn $r.Attribute[0].UpdateSequenceNumber

VolumePath               : \\.\C:
Version                  : 2.0
RecordNumber             : 132245
FileSequenceNumber       : 52
ParentFileRecordNumber   : 191621
ParentFileSequenceNumber : 59
Usn                      : 713538320
TimeStamp                : 11/17/2015 10:02:56 PM
Reason                   : DATA_EXTEND, FILE_CREATE, CLOSE
SourceInfo               : 0
SecurityId               : 0
FileAttributes           : ARCHIVE
FileName                 : helloworld.txt
```

This example uses Get-ForensicFileRecord and Get-ForensicUsnJrnl to get the UsnJrnl entries in the helloworld.txt file.

The first command gets the file record entries in the helloworld.txt files. The second command gets the USN of the first attribute in the Ntfs.FileRecord object that Get-ForensicFileRecord returns.
The third command uses Get-ForensicUsnJrnl to get the UsnJrnl record for the USN.

A file's most recent entry number can be found in its MFT FileRecord's $STANDARD_INFORMATION attribute.

### Example 3
```
[ADMIN]: PS C:\> $usn = Get-ForensicUsnJrnl -Path C:\evidence\UsnJrnl
```

This command get the UsnJrnl record of an exported UsnJrnl file.

## PARAMETERS

### -Path
Path to file to be parsed.

```yaml
Type: String
Parameter Sets: ByPath
Aliases: FullName

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -Usn
The Update Sequence Number of the record to return.

```yaml
Type: Int64
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -VolumeName
Specifies the name of the volume or logical partition.

Enter the volume name in one of the following formats: \\.\C:, C:, or C.

```yaml
Type: String
Parameter Sets: ByVolume
Aliases: 

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### System.String


## OUTPUTS

### PowerForensics.Ntfs.UsnJrnl

## NOTES

## RELATED LINKS


# Get-ForensicUsnJrnlInformation

## SYNOPSIS
Gets metadata about the specified volume's $UsnJrnl.

## SYNTAX

### ByVolume
```
Get-ForensicUsnJrnlInformation [[-VolumeName] <String>] [-AsBytes]
```

### ByPath
```
Get-ForensicUsnJrnlInformation -Path <String> [-AsBytes]
```

## DESCRIPTION
The Get-ForensicUsnJrnlInformation cmdlet parses the $UsnJrnl file&apos;s $MAX data stream and returns metadata about the UsnJrnl configuration.

By default, this cmdlet parses the $UsnJrnl file on the C:\ drive. To specify a drive, use the
VolumeName parameter. To specify an exported $UsnJrnl file, use the Path parameter.

You can also use the AsBytes parameter to get the metadata in byte format.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-ForensicUsnJrnlInformation

   MaxSize    AllocationDelta                 UsnId
   -------    ---------------                 -----
  33554432            8388608    130547872109887937
```

This command gets metadata about the $UsnJrnl on the C:\ logical volume.

### Example 2
```
[ADMIN]: PS C:\> Get-ForensicUsnJrnlInformation -Path C:\evidence\UsnJrnl

   MaxSize    AllocationDelta                 UsnId
   -------    ---------------                 -----
  33554432            8388608    130547872109887937
```

This command gets metadata about the $UsnJrnl on an exported UsnJrnl file.

### Example 3
```
[ADMIN]: PS C:\> Get-UsnJrnlInformation -AsBytes | Format-ForensicHex

Offset     _00_01_02_03_04_05_06_07_08_09_0A_0B_0C_0D_0E_0F  Ascii
------     ------------------------------------------------  -----
0x00000000  00 00 00 02 00 00 00 00 00 00 80 00 00 00 00 00  ................
0x00000010  C1 01 4B 17 99 CC CF 01 00 00 00 00 00 00 00 00  ..K.............
```

This command gets the gets metadata about the $Max data stream as a byte array.

## PARAMETERS

### -AsBytes
Returns the $UsnJrnl $Max data stream as byte array instead of as a UsnJrnlDetail object.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Path
Path to file to be parsed.

```yaml
Type: String
Parameter Sets: ByPath
Aliases: FullName

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -VolumeName
Specifies the name of the volume or logical partition.

Enter the volume name in one of the following formats: \\.\C:, C:, or C.

```yaml
Type: String
Parameter Sets: ByVolume
Aliases: 

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### System.String


## OUTPUTS

### PowerForensics.Ntfs.UsnJrnlDetail

## NOTES

## RELATED LINKS


# Get-ForensicVolumeBootRecord

## SYNOPSIS
Gets the Volume Boot Record from the specified volume.

## SYNTAX

### ByVolume
```
Get-ForensicVolumeBootRecord [[-VolumeName] <String>] [-AsBytes]
```

### ByPath
```
Get-ForensicVolumeBootRecord -Path <String> [-AsBytes]
```

## DESCRIPTION
The Get-ForensicVolumeBootRecord cmdlet reads the first 512 bytes (first sector) of the Logical Volume, also known as the Volume Boot Record, and parses its data structure to return a VolumeBootRecord object.

By default, this cmdlet parses the $Boot file on the C:\ drive. To specify the target drive, use the VolumeName parameter. To specify an exported $Boot file, use the Path parameter.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-ForensicVolumeBootRecord-VolumeName C


Signature             : NTFS    
BytesPerSector        : 512
SectorsPerCluster     : 8
ReservedSectors       : 0
MediaDescriptor       : 248
SectorsPerTrack       : 63
NumberOfHeads         : 255
HiddenSectors         : 2048
TotalSectors          : 125825023
LCN_MFT               : 786432
LCN_MFTMirr           : 2
ClustersPerFileRecord : 246
ClustersPerIndexBlock : 1
VolumeSN              : E3133CD4233CD4CA
Code                  : {0, 0, 0, 0...}
```

This command gets the VolumeBootRecord object for the C drive.

### Example 2
```
[ADMIN]: PS C:\> Get-ForensicVolumeBootRecord -VolumeName C: -AsBytes | Format-ForensicHex

Offset     _00_01_02_03_04_05_06_07_08_09_0A_0B_0C_0D_0E_0F  Ascii
------     ------------------------------------------------  -----
0x00000000  EB 52 90 4E 54 46 53 20 20 20 20 00 02 08 00 00  .R.NTFS    .....
0x00000010  00 00 00 00 00 F8 00 00 3F 00 FF 00 00 08 00 00  ........?.......
0x00000020  00 00 00 00 80 00 80 00 FF EF 7F 07 00 00 00 00  ................
0x00000030  00 00 0C 00 00 00 00 00 02 00 00 00 00 00 00 00  ................
0x00000040  F6 00 00 00 01 00 00 00 E3 13 3C D4 23 3C D4 CA  ..........&lt;.#&lt;..
0x00000050  00 00 00 00 FA 33 C0 8E D0 BC 00 7C FB 68 C0 07  .....3.....|.h..
0x00000060  1F 1E 68 66 00 CB 88 16 0E 00 66 81 3E 03 00 4E  ..hf......f.&gt;..N
0x00000070  54 46 53 75 15 B4 41 BB AA 55 CD 13 72 0C 81 FB  TFSu..A..U..r...
0x00000080  55 AA 75 06 F7 C1 01 00 75 03 E9 DD 00 1E 83 EC  U.u.....u.......
0x00000090  18 68 1A 00 B4 48 8A 16 0E 00 8B F4 16 1F CD 13  .h...H..........
0x000000A0  9F 83 C4 18 9E 58 1F 72 E1 3B 06 0B 00 75 DB A3  .....X.r.;...u..
0x000000B0  0F 00 C1 2E 0F 00 04 1E 5A 33 DB B9 00 20 2B C8  ........Z3... +.
0x000000C0  66 FF 06 11 00 03 16 0F 00 8E C2 FF 06 16 00 E8  f...............
0x000000D0  4B 00 2B C8 77 EF B8 00 BB CD 1A 66 23 C0 75 2D  K.+.w......f#.u-
0x000000E0  66 81 FB 54 43 50 41 75 24 81 F9 02 01 72 1E 16  f..TCPAu$....r..
0x000000F0  68 07 BB 16 68 52 11 16 68 09 00 66 53 66 53 66  h...hR..h..fSfSf
0x00000100  55 16 16 16 68 B8 01 66 61 0E 07 CD 1A 33 C0 BF  U...h..fa....3..
0x00000110  0A 13 B9 F6 0C FC F3 AA E9 FE 01 90 90 66 60 1E  .............f`.
0x00000120  06 66 A1 11 00 66 03 06 1C 00 1E 66 68 00 00 00  .f...f.....fh...
0x00000130  00 66 50 06 53 68 01 00 68 10 00 B4 42 8A 16 0E  .fP.Sh..h...B...
0x00000140  00 16 1F 8B F4 CD 13 66 59 5B 5A 66 59 66 59 1F  .......fY[ZfYfY.
0x00000150  0F 82 16 00 66 FF 06 11 00 03 16 0F 00 8E C2 FF  ....f...........
0x00000160  0E 16 00 75 BC 07 1F 66 61 C3 A1 F6 01 E8 09 00  ...u...fa.......
0x00000170  A1 FA 01 E8 03 00 F4 EB FD 8B F0 AC 3C 00 74 09  ............&lt;.t.
0x00000180  B4 0E BB 07 00 CD 10 EB F2 C3 0D 0A 41 20 64 69  ............A di
0x00000190  73 6B 20 72 65 61 64 20 65 72 72 6F 72 20 6F 63  sk read error oc
0x000001A0  63 75 72 72 65 64 00 0D 0A 42 4F 4F 54 4D 47 52  curred...BOOTMGR
0x000001B0  20 69 73 20 63 6F 6D 70 72 65 73 73 65 64 00 0D   is compressed..
0x000001C0  0A 50 72 65 73 73 20 43 74 72 6C 2B 41 6C 74 2B  .Press Ctrl+Alt+
0x000001D0  44 65 6C 20 74 6F 20 72 65 73 74 61 72 74 0D 0A  Del to restart..
0x000001E0  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0x000001F0  00 00 00 00 00 00 8A 01 A7 01 BF 01 00 00 55 AA  ..............U.
```

This commands get the bytes that represent the Volume Boot Record as a byte array.

## PARAMETERS

### -AsBytes
Returns Volume Boot Record as byte array instead of as VolumeBootRecord object.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Path
Path to file to be parsed.

```yaml
Type: String
Parameter Sets: ByPath
Aliases: FullName

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -VolumeName
Specifies the name of the volume or logical partition.

Enter the volume name in one of the following formats: \\.\C:, C:, or C.

```yaml
Type: String
Parameter Sets: ByVolume
Aliases: 

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### None


## OUTPUTS

### PowerForensics.Ntfs.VolumeBootRecord

## NOTES

## RELATED LINKS


# Get-ForensicVolumeInformation

## SYNOPSIS
Gets information about the specified volume.

## SYNTAX

### ByVolume
```
Get-ForensicVolumeInformation [[-VolumeName] <String>]
```

### ByPath
```
Get-ForensicVolumeInformation -Path <String>
```

## DESCRIPTION
The Get-ForensicVolumeInformation cmdlet parses the $Volume file&apos;s $VOLUME_INFORMATION attribute to return the metadata about the specified volume.

By default, the cmdlet parses the $Volume file on the C:\ drive. To specify an alternate target drive, use the -VolumeName parameter. To specify an exported $Volume file, use the -Path parameter.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-ForensicVolumeInformation

Name    : VOLUME_INFORMATION
Version : 3.1
Flags   : 0
```

This command gets the metadata about the C:\ logical volume.

### Example 2
```
[ADMIN]: PS C:\> Get-ForensicVolumeInformation -Path 'C:\evidence\$Volume'
```

This command gets metadata about an exported volume file, C:\evidence\$Volume.

## PARAMETERS

### -Path
Path to file to be parsed.

```yaml
Type: String
Parameter Sets: ByPath
Aliases: FullName

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -VolumeName
Specifies the name of the volume or logical partition.

Enter the volume name in one of the following formats: \\.\C:, C:, or C.

```yaml
Type: String
Parameter Sets: ByVolume
Aliases: 

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### System.String


## OUTPUTS

### PowerForensics.Ntfs.VolumeInformation

## NOTES

## RELATED LINKS


# Get-ForensicVolumeName

## SYNOPSIS
Gets the name of the specified volume.

## SYNTAX

### ByVolume
```
Get-ForensicVolumeName [[-VolumeName] <String>]
```

### ByPath
```
Get-ForensicVolumeName -Path <String>
```

## DESCRIPTION
The Get-ForensicVolumeName cmdlet parses the $Volume file's $VOLUME_NAME attribute to return the name of the specified volume.

By default, the cmdlet parses the $Volume file on the C:\ drive. To specify an alternate target drive, use the VolumeName parameter. To specify an exported $Volume file, use the Path parameter.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-VolumeName -VolumeName \\.\C:

VolumeNameString
----------------
testdrive
```

This command gets the name of the C:\ logical volume.

### Example 2
```
[ADMIN]: PS C:\> Get-VolumeName -Path 'C:\evidence\$Volume'

VolumeNameString
----------------
testdrive
```

This command gets the name of the volume in C:\evidence\$Volume file, and exported $Volume file.

## PARAMETERS

### -Path
Path to file to be parsed.

```yaml
Type: String
Parameter Sets: ByPath
Aliases: FullName

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -VolumeName
Specifies the name of the volume or logical partition.

Enter the volume name in one of the following formats: \\.\C:, C:, or C.

```yaml
Type: String
Parameter Sets: ByVolume
Aliases: 

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### System.String


## OUTPUTS

### PowerForensics.Ntfs.VolumeName

## NOTES

## RELATED LINKS


# Get-ForensicWindowsSearchHistory

## SYNOPSIS
Gets the search terms that have been searched for using the Windows Search feature.

## SYNTAX

### ByVolume
```
Get-ForensicWindowsSearchHistory [[-VolumeName] <String>]
```

### ByPath
```
Get-ForensicWindowsSearchHistory -HivePath <String>
```

## DESCRIPTION
The Get-ForensicWindowsSearchHistory cmdlet parses a user&apos;s NTUSER.DAT file to derive the terms that have been searched for using the Windows Search feature.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Get-ForensicWindowsSearchHistory -VolumeName C:
```

This command gets the URLs typed into Internet Explorer from all user's NTUSER.DAT hives on the C: logical volume.

### Example 2
```
[ADMIN]: PS C:\> Get-ForensicWindowsSearchHistory -HivePath C:\Users\Public\NTUSER.DAT
```

This command gets the URLs typed into Internet Explorer from the C:\Users\Public\NTUSER.DAT hive.

## PARAMETERS

### -HivePath
Registry hive to parse.

```yaml
Type: String
Parameter Sets: ByPath
Aliases: Path

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -VolumeName
Specifies the name of the volume or logical partition.

Enter the volume name in one of the following formats: \\.\C:, C:, or C.

```yaml
Type: String
Parameter Sets: ByVolume
Aliases: 

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### None


## OUTPUTS

### System.String

## NOTES

## RELATED LINKS


# Invoke-ForensicDD

## SYNOPSIS
Gets a byte-for-byte copy of a file, disk, or partition.

## SYNTAX

```
Invoke-ForensicDD [-InFile] <String> [[-OutFile] <String>] [[-Offset] <Int64>] [[-BlockSize] <UInt32>]
 [-Count] <UInt32>
```

## DESCRIPTION
The Invoke-DD cmdlet generates and returns an exact copy of a file, disk, or partition. 

Use the Offset (starting point), BlockSize (bytes/operation), and Count (# blocks) parameters to determine the segment of the InFile that is copied.

This cmdlet designed to work just like the popular dd Unix utility. For information about the dd utility, see "dd (Unix)" (https://en.wikipedia.org/wiki/Dd_%28Unix%29) in Wikipedia.

Except as noted, the cmdlets in the PowerForensics module require the permissions of a member of the Administrators group on the computer. To run them, start Windows PowerShell with the 'Run as administrator' option.

## EXAMPLES

### Example 1
```
[ADMIN]: PS C:\> Invoke-ForensicDD Invoke-DD -InFile \\.\PHYSICALDRIVE0 -Offset 0 -Count 1
```

This command copies the first sector of the Master Boot Record of the
\\.\PHYSICALDRIVE0 disk to the console.

The command uses the default values for OutFile (stdout; the Windows PowerShell console) and BlockSize (512; 1 sector).

### Example 2
```
[ADMIN]: PS C:\> Invoke-ForensicDD Invoke-DD -InFile \\.\HARDDISKVOLUME1 -OutFile C:\Users\Public\Desktop\MBR -Offset 512 -BlockSize 1024 -Count 3
```

This command copies three 1024-size blocks of the specified volume to a file in the C:\Users\Public\Desktop\MBR directory. It begins copying at the second sector (after the 512-byte offset).

It uses the Offset parameter to specify the starting point of the copy operation, the BlockSize parameter to specify the bytes per copy operation, and the Count parameter to specify the number of copy operations. 

It also uses the OutFile parameter to specify a location for the output. The default is writing to the Windows PowerShell console (stdout).

## PARAMETERS

### -BlockSize
Specifies the number of bytes to read/write in each operation. The default value is 512 (1 disc sector).

When reading from a device, such as \\.\PHYSICALDRIVE0 or \\.\C:, the value of BlockSize must be divisible by 512.

```yaml
Type: UInt32
Parameter Sets: (All)
Aliases: 

Required: False
Position: 3
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Count
Specifies the number of blocks that Invoke-ForensicDD reads from the file, disk, or partition. This parameter is required.

```yaml
Type: UInt32
Parameter Sets: (All)
Aliases: 

Required: True
Position: 4
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -InFile
Specifies the file, disk or partition to be copied, for example \\.\PHYSICALDRIVE0, \\.\HARDDISKVOLUME1, or \\.\C:. This parameter is required.

```yaml
Type: String
Parameter Sets: (All)
Aliases: 

Required: True
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Offset
Specifies the starting point in the file for the copy operation as a byte offset. This parameter is required.

```yaml
Type: Int64
Parameter Sets: (All)
Aliases: 

Required: False
Position: 2
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -OutFile
Writes the output to the specified file or directory. 

This parameter is optional. But default, Invoke-ForensicDD writes the output to standard ouptut ("stdout"), which is the Windows PowerShell console, but you can use this parameter or redirect the output.

```yaml
Type: String
Parameter Sets: (All)
Aliases: 

Required: False
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### None


## OUTPUTS

### System.Byte[]

## NOTES

## RELATED LINKS
