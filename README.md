# MOVED
Just use Notion to do development diaries. Markdown cannot split content into
pages which can make things nasty / unmanageable very soon.
---
## Intro
- Start Date : 20-Feb-2021
- Repo forked from : https://github.com/semigodking/redsocks 
- Commit forked from : `1951b49b774b0aab702348d0370e26bae1c3a7df`
- Current repo : https://github.com/wantMoreSleep/sleepy-redsocks

## Initial Problems
#### [`.v4`, `.v6` members do not exist in type `pf_addr`]
The current MacOS uses `xnu-4570` but the original `redsocks2` is based on
`xnu-3789` or earlier.
```c
// xnu-4570
struct pf_addr {
    union {
        struct in_addr          _v4addr;
        struct in6_addr         _v6addr;
        u_int8_t                _addr8[16];
        u_int16_t               _addr16[8];
        u_int32_t               _addr32[4];
    } pfa;              /* 128-bit address */
#define v4addr  pfa._v4addr
#define v6addr  pfa._v6addr
#define addr8   pfa._addr8
#define addr16  pfa._addr16
#define addr32  pfa._addr32
};
```
```c
// xnu-3789
struct pf_addr {
    union {
        struct in_addr		v4;
        struct in6_addr		v6;
        u_int8_t		addr8[16];
        u_int16_t		addr16[8];
        u_int32_t		addr32[4];
    } pfa;		    /* 128-bit address */
#define v4	pfa.v4
#define v6	pfa.v6
#define addr8	pfa.addr8
#define addr16	pfa.addr16
#define addr32	pfa.addr32
};
```
