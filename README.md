name: Cobrinha das contribuicoes

on:
  schedule:
    - cron: "0 */12 * * *"
  workflow_dispatch:

permissions:
  contents: write

jobs:
  gerar:
    runs-on: ubuntu-latest
    steps:
      - uses: Platane/snk@v3
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: |
            dist/github-contribution-grid-snake.svg?color_snake=#FF6FB5&color_dots=#FFE3F1,#FFB8DC,#FF8CC6,#FF6FB5,#D63F8C
            dist/github-contribution-grid-snake-dark.svg?palette=github-dark&color_snake=#FF6FB5&color_dots=#161b22,#5C2A4A,#8E3A6E,#C74E95,#FF6FB5
      - uses: crazy-max/ghaction-github-pages@v4
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
