# Intro to Blackbox Fuzzing: Binary-only fuzzing of pdfinfo using AFLplusplus

- Author: Patrick Ventuzelo 
- Link: https://academy.fuzzinglabs.com/introduction-blackbox-fuzzing

## Install AFLplusplus

link: https://github.com/AFLplusplus/AFLplusplus

``` sh
# https://github.com/AFLplusplus/AFLplusplus#building-and-installing-afl
git clone --depth 1 https://github.com/AFLplusplus/AFLplusplus
cd AFLplusplus
make

# https://github.com/AFLplusplus/AFLplusplus#qemus
cd qemu_mode
./build_qemu_support.sh
```

More info about afl binary-only fuzzing: https://github.com/AFLplusplus/AFLplusplus#fuzzing-binary-only-targets

## Choose your target (pdfinfo)

Link: https://linux.die.net/man/1/pdfinfo

Test your target:
``` sh
pdfinfo corpus_pdf/160F-2019.pdf
```

Interesting options:
```
  -box                 : print the page bounding boxes
  -meta                : print the document metadata (XML)
  -js                  : print all JavaScript in the PDF
  -struct              : print the logical document structure (for tagged files)
  -struct-text         : print text contents along with document structure (for tagged files)
  -isodates            : print the dates in ISO-8601 format
  -rawdates            : print the undecoded date strings directly from the PDF file
  -dests               : print all named destinations in the PDF

```

## Prepare your fuzzing

``` sh
mkdir corpus_pdf
mkdir out
```

## Run the fuzzer

``` sh
./AFLplusplus/afl-fuzz -Q -D -i corpus_pdf -o out -- ./pdfinfo @@
```

## Improve your fuzzing

PDF format: https://en.wikipedia.org/wiki/PDF#File_format

Find interesting pdf inputs: https://github.com/mozilla/pdf.js/tree/master/test/pdfs

# Going deeper

Check my dedicated C/C++ WhiteBox Fuzzing training: https://academy.fuzzinglabs.com/c-whitebox-fuzzing?coupon=blog


# Stay tuned

- Twitter: https://twitter.com/pat_ventuzelo
- Telegram: https://t.me/fuzzinglabs
- Youtube: https://www.youtube.com/channel/UCGD1Qt2jgnFRjrfAITGdNfQ

Check my other tutorials and courses here: https://academy.fuzzinglabs.com/