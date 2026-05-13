# PPTX2MD (Personal Fork)

A tool to convert PowerPoint pptx files into markdown.

> **Note**: This is a personal fork of [pptx2md](https://github.com/ssine/pptx2md) as the original maintainers have abandoned the upstream repository.

## Improvements in This Fork

- Better error handling for shapes without embedded images
- Improved logging to distinguish between PIL and Wand conversions
- Fixed Windows path separators in markdown image links
- Enhanced URL encoding for image paths

## Installation

Do not install from PyPI (`pip install pptx2md`) - that is the original upstream version without these fixes.

**Requirements**: Python 3.10+

### Install from GitHub (this fork)

```sh
pip install git+https://github.com/alexander-goldstein/pptx2md.git
```

### Editable install for development

```sh
git clone https://github.com/alexander-goldstein/pptx2md.git
pip install -e pptx2md/
```

## Usage

```sh
pptx2md [pptx filename]
```

Default output is `out.md` with images in `/img/` folder.

**Note**: Only .pptx files are supported (not older .ppt format).

## Custom Titles

Use `-t titles.txt` to provide a hierarchical title structure. Indentation (spaces) determines heading levels. Fuzzy matching is used to match slide titles.

Example `titles.txt`:
```
Heading 1
  Heading 1.1
    Heading 1.1.1
  Heading 1.2
```

## Key Arguments 

- `-t [file]` - Custom title hierarchy file
- `-o [file]` - Output file path
- `-i [path]` - Image directory
- `--image-width [px]` - Max image width (uses HTML img tag)
- `--disable-notes` - Skip presenter notes
- `--enable-slides` - Add slide delimiters (`---`)
- `--wiki` / `--mdk` / `--qmd` - Output format (TiddlyWiki / Madoko / Quarto)
- `--page [n]` - Convert only specified page

**Note**: Install [wand](https://docs.wand-py.org/en/0.6.12/) for better WMF image conversion.


## API Usage

```python
from pptx2md import convert, ConversionConfig
from pathlib import Path

convert(
    ConversionConfig(
        pptx_path=Path('presentation.pptx'),
        output_path=Path('output.md'),
        image_dir=Path('img'),
        disable_notes=True
    )
)
```

---

**Original project**: [ssine/pptx2md](https://github.com/ssine/pptx2md)
