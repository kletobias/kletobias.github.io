---
title: 'sed command'
subtitle: 'Learning Linux - Section 5.3'
date: 2021-12-28 00:00:00
description: 'This article covers some of the essential commands and / or concepts used in any Linux distribution. Vim text editor was used and CentOS 7 was the OS used in this series. It was setup as command line only virtual machine and accessed through ssh. There are 8 Sections in total.'
featured_image: bash-ga254901e3_1280.png
gallery_images: Bash_GNOME_Terminal_screenshot.png
accent_color: '#4C60E6'
---

<!---Gallery is used, when listing the articles, featured is the image placed at the top of the article.
-->
TODO insert correct title of this chapter and also the correct 5.x number.

### `sed` command

- `sed` replaces a string in a file with a new string.
- It can be used to find and delete a line of a file. Use cases are\:
  - Remove empty lines.
  - Remove the first line or `n` lines.
  - Replace tabs with spaces.
  - Show defined lines from a file.
  - Substitute \(replace) within vi editor.
  - And much more...

#### `sed 's/DDR/DNS/g FILE`

- Like this, the command does\:
  - `s` substitute
  - `DDR` with `DNS`
	- `g` - do this for all matches in the `FILE`.
	- It will not write the above changes to the file by default and will only show them on screen.

##### Example

The this text file is used in the following examples.

```vim
~ $ cat ddr4_vs_5
DDR5 is improvement to existing DDR4 and is similar to LPDDR4.

While DDR4 DIMMs (memory stick) are 64 bits (72 bits with ECC, so called buffered or registered) DDR5 moved to 2 x 32 bits or 2 x 40 bits for ECC. Btw LPDDR4 is 2 x 16 bits. DDR5 DIMM has two separate 32 bit channels, like two DDR4 DIMMs - single DDR5 DIMM is dual channel.

Additional improvement is number of burst transfers. While DDR4 is 4 or 8, LPDDR4 16 or 32, DDR5 increased to 16. By doubling bursts DDR5 despite 32 bits achieves DDR4 speeds. Btw in x86 CPU (and others too) cache line is 64 bytes what corresponds to DDR4 64 bits and 8 transfers.

Operating voltage is reduced from 1.2V to 1.1V what reduces power consumption, eg LPDDR4 is 1V. Additional features are added which speed up DDR5 further, eg number of banks, hidden refresh, etc.

Also memory sizes are increased. DDR4 per DIMM is 32GB while DDR5 increases this to 64GB and further.
Additionally transfer speeds are increased. Latest DDR4 is 3200/3600 (originally 2133 or 2166) while DDR5 starts at 4800, followed by 5200, 6000 and even 10000. Of course, latencies, famous CL, is also higher cause internally tech cannot improve too much. Eg DDR4 3200 has CL 16 what is 10 ns while DDR5 4800 is 34 what is 14 ns. There are more expensive CL 30 DIMMs. So, no big differences but compensated with longer bursts and higher transfer speeds.

At the end DDR5 is bit faster but is also way more expensive.
~ $
```

Reading the first line before running `sed` on the file\:

```bash
~ $ head -1 ddr4_vs_5
DDR5 is improvement to existing DDR4 and is similar to LPDDR4.
~ $
```

Running the command prints the following\:

```bash
~ $ sed 's/DDR/DNS/g' ddr4_vs_5
DNS5 is improvement to existing DNS4 and is similar to LPDNS4.
~ $
```

However, examining the first line printed above reveals that no changes have been written to the file itself.

```bash
~ $ head -1 ddr4_vs_5
DDR5 is improvement to existing DDR4 and is similar to LPDDR4.
~ $
```

The changes are written to the file, if one specifies option `-i`, in the `sed` command.

```bash
~ $ sed -i 's/DDR/DNS/g' ddr4_vs_5 && head -1 ddr4_vs_5
DNS5 is improvement to existing DNS4 and is similar to LPDNS4.
~ $
```

Deleting character\(s) is done by not giving it a replacement.

```bash
~ $ sed 's/improvement//g' ddr4_vs_5 | head -1
DNS5 is  to existing DNS4 and is similar to LPDNS4.
```

Notice the two white spaces between 'is' and 'to'. In order to only have one afterwards, one can do it like so\:

```bash
~ $ sed 's/improvement //g' ddr4_vs_5 | head -1
DNS5 is to existing DNS4 and is similar to LPDNS4.
~ $
```

To delete every line, where a pattern is matched on, the user can use\:

```bash
~ $ sed '/DDR/d' ddr4_vs_5





~ $
```

It left an empty file after running the above command. There was an occurrence of `DDR` on every line and every line was deleted.

{>>Start where the deleting empty lines happens in the video.<<}