+++
title = "EzProtocol"
date = 2019-08-09T14:11:14-07:00
draft = false

# Tags: can be used for filtering projects.
# Example: `tags = ["machine-learning", "deep-learning"]`
tags = []

# Project summary to display on homepage.
summary = ""

# Slides (optional).
#   Associate this page with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references 
#   `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides = ""

# Optional external URL for project (replaces project detail page).
external_link = ""

# Links (optional).
url_pdf = ""
url_code = ""
url_dataset = ""
url_slides = ""
url_video = ""
url_poster = ""

# Custom links (optional).
#   Uncomment line below to enable. For multiple links, use the form `[{...}, {...}, {...}]`.
# url_custom = [{icon_pack = "fab", icon="twitter", name="Follow", url = "https://twitter.com"}]

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
[image]
  # Caption (optional)
  caption = ""

  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = ""
+++

ezProtocol is a program designed for Opentrons OT2 robot. It handles writing detailed script for you so you can spend your time on things that matter. It can be found [here](https://github.com/SichongP/ezProtocol). 

ezProtocol can read protocol file in a format designed to be easy but versatile. 

See [here](https://github.com/ucdavis/VGL_OT-2/blob/protocolWriter/dev/protocolWriter/How_to_write_a_protocol.md) on how to make a protocol file.

## Requirements 
ezProtocol relies on below packages:
- PyYAML
- Pandas
- python-frontmatter
- regex
- opentrons

## Installation (pip deploy pending)
Clone this repo:
```
git clone https://github.com/SichongP/ezProtocol
```

Change directory:
```
cd ezProtocol
```
Install package:
```
pip install .
```
**Or**, use install.sh script:
```
bash install.sh
```
Test installation:
```
ezprotocol -h
```

## Getting started 
Once you have protocol and deck layout file ready (see [here](https://github.com/ucdavis/VGL_OT-2/blob/protocolWriter/dev/protocolWriter/How_to_write_a_protocol.md) for more detail on protocol and layout format), on commandline, type:
```
ezprotocol -p protocol.txt -d deck_layout.csv -o ot2_script.py
```
