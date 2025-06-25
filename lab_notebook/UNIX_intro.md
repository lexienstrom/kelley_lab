# UNIX Basics: Text Processing with `awk`, `grep`, and `sed`

Today, we'll learn how to manipulate and analyze text files on the UNIX command line using:

- `awk`
- `grep`
- `sed`

We’ll use this file as our example:

---

### sample_info.txt

```
#Individual_Number Spawning_Depth Standard_Length Sex Colour
BL_100 4 35 M Blue
BL_101 5 32 F Blue
BL_102 4 36 M Blue
BL_400 4 34 M Blue
BL_432 10 41 F Blue
NR_700 24 18 F Red
NR_703 31 16 F Red
NR_704 33 19 F Red
NR_870 32 17 M Red
NR_871 31 18 F Red
```

### Concept:
- `awk` splits each line into columns (fields).
- By default, it splits on whitespace or tabs.
- `$1` is the first field, `$2` the second, and so on.

### Example 1: Print just the Individual Number column

```bash
awk '{ print $1 }' sample_info.txt
```

### Example 2: Filter rows where Spawning_Depth > 20

```bash
awk '$2 > 20' sample_info.txt
```

Output
```
NR_700	24	18	F	Red
NR_703	31	16	F	Red
NR_704	33	19	F	Red
NR_870	32	17	M	Red
NR_871	31	18	F	Red
```
### Example 3: Calculate average Standard_Length

```
awk 'NR > 1 { sum += $3; count++ } END { print sum/count }' sample_info.txt
```

