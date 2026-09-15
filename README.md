# bruceho293.github.io

Personal site for [Gia Huan (Bruce) Ho](https://www.linkedin.com/in/huangiaho), a software developer. Live at [bruceho293.github.io](https://bruceho293.github.io).

The blog covers experiments and notes from work and side projects. Current list contains the following from latest to oldest:
- Numbrace - A casual game with Flutter and Flame about number
- Java 25 - List Add operation comparison
- Hosting Static website from another repo with Git Submodules

The site is a [Jekyll](https://jekyllrb.com/) project on the [Chirpy](https://github.com/cotes2020/jekyll-theme-chirpy) theme. GitHub Actions builds it and deploys to GitHub Pages on push to `main`.

## Content

Posts live in `_posts/`. Site settings live in `_config.yml`. The About, Archives, Categories, and Tags pages live in `_tabs/`.

`assets/one-math-game` is a submodule of [one-math-game](https://github.com/bruceho293/one-math-game). After you change that repo, update the submodule here and push so GitHub Pages picks it up:

```shell
cd assets/one-math-game
git pull
cd ../..
git add assets/one-math-game
git commit -m "Update one-math-game"
```

Chirpy theme docs are in the [Chirpy wiki](https://github.com/cotes2020/jekyll-theme-chirpy/wiki).

## License

The theme and starter files are [MIT](LICENSE). Post content is mine.
