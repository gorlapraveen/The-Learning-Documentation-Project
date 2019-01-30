Create `.gitlab-ci.yml` in your repository, with the following code.


```
compile_pdf:
  image: aergus/latex
  script:
    - latexmk -pdf main.tex
  artifacts:
    paths:
      - main.pdf
```

`main.tex` is a latex script and `main.pdf` is its generated `pdf` document file. Change `main` in the above code according to your wish.

Find the builds(`pdf's`) at [https://your-git-domain.com/<repo_name_space>/pipelines](#) i.e goto your project-repo pipelines.