---
banner: "[[banner-2.jpg]]"
date: 2025-08-24
title: "[블로그 개선] Hugo 블로그를 만들어보았습니다"
tags:
  - blog
  - hugo
banner_y: 0.702
featuredImage: "image.png"
featuredImagePreview: "image.png"
---
2025학년도 1학기를 보내면서 글을 쓸 기회가 많이 없어졌었다. 사실 자잘하게 글을 쓰고 문서를 하는 일은 많이 했으나, 실제로 `완벽한 블로그 글을 작성해야한다.` 라는 머릿속의 집착 때문에 글을 쓰는 것이 두려워 진것도 사실이다...

더군다나 불편한 점도 많이 느끼고 있었는데, 이에 블로그 작성 방법을 개선해서 프로젝트(끝이 나는 작업)이 끝나게 되면 자연스럽게 블로그 글도 쓸 수 있도록 환경을 조성하려고 하였고, 그러다보니 블로그 구조를 개선하게 되었다.

## 블로그 개선 이유

### 1. 블로그 빌드 속도 개선

`Ruby` 언어로 만들어진 지킬은 `Go` 언어로 만들어졌는데, 그러다보니 `Ruby` 를 위한 의존성 설치와 세팅 시간이 많이 잡아먹게 되었고, 최종적으로 빌드 시 1분이 걸리는 불상사가 일어난다.

