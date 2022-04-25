## YASFS:

_This document still being retyped, and thus incomplete at this point_

This document speaks of the actual low level on disk structure of the two versions of the YASFS filesystem.  The small version is the one most often used, as it is a little faster than the full version, and it is rare to have volume sizes large enough to use the full version.

# Small, Fast, Version:

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


# Full Version:

Do to not having any volumes larger than 8TB to work with this version has minimal testing and the current implementation may fail.  This is to the point that I may not release the full version yet.

YASFS is a simple extents based Filesystem that supports up to 2 data streams (forks) per file, has a date format that includes a 32-bit days since January 1st 1950 value and a seperate 24-bit centaseconds into the day value.  There is a free-space map per volume, this is a set of extents that each represent an unused portion of space.  The FreeSpace map is just extent blocks, where the unused 6 bytes of a regular extents block is the cluster number of the next extents block of the free-space map.

The root block of YASFS gives the locations of the free-space map, the root directory, and the information on the logical volume.  It also contains the offset on the physical media to either the rootblock of the next YASFS volume on the same volume, or a forign partition type, or 0 for this being the last partition.

The root block may be anywhere in the first 8192 physical sectors of the volume.  The structure of the root block is:
```c
typedef struct {
  UINT32 Magic;    /* Magic number, should be the ASCII string "YASF". */
  UINT32 day;      /* Day of creation of rootblock in days since 1950. */
  UINT32 time;     /* Creation time, centaseconds since midnight. */
  UINT32 lvsize;   /* Low 32-bits of volume size in clusters. */
  UINT16 hvsize;   /* High 16-bits of volume size in clusters. */
  UINT16 clsz;     /* Size in bytes of allocation cluster. */
  UINT32 freemap;  /* Cluster where free-space map begins. */
  UINT32 rootdir;  /* Cluster where the rootdirectory starts. */
  UINT32 padd[1004]; /* Padding to make block 4096 bytes long. */
  char   name[32]; /* Volume name. */
  UINT64 nxtyas;  /* Offset from here to next YASFS volume rootblock. */
  UINT64 prvyas;  /* Offset from here to last YASFS volume rootblock. */
}YASFSROOT;
```
By default YASFS uses 4096 byte clusters, this is also the minimum cluster size in YASFS.  Using the default cluster size the maximum volume size is 1EB (1 ExaByte = 1024 PetaBytes = 1048576 TeraBytes), in other words more than we are likely to see possible for a good long time.

YASFS directory entries contain the filename (up to 31-characters), language selector, creation timestamp, last modified timestamp, the extent pointer and length for each data stream, extent pointer type of each data stream, and a flags word.  A directory entry can point to a file or a directory, this is a fully hierachical file system.  The purpose of extent types is so that an extent may point to an extent block allowing more than one extent per file, then the entries of the extent block point to data extents for a maximum of 409 extents per file (extent block is always 4096 bytes, as that is the default cluster size). 

The directory entry of YASFS is extremely simple, and 64 bytes in size:

```c
typedef struct {
  char   name[31];/* File name. */
  char   lang;    /* What high bit character set to use. */
  UINT32 flags;   /* Top 2 bits specify extent types, low 30-bits flags. */
  UINT32 time;    /* Centaseconds since midnight. */
  UINT32 day;     /* Days since Jan 1st 1950. */
  UINT16 str0h;   /* High 16 bytes of cluster numbers.
  UINT16 str1h;
  UINT32 str0l;   /* Stream 0 first cluster (or extent block cluster). */
  UINT32 len0;    /* Stream 0 length in bytes. */
  UINT32 str1l;   /* Stream 1 first cluster (or extent block cluster). */
  UINT32 len1;    /* Stream 1 length in bytes. */
}YASDIRENT;
```

If a stream has multiple extents (uses an extent block) then the length for that stream should be set to the cluster size (extent block is one cluster).  Then the stream size is the total of the sizes of extents used refered to by the extent block.  This means a stream can be up to a bit over 1.5TB (1636GB) in size if it uses all 409 extents and the volume is large enough.  The upper 2 bits of the flags word is used to determine for each extent if it is just a single extent or uses an extents block (set for extents block), where bit 30 is for stream 0, bit 31 for stream 1.

Each extent block is a list of extents with the first 48-bits of each entry being the starting cluster and the last 32-bits of each entry being the length of the extent in bytes.  For some systems the remaining 6 bytes in the extent block can be used for metadata (like file and creater type information or similar).

Each directory consists of a list of directory entries, with the first invisable entry pointing to the parrent directory.  Before the first entry is a sinble 32-bit value, with the bottom 10 bits used to specify the number of entries in the directory table, bits 10 through 19 give the number of used entries in the directory, bits 20 through 32 are currently unused and should be 0, there is a 60 byte unused space between the header word and the first entry, to keep the directory entries 64-byte aligned.
