---
layout: post
title: 깃허브에 드디어 첫 사이트 오픈!!
---
깃을 설치하고 루비를 설치하고 로컬에서 jekyll을 실행시키는데 자꾸 에러가 나서 어찌할바를 몰랐는데, 그 해법을 오늘에서야 발견했다.
사이트 참조: https://docs.github.com/ko/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll
루비 프롬프트에서 bundle exec jekyll serve 을 실행하면 자꾸 에러가 났었는데, 그 이유가 ruby 3.0 이상을 설치한 경우에는 webrick이 설치되지 않아서 생기는 오류였던 것이다. webrick 실행을 시도하면 이 오류가 말끔히 해소된다. bundle add webrick 이후에 bundle exec jekyll serve를 실행하면 된다.

* 루비설치후 ruby 프로프트를 실행(윈도우버튼을 클릭하고 ruby라고 타이핑하면 바로가기가 뜬다) 해서 3일 입력하여 개발도구 포함버전으로 설치한다
* gem install jekyll bundler 로서 지킬을 설치해주고 jekyll -v 로 버전을 확인하여 설치가 정상적으로 진행되었는지 재확인필요!
* 깃허브 테마가 설치되어 있는 폴더로 이동해서 bundle add webrick 실행후 bundle exec jekyll serve 실행하면 로컬서버가 발동된다.

마크다운 문법을 숙지해서 글을 써내려가면 되겠다

> 쉬울거라 생각했던 깃허브에 블로그 테마 업로드하는 것이 ruby 버전에 따른 webrick 실행문제로 골머리를 쌓았다.

소감 몇마디를 마크다운 문법으로 적어내려가기.
