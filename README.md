# Knowla Buying Guide

A single-page tool that helps choose Knowla software packages ("planets") by selecting the skills or areas you want to develop. Pick one or more criteria, press **Filter**, and the matching packages are listed with their description, age range and net price.

## How it works

- `index.html` is the whole app: HTML, a little CSS and JavaScript.
- The product data lives in an Excel workbook embedded in the page as a base64 string (`base64ExcelData`). On load it is decoded and parsed in the browser with [SheetJS](https://sheetjs.com/).
- Each spreadsheet row is one package/criterion pair. The columns used are:

  | Column | Meaning |
  | --- | --- |
  | `Selection Criteria` | Criterion shown as a checkbox |
  | `Software` | Package name (rows with the same name are merged into one card) |
  | `Priority` | Sort order; lower numbers first (1, 2, 3 set the title size) |
  | `Details` | Short description |
  | `Age` | Recommended age range |
  | `Price` | Net price in euros |
  | `Full Text` | Long description |
  | `piclink` | Image URL |

- Results show packages matching **any** selected criterion, sorted by `Priority`; packages with equal priority keep their spreadsheet order.

## Running it

No build step. Open `index.html` in a browser, or serve the folder:

```sh
python3 -m http.server 8000
```

An internet connection is needed for the Bootstrap and SheetJS CDN scripts and the product images.

## Updating the data

Edit the workbook, convert it to base64 (for example `base64 -w0 data.xlsx`) and replace the value of `base64ExcelData` in `index.html`.

## Dependencies (loaded from CDNs)

- [Bootstrap 5.3](https://getbootstrap.com/)
- [SheetJS (xlsx) 0.17](https://sheetjs.com/)
