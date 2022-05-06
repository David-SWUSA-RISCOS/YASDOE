## YASFS:

_This document still being retyped, and thus incomplete at this point_

This document speaks of the actual low level on disk structure of the two versions of the YASFS filesystem.  The small version is the one most often used, as it is a little faster than the full version, and it is rare to have volume sizes large enough to use the full version.



YASFS is a simple extents based Filesystem that supports up to two data streams (forks) per file, has a date format that includes a 32-bit days since Jan 1st 1950 value and a seperate 24-bit centaseconds into the day value.  The free-space map for the fast version is stored as a bitmap, where there is one bit per cluster and the bit being set represents used space cleared free-space.  The free-space bitmap starts in the cluster after the root block.  This is the prefered version of the YASFS File System, as it is a good bit faster than the full version.  This is also the version that is required for the bootable volume.

Because the root block has the offset to the next volume in 4096 byte clusters, you can have multiple volumes on a single partition on a storage device.  This could be looked as a form of sub-partition support.

Clusters are always 2048 bytes in the fast version of YASFS, with 32-bit indexing thus allowing for two to the fourty-third power bytes volume sizes (8TB (8192GB)), with potentially infinate number of volumes (the implementation limits to a maximum of 64 volumes).  File sizes are determined by the sum of all extents, each file can have up to 256 extents for a maximum file size of 1TB (1024GB)(minus 256 bytes).  This is a very simple filesystem.

The root block must be located as the second block on a partition, and takes the form:
```c
typedef struct {
  UINT32 Magic;     /* Magic number, should be the ASCII string "YFSF". */
  UINT32 day;       /* Day of creation of rootblock in days since 1950. */
  UINT32 time;      /* Creation time, centaseconds since midnight. */
  UINT32 lvsize;    /* Volume size in clusters. */
  UINT32 rootdir;   /* Cluster where the rootdirectory starts. */
  UINT32 padd[497]; /* Padding to make block 2048 bytes long. */
  char   name[32];  /* Volume name. */
  UINT32 nxtyas;    /* Offset from here to next YASFS volume rootblock. */
  UINT32 prvyas;    /* Offset from here to last YASFS volume rootblock. */
}YFSROOT;
```

The directory entry format is:

```c
typedef struct {
  char   name[31];/* File name. */
  char   lang;    /* What high bit character set to use. */
  UINT32 types;   /* Type information word. */
  UINT32 flags;   /* Top 2 bits specify extent types, low 30-bits flags. */
  UINT32 time;    /* Centaseconds since midnight. */
  UINT32 day;     /* Days since Jan 1st 1950. */
  UINT32 str0;    /* Stream 0 first cluster (or extent block cluster). */
  UINT32 len0;    /* Stream 0 length in bytes. */
  UINT32 str1;    /* Stream 1 first cluster (or extent block cluster). */
  UINT32 len1;    /* Stream 1 length in bytes. */
}YFSDIRENT;
```

Either or both streams may be have zero size and null starting cluster meaning the stream is unused.  If both streams are null then the entry is not a file or directory, it is just a directory entry (can be used for informational purposes).

In the case of a file stream being less than 4GB (-1 byte), and being continuous series of clusters on the storage device, the extent points directly to the stream data, and the length represent the whole stream.  In the case of a file stream being fragmented or being larger than or equal to 4GB the stream extent points to an extents block, and the length is 1 cluster (2048 bytes, the size of the extents block).  An extents block is just 256 pairs of 32-bit values, where the first value in each pair is the cluster where the data begins and the second is the length of the extent in bytes.  The top two bits of the flags tell if str0 and str1 point at the data or to an extent block, with bit 30 being one for extents block on str0, and bit 31 being one for extents block on str1.  The maximum file size is 1TB minus 256 bytes.

So long as the character set selected is a single byte character set the name can be up to 31 characters long, null padded.  In the case of selecting Unicode for the high bit characters UTF-8 encoding is used, and multiple byte characters will decrease the maximum possible length of the file name, which still must be no more than 31 bytes.

There are no creation dates for files, only last modification dates.  This is intentional, as it aids in keeping the system simple.

The types feild is OS dependant.  It is not used in YASDOE, though it is used in GraFaDOE, and may be needed in other Operating Systems.

The low 30 bits of the flags (bits 00-1D) are:
```
BIT  :  MEANING
-----|----------------------------------
00   :  Owner Hold.
01   :  Owner Script.
02   :  Owner Pure.
03   :  Owner Archive.
04   :  Owner Read.
05   :  Owner Write.
06   :  Owner Execute.
07   :  Owner Delete.
08   :  Others Hold.
09   :  Others Script.
0A   :  Others Pure.
0B   :  Others Archive.
0C   :  Others Read.
0D   :  Others Write.
0E   :  Others Execute.
0F   :  Others Delete.
10-13:  Owner Handle.
14   :  Reserved.
15   :  Reserved.
16   :  Reserved.
17   :  Reserved.
18   :  Stream str1 is a Resource Fork (mac style).
19   :  Stream str1 is a Resource Fork (gs style).
1A   :  Uses Stream str1 for .info.
1B   :  Reserved
1C   :  Subdirectory.
1D   :  Being Updated (used to track potential sync loss).
```

A directory is a series of 256 directory entries occupying 8 continuous clusters (16KB).  The first cluster of the root directory is the first cluster after the end of the free-space bitmap.



