# .github/workflows/latex-build.yml
name: 📚 LaTeX PDF Builder

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  build-pdf:
    runs-on: ubuntu-latest

    steps:
    - name: 📥 Checkout repository
      uses: actions/checkout@v3

    - name: 🧰 Install LaTeX packages
      run: |
        sudo apt-get update
        sudo apt-get install -y texlive-full

    - name: 🏗 Compile LaTeX to PDF
      run: |
        mkdir -p output
        pdflatex -output-directory=output main.tex

    - name: 📤 Upload PDF artifact
      uses: actions/upload-artifact@v3
      with:
        name: compiled-pdf
        path: output/main.pd