그래서 문제를 해결하기 위해 [검색하던 중](https://stackoverflow.com/questions/26855552/jekyll-compiling-seems-way-too-slow), 검색 결과 `node_modules` 의 문제가 있었음을 알아냈다.

실제로 내 블로그 `github workflow` 로그를 확인하면, 루비 세팅 시간이 많이 걸리는 것을 확인할 수 있다. 

![](<새로운 블로그 리뉴얼을 환영해주세요!-1756027776764.webp>)

문제는 이 결과가 사실은 루비 빌드 시 `node_modules` 를 포함한 여러 디렉토리를 제외한 값이라는 것이다…

실제로 `로컬환경`에서 루비를 세팅하고 버전 관리하는 것부터 너무나도 복잡했다.

![](<새로운 블로그 리뉴얼을 환영해주세요!-1756027851593.webp>)

게다가 내 블로그 프로젝트에는 빌드 시 `exclude` 할 폴더에 노드 모듈이 포함되어 있다.

그래서 `Go` 에 관심이 많기도 했고, 후술할 이유로 조금 더 개선을 위해 다른 테마를 찾으려고 했다.
### 2. 블로그 디자인 단순화

이유라기 보다는 변경점에 가깝다.

사실 양쪽에 프로필 / ToC / 최근 업데이트 문서 등 불필요한 정보가 너무나도 많다고 생각이 들었다.

이번에 블로그를 개선하면서 오로지 문서에 집중해보고 싶었다. 그리고 배경은 이쁘다고 생각해서 넣었는데 오히려 불호에 가까운 피드백을 받았다.. 계속 보니 가독성 자체에는 좋지 않다고 보이더라.

이전 블로그의 디자인을 그대로 가져오기 위해 시간 투자를 하기에는 아깝다고 생각이 들어 어쩔 수 없지만 간단하게 디자인을 변경하였다.

![](<새로운 블로그 리뉴얼을 환영해주세요!-1756026623283.webp>)

이전 디자인은 이랬는데, 조금 어두운 면도 있고, 글자 색상도 어두워서 가독성이 떨어진다고 생각하였고, 이런 부분을 개선했다. 특히, `가독성`에 집중하도록 노력했다.

다른 테마를 사용하면 어떨지 모르겠는데, 이미 `chirpy` 테마에 고착화되어서 새롭게 블로그를 리뉴얼 해보는 것도 나쁘지 않다고 판단했다.

또한, 가독성에 집중하기 위해 `word-break: keep-all;` 옵션을 넣어주었다.

띄어쓰기가 있는 한글 특성상 단어를 잘라서 줄바꿈을 하지 않고, 단어 단위로 줄바꿈을 해주는 `keep-all` 특성이 좋다고 판단하여 적용해보았다.

```css

.post-single p {
	word-break: keep-all;
}
```

### 3. 옵시디언 통합

이전까지는 옵시디언 볼트(프로젝트)를 블로그용, 나누고 있었다. 그렇기 때문에 더더욱 블로그 글을 안쓴 것도 있는 것 같았다.

`문서화` 와 `블로그 글 작성` 사이에서 조금 괴리감을 느끼고 있었고, 그래서 더더욱 블로그 글은 완벽하게 써야한다고 생각하게 돼서 잘 안쓰게 됐다.

더욱이나 접근성도 안좋아지니 블로그 작성 자체에 눈을 들이게 되는 일이 많이 줄었었다.

![](<새로운 블로그 리뉴얼을 환영해주세요!-1756026537606.webp>)

이는 실제로 `PARA` 노트 기법으로 작성중인 내 옵시디언 저장소다. 이 부분에 리소스(혹은 아카이브) 부분에 블로그 탭을 추가하여 버전관리를 하기로 했다.

그렇다면 이제 문제가 생긴다.

> 버전관리는 어떻게 할 것인가?

실제로 내 저장소 내에는 깃허브로 공유해서는 안되는 중요자료들이 많다.

이 부분에 있어서 고민이 많이 되었는데, 결국 블로그 .git 프로젝트 자체를 `icloud` 내에 전부 넣었다. (…)

icloud 자체가 기본이 5GB라서 프로젝트 하나를 넣어두기엔 충분하다고 생각하고, 최근에 볼트에서 `webp` 포맷으로 변경하여 이미지 크기를 최적화했기 때문에.. 상관없다고 판단했다.

```yaml
module:
  mounts:
    - source: content
      target: content

    - source: "../99. Images"
      target: "assets"

    - source: "../03. Resources/BlogPosts"
      target: "content/posts"
```

그리고 실제로 내가 쓰는 옵시디언 저장소에서는 `03. Resources` 폴더에 자주 보는 자료들은 이곳에 넣는다. 

블로그로 공개할 문서들은 `BlogPosts` 에 넣고 `CLI`에서 커밋을 날리면 자연스럽게 블로그 포스트도 가능하도록 만들어주었다!

## 옵시디언 이미지 문법 인식을 위한 hugo 플러그인 생성

이전에 chirpy 테마로 넘어오면서 대부분의 프론트매터는 수정해주었지만, 이번엔 그럴필요 없도록 했다.

**무언가 마이그레이션한다면 기존 리소스는 최대한 수정할 일이 없어야한다고 생각하기 때문에 최대한 노력해보았다.**

이번에도 그래서 최대한 프론트매터를 호환되게 만들었고, 특히 이미지처리할 때 별도의 플러그인을 휴고 문법에 맞게 만들었다. (이부분은 내가 문법을 몰라서 제미니한테 물어보면서 코드를 짰다.)

혹시 필요할 일이 있을까봐 코드를 공유한다.

이 코드는 `layouts/_default/_markup/render-image.html` 파일인데, assets 폴더에서 이미지 파일을 찾아오는 플러그인이다.

```html
{{- $alt := .Text -}}
{{- $destination := .Destination -}}
{{- $isExternal := strings.HasPrefix $destination "http" -}}

{{- if not $isExternal -}}
  {{/* target이 "assets"이므로 바로 파일명을 찾습니다. */}}
  {{- $image := resources.Get (strings.TrimPrefix "/" $destination) -}}

  {{- if $image -}}
    <img src="{{ $image.RelPermalink }}" alt="{{ $alt }}" loading="lazy">
  {{- else -}}
    <p style="color: red;">Asset not found: {{ $destination }}</p>
  {{- end -}}
{{- else -}}
  <img src="{{ $destination | safeURL }}" alt="{{ $alt }}" loading="lazy">
{{- end -}}
```

두번째로 `layouts/_default/single.html` 이다. 포스트 페이지를 구성하는 코드인데, `PaperMod` 라는 테마를 사용하면서 그대로 긁어와서 `Content` 부분만 수정해주었다.

`![[]]` 같은 위키링크 형태로 옵시디언에서는 이미지를 링킹을 하는데, 공식 마크다운 이미지 문법인 `![]()` 을 쓰지 않은 이유로는 이미 만들어진 문서들이 대부분 위키링크 형태이기 때문이다.

```html
{{- define "main" }}

<article class="post-single">
  <header class="post-header">
    {{ partial "breadcrumbs.html" . }}
    <h1 class="post-title entry-hint-parent">
      {{ .Title }}
      {{- if .Draft }}
      <span class="entry-hint" title="Draft">
        <svg xmlns="http://www.w3.org/2000/svg" height="35" viewBox="0 -960 960 960" fill="currentColor">
          <path
            d="M160-410v-60h300v60H160Zm0-165v-60h470v60H160Zm0-165v-60h470v60H160Zm360 580v-123l221-220q9-9 20-13t22-4q12 0 23 4.5t20 13.5l37 37q9 9 13 20t4 22q0 11-4.5 22.5T862.09-380L643-160H520Zm300-263-37-37 37 37ZM580-220h38l121-122-18-19-19-18-122 121v38Zm141-141-19-18 37 37-18-19Z" />
        </svg>
      </span>
      {{- end }}
    </h1>
    {{- if .Description }}
    <div class="post-description">
      {{ .Description }}
    </div>
    {{- end }}
    {{- if not (.Param "hideMeta") }}
    <div class="post-meta">
      {{- partial "post_meta.html" . -}}
      {{- partial "translation_list.html" . -}}
      {{- partial "edit_post.html" . -}}
      {{- partial "post_canonical.html" . -}}
    </div>
    {{- end }}
  </header>
  {{- $isHidden := (.Param "cover.hiddenInSingle") | default (.Param "cover.hidden") | default false }}
  {{- partial "cover.html" (dict "cxt" . "IsSingle" true "isHidden" $isHidden) }}
  {{- if (.Param "ShowToc") }}
  {{- partial "toc.html" . }}
  {{- end }}

  {{- if .Content }}
    {{- $content := .RawContent -}}
    {{- $find := "!\\[\\[(.*?)\\]\\]" -}}
    {{- $matches := findRE $find $content -}}

    {{- range $matches -}}
      {{- $originalMatch := . -}}
      {{- $pathAndWidth := replaceRE $find "$1" $originalMatch -}}
      {{- $path := $pathAndWidth -}}
      {{- $width := "" -}}
      {{- if strings.Contains $pathAndWidth "|" -}}
        {{- $parts := split $pathAndWidth "|" -}}
        {{- $path = index $parts 0 -}}
        {{- $width = index $parts 1 -}}
      {{- end -}}
      
      {{- $image := resources.Get $path -}}
      {{- if $image -}}
        {{- $imgTag := printf "<img src=\"%s\" alt=\"%s\" loading=\"lazy\"" $image.RelPermalink (strings.TrimSuffix ".webp" (strings.TrimSuffix ".png" (strings.TrimSuffix ".jpg" $path))) -}}
        {{- if $width -}}
          {{- $imgTag = printf "%s style=\"width: %spx;\">" $imgTag $width -}}
        {{- else -}}
          {{- $imgTag = printf "%s>" $imgTag -}}
        {{- end -}}
        {{- $content = replace $content $originalMatch $imgTag -}}
      {{- end -}}
    {{- end -}}

    {{- $finalContent := $content | .RenderString -}}

    <div class="post-content">
      {{- if not (.Param "disableAnchoredHeadings") }}
        {{- partial "anchored_headings.html" $finalContent -}}
      {{- else }}
        {{- $finalContent | safeHTML -}}
      {{- end }}
    </div>
  {{- end }}

  <footer class="post-footer">
    {{- $tags := .Language.Params.Taxonomies.tag | default "tags" }}
    <ul class="post-tags">
      {{- range ($.GetTerms $tags) }}
      <li><a href="{{ .Permalink }}">{{ .LinkTitle }}</a></li>
      {{- end }}
    </ul>
    {{- if (.Param "ShowPostNavLinks") }}
    {{- partial "post_nav_links.html" . }}
    {{- end }}
    {{- if (and site.Params.ShowShareButtons (ne .Params.disableShare true)) }}
    {{- partial "share_icons.html" . -}}
    {{- end }}
  </footer>

  {{- if (.Param "comments") }}
  {{- partial "comments.html" . }}
  {{- end }}
</article>

{{- end }}{{/* end main */}}
```

크게 건드렸던 건 이렇게 두개였던 것 같고, 한 4시간 정도 걸렸던 것 같다.

## 배포과정 중 생긴 문제해결 과정

그리고 배포를 할 것인데, 그냥 끼얹기보단 새롭게 orphan branch를 만들어서 이 브랜치를 `main` 브랜치로 바꾸어서 기존 플젝에 업데이트 해보았다.

우선 공식 `hugo` 사이트에서 아래 배포 스크립트를 그대로 적용해보았다. `TZ`만 우리나라 서울로 바꾸어주었고, 그대로 옮겨보았다.

```yaml
name: Build and deploy
on:
  push:
    branches:
      - main
  workflow_dispatch:
permissions:
  contents: read
  pages: write
  id-token: write
concurrency:
  group: pages
  cancel-in-progress: false
defaults:
  run:
    shell: bash
jobs:
  build:
    runs-on: ubuntu-latest
    env:
      DART_SASS_VERSION: 1.90.0
      GO_VERSION: 1.24.5
      HUGO_VERSION: 0.148.2
      NODE_VERSION: 22.18.0
      TZ: Europe/Oslo
    steps:
      - name: Checkout
        uses: actions/checkout@v5
        with:
          submodules: recursive
          fetch-depth: 0
      - name: Setup Go
        uses: actions/setup-go@v5
        with:
          go-version: ${{ env.GO_VERSION }}
          cache: false
      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: ${{ env.NODE_VERSION }}
      - name: Setup Pages
        id: pages
        uses: actions/configure-pages@v5
      - name: Create directory for user-specific executable files
        run: |
          mkdir -p "${HOME}/.local"
      - name: Install Dart Sass
        run: |
          curl -sLJO "https://github.com/sass/dart-sass/releases/download/${DART_SASS_VERSION}/dart-sass-${DART_SASS_VERSION}-linux-x64.tar.gz"
          tar -C "${HOME}/.local" -xf "dart-sass-${DART_SASS_VERSION}-linux-x64.tar.gz"
          rm "dart-sass-${DART_SASS_VERSION}-linux-x64.tar.gz"
          echo "${HOME}/.local/dart-sass" >> "${GITHUB_PATH}"
      - name: Install Hugo
        run: |
          curl -sLJO "https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_linux-amd64.tar.gz"
          mkdir "${HOME}/.local/hugo"
          tar -C "${HOME}/.local/hugo" -xf "hugo_extended_${HUGO_VERSION}_linux-amd64.tar.gz"
          rm "hugo_extended_${HUGO_VERSION}_linux-amd64.tar.gz"
          echo "${HOME}/.local/hugo" >> "${GITHUB_PATH}"
      - name: Verify installations
        run: |
          echo "Dart Sass: $(sass --version)"
          echo "Go: $(go version)"
          echo "Hugo: $(hugo version)"
          echo "Node.js: $(node --version)"
      - name: Install Node.js dependencies
        run: |
          [[ -f package-lock.json || -f npm-shrinkwrap.json ]] && npm ci || true
      - name: Configure Git
        run: |
          git config core.quotepath false
      - name: Cache restore
        id: cache-restore
        uses: actions/cache/restore@v4
        with:
          path: ${{ runner.temp }}/hugo_cache
          key: hugo-${{ github.run_id }}
          restore-keys:
            hugo-
      - name: Build the site
        run: |
          hugo \
            --gc \
            --minify \
            --baseURL "${{ steps.pages.outputs.base_url }}/" \
            --cacheDir "${{ runner.temp }}/hugo_cache"
      - name: Cache save
        id: cache-save
        uses: actions/cache/save@v4
        with:
          path: ${{ runner.temp }}/hugo_cache
          key: ${{ steps.cache-restore.outputs.cache-primary-key }}
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./public
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```


![](<새로운 블로그 리뉴얼을 환영해주세요-1756097756323.webp>)

기존 방식보다 **무려 40초나 줄었고,** 엄청 빠르게 빌드되는 걸 확인할 수 있다.

이 빌드가 그냥 처음부터 `Go` 를 다 깔고 하는 걸 생각하면 엄청 빠르단걸 확인할 수 있다.

![](<새로운 블로그 리뉴얼을 환영해주세요-1756098002261.webp>)

이렇게 이제 블로그 배포가 잘 되는 걸 확인할 수 있다.

하지만 보는 것처럼 글이 하나도 없다. 이건 당연하다. 왜냐하면 위에서 봤던 것처럼 내 개인 옵시디언 볼트에서 끌어와서 빌드하는 방식이니, 볼트 자체를 깃허브에 업로드하는게 아니니까 그렇다.

여기서 내가 생각해본게 두가진데,,

1. symlink 같은걸 도입해서 내 볼트에 있는 블로그 포스트도 git이 인식해서 올려줄 수 있도록 하거나
2. 처음부터 블로그 포스트(`.md`) 들을 git에 업로드하도록 만들기

내가 옵시디언과의 연동성을 생각해볼때 2번은 절대 싫었다. 왜냐하면 내 옵시디언 저장소는 icloud에서 관리되기 때문이다.

결국엔 symlink 같은걸 도입하거나, 업로드 스크립트를 만들거나 해야할 것 같았다.

### 1. 배포를 위해서 심링크를 쓰기

우선, 진짜 symlink가 git에서 진짜 되는지 한번 해볼 필요가 있다. 당시에 `git` 이 심볼릭 링크를 어떻게 다루는지 몰라서 일단 직접 만들어보았다.

일단은 컨텐츠를 휴고에서 옮기는 `mount` 를 삭제하고 심링크를 추가해보았다.

심링크 추가까지는 너무 잘되었다. 휴고 블로그 서버도 잘 작동되었다. `vscode` 에서도 단순히 폴더로 인식됐다.

![](<새로운 블로그 리뉴얼을 환영해주세요-1756098346361.webp>)

하지만 깃에서 추가할 때는 문제가 되었는데, 그 이유는 깃에서는 [심링크 자체에서 링크 정보만을 커밋한다.](https://www.geeksforgeeks.org/git/how-does-git-handle-symbolic-links/)

그래서 깃허브에서는 "링크되는 정보" 자체만을 저장해서 버전 관리되기 때문에 하드 링크로 바꾸어보려고 했는데.. 이게 어쩌나, [디렉토리는 하드링크를 할 수 없다!](https://askubuntu.com/questions/210741/why-are-hard-links-not-allowed-for-directories) 왜냐하면 무한루프가 생길 수 있기 때문이다.
### 2. 셸 스크립트 사용

그래서 결국 스크립트를 사용해서 배포용 스크립트를 만들기로 했다. 구글링을 직접 하면서 어떤 방법이 있나 찾아보았다.

다행히, 옵시디언을 좋아하는 한 개발자분께서 `shell commands` 라는 옵시디언 플러그인을 만들어두셨다.

https://publish.obsidian.md/shellcommands/Index

옵시디언 볼트에서 직접 터미널을 통해 셸 스크립트를 실행할 수 있는 플러그인이다.

그래서 아래처럼 직접 내 블로그 포스트 디렉토리를 찾아 사이트를 **빌드해서 그냥 이대로 올렸다.**

어차피 로컬에서 올려야한다면, `github action` 을 통해서 빌드를 하고 올리는게 낫다고 생각했다.

### `rsync` 명령어

그런데, `mv` 를 통해 빌드 파일을 버전관리하는 디렉토리로 옮기던 중 애로 사항이 있었다.

```
mv: rename public/archives to public-git/archives: Directory not empty
mv: rename public/assets to public-git/assets: Directory not empty
mv: rename public/categories to public-git/categories: Directory not empty
mv: rename public/page to public-git/page: Directory not empty
mv: rename public/posts to public-git/posts: Directory not empty
mv: rename public/search to public-git/search: Directory not empty
mv: rename public/tags to public-git/tags: Directory not empty
To https://github.com/moozeh/blog-static.git
   e499e5e..5e605e7  main -> main
```

위처럼 `Directory not empty` 와 같은 문제가 있었다.

그래서 어차피 복사할 거 그냥 `rsync` 명령어를 사용했다.

`rsync` 같은 경우 대상을 완벽하게 동일하게 복사해주므로 딱 나에게 필요한 명령어였다.

이 명령어가 보통 백업할 때 쓰이는 듯하다. 실제로 나중에 백업 프로그램을 만들 일이 생긴다면 이 명령어를 참고해보는 것도 좋을 것 같다.

```sh
rsync -ah [SORCE_DIR] [TARGET_DIR]
```

위와 같이 사용하여 복사할 수 있다. 그밖의 옵션에 관해선 이렇다.

- `-a` 옵션 : 아카이브 모드. 권한, 시간, 심볼릭 링크 등 세세한 정보까지 복사해준다.
- `-v` 옵션 : verbose. 스크립트를 사용할 때 아는 그것. 디버깅에 용이하다.
- `-h` 옵션 : human readable. 복사할 때 출력시 결과를 `KB`, `MB` 등 사람이 보기 편하게 나타내게해준다.

나는 실제로 출력 결과를 통해 디버깅해야하는데, 셸 스크립트이기 때문에 -v 옵션은 필요 없어서 사용하진 않았다.

최종 결과는 이렇게 나왔다. 블로그를 전부 쓰고 `cmd + p` 를 눌러 스크립트를 실행해주면 된다.

이전과 달리 옵시디언 볼트는 하나만 사용하고, 버전 관리는 빌드 결과만 해주면 된다!!! 너무 좋다 ^^

```sh
#!/bin/bash
export PATH="$PATH:/opt/homebrew/bin";
echo "Building static site..."
cd blog
hugo build

if [ $? -ne 0 ]; then
  echo "Failed to build hugo project. Aborted."
  return -1
fi

echo "Uploading static website files to a github repository."

rsync -ah public/* public-git
cd public-git

git pull
git add .
git commit -m "Uploaded post via obsidian shell script"

if [ $? -ne 0 ]; then
  echo "failed to commit to a remote repository. Aborted."
  return -1
fi

git push

if [ $? -ne 0 ]; then
  git reset --hard HEAD~1
  echo "failed to push. soft reseting data."
  return -1
fi
```

### 3. Github Pages 고질적인 문제

이렇게 블로그를 개선하니 이게 웬걸, 이번엔 `Github Pages` 도 말썽이다 ㅠㅠ

![](<20250824 새로운 블로그 리뉴얼을 환영해주세요-1756382539402.webp>)

깃허브 페이지 빌드 및 배포 자체(내가 어찌할 수 있는게 없다..)에만 1분이 걸리더니 이내 계속 `Queued` 상태에서 먹통이 되었다.


![](<20250824 새로운 블로그 리뉴얼을 환영해주세요-1756382463604.webp>)

실제로 내가 댓글을 단 이후로 안되는 사람들이 많더라.

그래서 여러 방법들을 찾기 위해 구글링하다가 `Cloudflare Pages` 라는게 있다고 알게 되었다.

### Cloudflare Pages

보다시피 나는 도메인을 운영중이고, 이는 클라우드 플레어에서 관리한다. 그렇기 때문에, 클플 페이지를 사용하면 효율적이게 도메인 연결도 다 해줄 수 있게 된다.

![](<20250824 새로운 블로그 리뉴얼을 환영해주세요-1756382692924.webp>)

물론, 클플 페이지에서 깃 저장소와 연동을 지원해준다.

https://developers.cloudflare.com/pages/configuration/git-integration/

그래서 현재는 클플 페이지를 사용하고 있다. 배포 자체가 엄청 빠르고 만족 중이다!
## 앞으로의 방침

앞으로 블로그글을 쓸 때는 그냥 `타인에게 공유할 일이 잦을 문서`, `고민하는 과정을 쓰는 문서` 로 나누어서 쓸 것 같다.

문제해결을 좋아하는 친구와 얘기해봤는데, 뭔가 거창한 이력을 적는 것보다, 내가 하고 싶은 프로젝트에서 생긴 문제 해결 과정을 까먹지 않게만 기록해도 충분할 듯하다.

그리고, 그야 그도 그럴게, **문제 해결을 어떻게 한번에 하겠나?** 한번에 해결이 되면 나 혼자 이미 회사를 차렸지.. 계속 고민해서 끊임없이 완벽보단 완주를 노려봐야할 것 같다.

실제로 부스트캠프를 하면서도 내 고민과정을 제대로 기록하지 못한 것에 후회를 많이 했었는데 아직 좀 더 고쳐야할 것 같아서 내적으로 많이 고민이 되긴 한다.

내가 완벽하다고 생각하기 보단 계속 이렇게 달려야 좋은 사람이고 발전하는 사람이 아닐까 생각한다. 다시 한번 잘 노력해보자!