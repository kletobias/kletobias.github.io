# Formatting Guide
## Header Structure
```md
---
title: 'Multicollinearity<br> What It Is & Measures To Spot It'
subtitle: 'Covariance And The Pearson Correlation Coefficient'
date: 2022-05-06 06:00:00
description: 'Covariance and the Pearson Correlation Coefficient: How to Spot Multicollinearity between random variables.'
accent_color: '#08877d'
featured_image:
 - '/images/negative-space-aerial-pacific-ocean.jpeg'
---
```

- Summary goes above the title tag (#) and has h3 level ### Summary...
- href text inside [ ] should all be uppercase
- <br> tag at the end of every paragraph.
- Text hard wrapped at 80 cols, not breaking any line of text.
- In addition to <br> at the end of each paragraph, there should be a <br> tag between <href> and description and tags and next <href>.
- **Tags:**, **Description:** should have uppercase first character.
- **Description:**  and **Tags:** have colon inside bold flags and one space before their values.
- Tags are lowercase.
- Tags have `tag`, if and only if it is referring to an actual command in Python.
- Tags for concepts only use lowercase characters.
- There should be a comma between each tag
- There should be a comma in the href text inside [ ] where needed.
- No period inside [ ]
- Colon where needed inside [ ]
- DataFrame columns have single single quotes around them. No ` ` or " ".
- In general stick to single quotes where possible.

## Steps To Do Before Every Post Is Pushed

Always check for any `TODO\:` and `ERROR:` tags inside an article.<br>
<br>
Always check for any `# fmt: off` and `# fmt: on` lines and delete them before
pushing!<br>
<br>
