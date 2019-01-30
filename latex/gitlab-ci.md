```compile_pdf:
  image: aergus/latex
  script:
    - latexmk -pdf main.tex
  artifacts:
    paths:
      - main.pdf
```