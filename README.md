# AUID

Absolute Unique IDentifier

### Why not uuid?

UUID is useful. It can be almost guaranteed to be unique even when generated in the client side. But that's all. We cannot insert any information about that key.

### What's auid?

AUID is a 32-length ASCII text, same length as UUID. Difference is, AUID uses Base64 encoded string instead of hexadecimal string. It enables AUID to contain more information in the same length.

### Wait, we don't need larger UUID!

Right, UUID is large enough. We don't need more.
AUID is not a just larger UUID. It's format is little bit complicate then UUID.

##### AUID's structure has 4 parts.

1. First character of AUID is custom mask. You can use any valid Base64 character(except '=') to mark your AUID's type.
1. Second character of AUID is century mask. This makes AUID usable until 63th century.
1. Next 6 characters means the time passed from the century begins in seconds.
1. Remaining 24 characters are Base64 encoded binary representation of traditional UUID.

Yes, custom mask and timestamp in the same size of the UUID. Until 83th century!

## AUID format

1. Standard
    - r-v-G7xhn2-6Q9NWXGqHopHX1bbmYEYppB
    - 1-1-6-24
    - custom-century-timestamp-uuid
1. Shortened
    - rvG7xhn26Q9NWXGqHopHX1bbmYEYppB
    - without '-'
1. Binary
    - AUID is also a valid Base64 encoded string. So it can be converted to 24-byte binary format.

## AUID specification

1. All characters in AUID must be a valid Base64 character(e.g. A-Za-z0-9+/).
1. First character is free-to-use field. There's no more limitation for this field.
1. Second character represent the century that this AUID is created.
    - Century count is started with 20th century. So 20th century takes 1st character of Base64.
    - ex) 2015 -> 21th century -> B
1. 3rd - 8th characters represent the timestamp from the century is begin in seconds that this AUID is created.
    - 3th - 8th characters are basically Base64 encoded 4byte number, but slightly modified.
    - 8rd character must be in the I-L(8th-12th character of Base64). This makes AUID not to valid UUID string(hexadecimal code never contains that character).
    - ex) 40726941 -> 0b 111100,101100,000001,100011,110111,11 -> 8sBj3L
1. 9th - 32th characters represent uid same as UUID range.
