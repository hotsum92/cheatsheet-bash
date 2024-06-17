# google-chrome headless

## version

```
google-chrome --version
```

## dump-dom

```
google-chrome --headless --print-to-pdf='file.pdf' --dump-dom https://google.com/
```

--virtual-time-budget=10000
--run-all-compositor-stages-before-draw

pup '#home-outer > div:nth-child(7) > ul > li:nth-child(8) > a attr{href}'
pup '#home-outer > div:nth-child(7) > ul > li:nth-child(8) > a text{}'
pup '#home-outer > div:nth-child(7) > ul > li:nth-child(8) > a json{}'

