# [Jekyll 기반 블로그](https://mmistakes.github.io/minimal-mistakes/)

[![LICENSE](https://img.shields.io/badge/license-MIT-lightgrey.svg)](https://raw.githubusercontent.com/mmistakes/minimal-mistakes/master/LICENSE)
[![Jekyll](https://img.shields.io/badge/jekyll-%3E%3D%203.7-blue.svg)](https://jekyllrb.com/)

Minimal Mistakes는 개인 사이트, 블로그, 포트폴리오 제작에 적합한 유연한 2열 Jekyll 테마입니다. 이름에서 알 수 있듯이, 스타일링은 의도적으로 미니멀하게 설계되어 사용자가 직접 수정하고 맞춤 설정할 수 있습니다 :smile:.

:sparkles:새로운 소식을 확인하세요 [CHANGELOG](CHANGELOG.md).

**참고:** 테마는 [jekyll-include-cache](https://github.com/benbalter/jekyll-include-cache) 플러그인을 사용합니다. 이 플러그인은 `Gemfile`에 설치해야 하며, `_config.yml`의 `plugins` 배열에 포함되어야 합니다. 그렇지 않으면 빌드 시 `알 수 없는 태그 'include_cached'` 오류가 발생합니다.

[![Minimal Mistakes live preview][2]][1]

[1]: https://mmistakes.github.io/minimal-mistakes/
[2]: screenshot.png (live preview)

![layout examples](screenshot-layouts.png)

## 주목할만한 특징

- 설치/업그레이드를 더욱 간편하게 하기 위해 "테마 젬"으로 번들로 제공됩니다.
- GitHub Pages와 호환됩니다.
- Jekyll 내장 Sass/SCSS 전처리기를 지원합니다.
- 9가지 스킨(색상 변형)을 제공합니다.
- 다양한 반응형 레이아웃 옵션(단일, 아카이브 인덱스, 검색, 스플래시, 페이지 매김 홈페이지)을 제공합니다.
- [Twitter Cards](https://dev.twitter.com/cards/overview) 및 [Open Graph](http://ogp.me/) 데이터를 지원하여 검색 엔진에 최적화되었습니다.
- 선택 사항 [헤더 이미지](https://mmistakes.github.io/minimal-mistakes/docs/layouts/#headers), [사용자 정의 사이드바](https://mmistakes.github.io/minimal-mistakes/docs/layouts/#sidebars), [목차](https://mmistakes.github.io/minimal-mistakes/docs/helpers/#table-of-contents), [갤러리](https://mmistakes.github.io/minimal-mistakes/docs/helpers/#gallery), 관련 게시물, [브레드크럼 링크](https://mmistakes.github.io/minimal-mistakes/docs/configuration/#breadcrumb-navigation-beta), [탐색 목록](https://mmistakes.github.io/minimal-mistakes/docs/helpers/#navigation-list) 등 다양한 기능을 제공합니다.
- 댓글 지원([Disqus](https://disqus.com/), [Facebook](https://developers.facebook.com/docs/plugins/comments), Google+, [Discourse](https://www.discourse.org/), [Staticman](https://staticman.net/), [utterances](https://utteranc.es/), [giscus](https://giscus.app/)를 통한 정적 기반).
- [Google 애널리틱스](https://www.google.com/analytics/) 지원
- UI 현지화된 텍스트는 영어(기본값), 아랍어(عربي), 브라질 포르투갈어(Português brasileiro), 불가리아어, 카탈로니아어, 중국어, 체코어, 덴마크어, 네덜란드어, 핀란드어, 프랑스어(Français), 독일어(Deutsch), 그리스어, 히브리어, 힌디어(हिंदी), 헝가리어, 인도네시아어, 아일랜드어(Gaeilge), 이탈리아어(Italiano), 일본어, 스와힐리어, 한국어, 말라얄람어, 미얀마어(Burmese), 네팔어(Nepalese), 노르웨이어(Norsk), 페르시아어(فارسی), 폴란드어, 펀자브어(ਪੰਜਾਬੀ), 루마니아어, 러시아어, 슬로바키아어, 스페인어(Español), 스웨덴어, 태국어, 터키어(Türkçe), 우크라이나어(Українська), 베트남어입니다.

## Skins (color variations)

이 테마는 기본 스킨 외에도 9가지의 다양한 스킨으로 제공됩니다.

| `air` | `contrast` | `dark` |
| --- | --- | --- |
| [![air skin](https://mmistakes.github.io/minimal-mistakes/assets/images/air-skin-archive.png)](https://mmistakes.github.io/minimal-mistakes/assets/images/air-skin-archive-large.png) | [![contrast skin](https://mmistakes.github.io/minimal-mistakes/assets/images/contrast-skin-archive.png)](https://mmistakes.github.io/minimal-mistakes/assets/images/contrast-skin-archive-large.png) | [![dark skin](https://mmistakes.github.io/minimal-mistakes/assets/images/dark-skin-archive.png)](https://mmistakes.github.io/minimal-mistakes/assets/images/dark-skin-archive-large.png) |

| `dirt` | `mint` | `sunrise` |
| --- | --- | --- |
| [![dirt skin](https://mmistakes.github.io/minimal-mistakes/assets/images/dirt-skin-archive.png)](https://mmistakes.github.io/minimal-mistakes/assets/images/dirt-skin-archive-large.png) | [![mint skin](https://mmistakes.github.io/minimal-mistakes/assets/images/mint-skin-archive.png)](https://mmistakes.github.io/minimal-mistakes/assets/images/mint-skin-archive-large.png) | [![sunrise skin](https://mmistakes.github.io/minimal-mistakes/assets/images/sunrise-skin-archive.png)](https://mmistakes.github.io/minimal-mistakes/assets/images/sunrise-skin-archive-large.png) |

| `aqua` | `neon` | `plum` |
| --- | --- | --- |
| [![aqua skin](https://mmistakes.github.io/minimal-mistakes/assets/images/aqua-skin-archive.png)](https://mmistakes.github.io/minimal-mistakes/assets/images/aqua-skin-archive-large.png) | [![neon skin](https://mmistakes.github.io/minimal-mistakes/assets/images/neon-skin-archive.png)](https://mmistakes.github.io/minimal-mistakes/assets/images/neon-skin-archive-large.png) | [![plum skin](https://mmistakes.github.io/minimal-mistakes/assets/images/plum-skin-archive.png)](https://mmistakes.github.io/minimal-mistakes/assets/images/plum-skin-archive-large.png) |

## Demo pages

| 이름                                        | 설명                                           |
| ------------------------------------------- | ----------------------------------------------------- |
| [헤더 이미지가 있는 게시물][header-image-post] | 큰 헤더 이미지가 있는 게시물입니다. |
| [HTML 태그 및 서식 게시물][html-tags-post] | 테마에서 스타일을 지정하는 다양한 일반적인 마크업입니다. |
| [구문 강조 게시물][syntax-post] | 강조 표시된 코드를 표시하는 게시물입니다. |
| [갤러리가 있는 게시물][gallery-post] | `<figure>` 요소로 둘러싸인 여러 이미지를 보여주는 게시물입니다. |
| [샘플 컬렉션 페이지][sample-collection] | 컬렉션의 단일 페이지입니다. |
| [카테고리 아카이브][categories-archive] | 카테고리별로 그룹화된 게시물입니다. |
| [태그 아카이브][tags-archive] | 태그별로 그룹화된 게시물입니다. |

추가 샘플 게시물은 데모 사이트의 [게시물 보관소][연도 보관소]에서 확인할 수 있습니다. 이 게시물(및 전체 데모 사이트)의 소스 파일은 [`/docs`](docs)에서 확인할 수 있습니다.

[헤더-이미지-게시물]: https://mmistakes.github.io/minimal-mistakes/layout-header-image-text-readability/
[갤러리-게시물]: https://mmistakes.github.io/minimal-mistakes/post%20formats/post-gallery/
[html-태그-게시물]: https://mmistakes.github.io/minimal-mistakes/markup/markup-html-tags-and-formatting/
[구문-게시물]: https://mmistakes.github.io/minimal-mistakes/markup-syntax-highlighting/
[샘플-컬렉션]: https://mmistakes.github.io/minimal-mistakes/recipes/chocolate-chip-cookies/
[카테고리-아카이브]: https://mmistakes.github.io/minimal-mistakes/categories/
[태그 아카이브]: https://mmistakes.github.io/minimal-mistakes/tags/
[년도 아카이브]: https://mmistakes.github.io/minimal-mistakes/year-archive/

## 설치

설치 방법은 세 가지가 있습니다. [젬 기반 테마](https://jekyllrb.com/docs/themes/#understanding-gem-based-themes), [원격 테마](https://blog.github.com/2017-11-29-use-any-theme-with-github-pages/)(GitHub Pages 호환), 또는 모든 테마 파일을 프로젝트에 포크하거나 직접 복사하는 것입니다.

### Gem 기반 방식

Gem 기반 테마를 사용하면 `assets`, `_layouts`, `_includes`, `_sass`와 같은 디렉터리가 테마의 gem에 저장되어 사용자에게는 보이지 않습니다. 하지만 필요한 모든 디렉터리는 Jekyll 빌드 과정에서 읽고 처리됩니다.

이렇게 하면 테마 파일을 관리할 필요가 없으므로 설치 및 업데이트가 더 쉬워집니다. 설치 방법:

1. `Gemfile`에 다음을 추가합니다.

```ruby
gem "minimal-mistakes-jekyll"
```

2. 다음 [Bundler](http://bundler.io/) 명령을 실행하여 번들된 gem을 가져오고 업데이트합니다.

```bash
bundle
```

3. 프로젝트의 Jekyll `_config.yml` 파일에 `theme`을 설정합니다.

```yaml
theme: minimal-mistakes-jekyll
```

테마를 업데이트하려면 `bundle update`를 실행합니다.

### 원격 테마 메서드

원격 테마는 Gem 기반 테마와 유사하지만 `Gemfile`을 변경하거나 허용 목록에 추가할 필요가 없으므로 GitHub Pages로 호스팅되는 사이트에 적합합니다.

설치 방법:

1. `Gemfile`의 내용을 다음과 같이 생성하거나 바꿉니다.

```ruby
source "https://rubygems.org"

gem "github-pages", group: :jekyll_plugins
gem "jekyll-include-cache", group: :jekyll_plugins
```

2. `_config.yml`의 `plugins` 배열에 `jekyll-include-cache`를 추가합니다.

3. 다음 [Bundler](https://bundler.io/) 명령을 실행하여 번들된 gem을 가져오고 업데이트합니다.

```bash
bundle
```

4. `_config.yml` 파일에 `remote_theme: "mmistakes/minimal-mistakes@4.27.1"`을 추가합니다. 다른 `theme:` 또는 `remote_theme:` 항목을 제거합니다.

<!--
개발자 참고: 버전 번호는 현재 다음 파일에 하드코딩되어 있습니다.

- package.json
- README.md (이 파일)
- docs/_data/theme.yml
- docs/_pages/home.md (Front Matter "발췌")

`package.json`은 신뢰할 수 있는 버전 번호를 저장하며, 다른 버전 번호는 `bundle exec rake version` 명령어를 사용하여 업데이트할 수 있습니다.

다음 파일도 다시 생성해야 합니다.

- _includes/copyright.html, _includes/copyright.js, _sass/minimal-mistakes/_copyright.scss
(`bundle exec rake clean`을 실행한 후 `bundle exec rake copyright`을 실행 - 세 파일 모두 `package.json`을 참조합니다.)
- assets/js/main.min.js (`bundle exec rake js`를 실행하고 `_includes/copyright.js`를 참조합니다.)

*팁*: 기본 Rake 작업은 위의 모든 파일을 한 번에 업데이트합니다.

또한, 라이선스 연도는 다음 파일에 하드코딩되어 있으며 Rake 작업에는 포함되지 않습니다.

- README.md (이 파일, 마지막 부분)
- LICENSE
-->

**예제를 찾고 계신가요?** GitHub Pages 호스팅 사이트를 구축하고 실행하는 가장 빠른 방법은 [Minimal Mistakes 원격 테마 스타터](https://github.com/mmistakes/mm-github-pages-starter/generate)를 사용하는 것입니다. 스타터에서 새 저장소를 생성하고, 샘플 콘텐츠를 직접 작성한 콘텐츠로 대체한 후 필요에 따라 구성합니다.

## 사용법

구성, 사용자 지정, 콘텐츠 추가/마이그레이션 등에 대한 자세한 내용은 [테마 설명서](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/)를 참조하세요.

## 기여

문서에서 오타를 발견하셨거나 [버그 수정](https://github.com/mmistakes/minimal-mistakes/issues)에 관심이 있으신가요? 그렇다면 [이슈 제출](https://github.com/mmistakes/minimal-mistakes/issues/new) 또는 [풀 리퀘스트](https://help.github.com/articles/using-pull-requests/)를 해주세요. 풀 리퀘스트를 처음 하시는 경우, [GitHub Flow](https://guides.github.com/introduction/flow/)를 먼저 읽어보시는 것이 도움이 될 수 있습니다.

테마 사용에 대한 도움이나 일반적인 Jekyll 지원 관련 질문은 [Jekyll Talk 포럼](https://talk.jekyllrb.com/)을 이용해 주세요.

### 풀 리퀘스트

풀 리퀘스트를 제출할 때는 다음을 수행하세요.

1. 저장소를 복제합니다.
2. `master`에서 브랜치를 생성하고 의미 있는 이름(예: `my-awesome-new-feature`)을 지정합니다.
3. GitHub에서 풀 리퀘스트를 열고 기능이나 수정 사항을 설명합니다.

개선 사항, 오타 수정 등을 제출하는 경우 테마 문서와 데모 페이지는 [`/docs`](docs)에서 확인할 수 있습니다.

## 개발

이 테마를 개발할 환경을 설정하려면 `bundle install`을 실행하세요.

테마를 테스트하려면 `bundle exec rake preview`를 실행하고 브라우저에서 `http://localhost:4000/test/`를 엽니다. 이렇게 하면 `test/` 디렉터리의 콘텐츠를 사용하는 Jekyll 서버가 시작됩니다. 테마와 테스트 사이트가 수정되면 서버가 다시 생성되고, 새로 고침 후 브라우저에서 변경 사항을 확인할 수 있습니다.

## 크레딧

### 제작자

**Michael Rose**

- <https://mademistakes.com>
- <https://twitter.com/mmistakes>
- <https://github.com/mmistakes>

### Icons + Demo Images:

- [The Noun Project](https://thenounproject.com) - Garrett Knoll, Arthur Shlain, and [tracy tam](https://thenounproject.com/tracytam)
- [Font Awesome](http://fontawesome.io/)
- [Unsplash](https://unsplash.com/)

### Other:

- [Jekyll](http://jekyllrb.com/)
- [jQuery](http://jquery.com/)
- [Susy](http://susy.oddbird.net/)
- [Breakpoint](http://breakpoint-sass.com/)
- [Magnific Popup](http://dimsemenov.com/plugins/magnific-popup/)
- [FitVids.JS](http://fitvidsjs.com/)
- [GreedyNav.js](https://github.com/lukejacksonn/GreedyNav)
- [Smooth Scroll](https://github.com/cferdinandi/smooth-scroll)
- [Gumshoe](https://github.com/cferdinandi/gumshoe)
- [jQuery throttle / debounce](http://benalman.com/projects/jquery-throttle-debounce-plugin/)
- [Lunr](http://lunrjs.com)
- [Clipboard.js](https://clipboardjs.com)

## License

MIT 라이선스(MIT)

저작권(c) 2013-2024 Michael Rose 및 기여자

본 소프트웨어 및 관련 문서 파일(이하 "소프트웨어")의 사본을 취득한 모든 사람에게 소프트웨어를 제한 없이 사용할 수 있는 권한을 무상으로 부여합니다. 여기에는 소프트웨어 사본을 사용, 복사, 수정, 병합, 게시, 배포, 재라이선스 부여 및/또는 판매할 권리와 소프트웨어가 제공된 사람에게 이러한 권한을 부여할 권리가 포함되나 이에 국한되지 않습니다. 단, 다음 조건에 따라야 합니다.

상기 저작권 고지 및 본 허가 고지는 소프트웨어의 모든 사본 또는 상당 부분에 포함되어야 합니다.

본 소프트웨어는 상품성, 특정 목적에의 적합성 및 비침해에 대한 보증을 포함하되 이에 국한되지 않는 명시적 또는 묵시적인 어떠한 종류의 보증 없이 "있는 그대로" 제공됩니다. 어떠한 경우에도 저작자 또는 저작권자는 계약, 불법 행위 또는 기타 행위에 따른 소송을 포함하여 본 소프트웨어 또는 본 소프트웨어의 사용 또는 기타 거래와 관련하여 발생하는 모든 청구, 손해 또는 기타 책임에 대해 책임을 지지 않습니다.


Minimal Mistakes incorporates icons from [The Noun Project](https://thenounproject.com/) 
creators Garrett Knoll, Arthur Shlain, and tracy tam.
Icons are distributed under Creative Commons Attribution 3.0 United States (CC BY 3.0 US).

Minimal Mistakes incorporates [Font Awesome](http://fontawesome.io/),
Copyright (c) 2017 Dave Gandy.
Font Awesome is distributed under the terms of the [SIL OFL 1.1](http://scripts.sil.org/OFL) 
and [MIT License](http://opensource.org/licenses/MIT).

Minimal Mistakes incorporates photographs from [Unsplash](https://unsplash.com).

Minimal Mistakes incorporates [Susy](http://susy.oddbird.net/),
Copyright (c) 2017, Miriam Eric Suzanne.
Susy is distributed under the terms of the [BSD 3-clause "New" or "Revised" License](https://opensource.org/licenses/BSD-3-Clause).

Minimal Mistakes incorporates [Breakpoint](http://breakpoint-sass.com/).
Breakpoint is distributed under the terms of the [MIT/GPL Licenses](http://opensource.org/licenses/MIT).

Minimal Mistakes incorporates [FitVids.js](https://github.com/davatron5000/FitVids.js/),
Copyright (c) 2013 Dave Rubert and Chris Coyier.
FitVids is distributed under the terms of the [WTFPL License](http://www.wtfpl.net/).

Minimal Mistakes incorporates [Magnific Popup](http://dimsemenov.com/plugins/magnific-popup/),
Copyright (c) 2014-2016 Dmitry Semenov, http://dimsemenov.com.
Magnific Popup is distributed under the terms of the MIT License.

Minimal Mistakes incorporates [Smooth Scroll](http://github.com/cferdinandi/smooth-scroll),
Copyright (c) 2019 Chris Ferdinandi.
Smooth Scroll is distributed under the terms of the [MIT License](http://opensource.org/licenses/MIT).

Minimal Mistakes incorporates [Gumshoejs](http://github.com/cferdinandi/gumshoe),
Copyright (c) 2019 Chris Ferdinandi.
Gumshoejs is distributed under the terms of the [MIT License](http://opensource.org/licenses/MIT).

Minimal Mistakes incorporates [jQuery throttle / debounce](http://benalman.com/projects/jquery-throttle-debounce-plugin/),
Copyright (c) 2010 "Cowboy" Ben Alman.
jQuery throttle / debounce is distributed under the terms of the [MIT License](http://opensource.org/licenses/MIT).

Minimal Mistakes incorporates [GreedyNav.js](https://github.com/lukejacksonn/GreedyNav),
Copyright (c) 2015 Luke Jackson.
GreedyNav.js is distributed under the terms of the [MIT License](http://opensource.org/licenses/MIT).

Minimal Mistakes incorporates [Jekyll Group-By-Array](https://github.com/mushishi78/jekyll-group-by-array),
Copyright (c) 2015 Max White <mushishi78@gmail.com>.
Jekyll Group-By-Array is distributed under the terms of the [MIT License](http://opensource.org/licenses/MIT).

Minimal Mistakes incorporates [@allejo's Pure Liquid Jekyll Table of Contents](https://allejo.io/blog/a-jekyll-toc-in-liquid-only/),
Copyright (c) 2017 Vladimir Jimenez.
Pure Liquid Jekyll Table of Contents is distributed under the terms of the [MIT License](http://opensource.org/licenses/MIT).

Minimal Mistakes incorporates [Lunr](http://lunrjs.com),
Copyright (c) 2018 Oliver Nightingale.
Lunr is distributed under the terms of the [MIT License](http://opensource.org/licenses/MIT).

Minimal Mistakes incorporates [clipboard.js](https://clipboardjs.com/),
Copyright (c) 2021 Zeno Rocha.
Clipboard.js is distributed under the terms of the [MIT License](https://opensource.org/licenses/MIT).
