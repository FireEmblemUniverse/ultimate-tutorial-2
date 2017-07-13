### Appendix: Nightmare Module Format

NMM format: # at line[0] means comment, ignore it.  blank lines are ignored
also.  decimal is assumed, 0x for hex, 0 for octal (0b for binary?)

    Line 1: file version, ignore it.
    Line 2: file description, ignore it.
    Line 3: address of table, no 0800:0000h
    Line 4: number of entries Line 5: length of each entry
    Line 6: text file of entry names, might be useful. Default to numbers if not found
    Line 7: tbl file for text, ignore it.

Entry format:
    
    Line 1: Description (use as header row?)
    Line 2: Offset
    Line 3: Length in bytes
    Line 4: Type of data (Only care about H or DU/DS imo)
    Line 5: Text file for descriptions, ignore it for now.

    NEHU: Numeric Editbox Hexadecimal Unsigned
    NEDU: Numeric Editbox Decimal Unsigned
    NEDS: Numeric Editbox Decimal Signed
    NDHU: Numeric Dropdown Hexadecimal Unsigned
    NDDU: Numeric Dropdown Decimal Unsigned

