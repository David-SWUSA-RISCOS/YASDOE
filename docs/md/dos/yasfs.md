## YASFS:

_This document still being retyped, and thus incomplete at this point_

YASFS is a simple extents based Filesystem that supports up to 2 data streams (forks) per file, has a date format that includes a 32-bit days since 1950 value and a seperate 24-bit centaseconds into the day value.  There is a free-space map per volume, this is a set of extents that each represent an unused portion of space.  The FreeSpace map is just extent blocks, where the unused 6 bytes of a regular extents block is the cluster number of the next extents block of the free-space map.

The root block of YASFS gives the locations of the free-space map, the root directory, and the information on the logical volume.  It also contains the offset on the physical media to either the rootblock of the next YASFS volume on the same volume, or a forign partition type, or 0 for this being the last partition.

The root block may be anywhere in the first 8192 physical sectors of the storage device.  The structure of the root block is:
'''c
typedef struct {
  UINT32 Magic;    /* Magic number, should be the ASCII string "YASF". */
  UINT32 day;      /* Day of creation of rootblock in days since 1950. */
  UINT32 time;     /* Creation time, centaseconds since midnight. */
  UINT32 lvsize;   /* Low 32-bits of volume size in clusters. */
  UINT16 hvsize;   /* High 16-bits of volume size in clusters. */
  UINT16 clsz;     /* Size in bytes of allocation cluster. */
  UINT32 bitmap;   /* Cluster where free-space bitmap begins. */
  UINT32 rootdir;  /* Cluster where the rootdirectory starts. */
  UINT32 padd[117]; /* Padding to make block 4096 bytes long. */
  UINT64 nxtyas;  /* Offset from here to next YASFS volume rootblock. */
  UINT64 prvyas;  /* Offset from here to last YASFS volume rootblock. */
}YASFSROOT;
'''
By default YASFS uses 4096 byte clusters, this is also the minimum cluster size in YASFS.  Using the default cluster size the maximum volume size is 1EB (1 ExaByte = 1024 PetaBytes = 1048576 TeraBytes), in other words more than we are likely to see possible for a good long time.

YASFS directory entries contain the filename (up to 31-characters), language selector, creation timestamp, last modified timestamp, the extent pointer and length for each data stream, extent pointer type of each data stream, and a flags word.  A directory entry can point to a file or a directory, this is a fully hierachical file system.  The purpose of extent types is so that an extent may point to an extent block allowing more than one extent per file, then the entries of the extent block point to data extents for a maximum of 409 extents per file (extent block is always 4096 bytes, as that is the default cluster size). 

The directory entry of YASFS is extremely simple, and 64 bytes in size:

'''c
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
'''

If a stream has multiple extents (uses an extent block) then the length for that stream should be set to the cluster size (extent block is one cluster).  Then the stream size is the total of the sizes of extents used refered to by the extent block.  This means a stream can be up to a bit over 1.5TB (1636GB) in size if it uses all 409 extents and the volume is large enough.  The upper 2 bits of the flags word is used to determine for each extent if it is just a single extent or uses an extents block (set for extents block), where bit 30 is for stream 0, bit 31 for stream 1.

Each extent block is a list of extents with the first 48-bits of each entry being the starting cluster and the last 32-bits of each entry being the length of the extent in bytes.  For some systems the remaining 6 bytes in the extent block can be used for metadata (like file and creater type information or similar).

Each directory consists of a list of directory entries, with the first invisable entry pointing to the parrent directory.  Before the first entry is a sinble 32-bit value, with the bottom 10 bits used to specify the number of entries in the directory table, bits 10 through 19 give the number of used entries in the directory, bits 20 through 32 are currently unused and should be 0, there is a 60 byte unused space between the header word and the first entry, to keep the directory entries 64-byte aligned.
