---
title: "2025년 하반기 회고"
date: 2026-03-28
tags:
  - 회고
summary: "좀 많이 뒤늦게 회고를 해보았습니다.."
draft: true
---

## 하반기 결심 체크리스트

- [ ] 

## 목표

- 공부한 내용과 프로젝트 회고를 읽기 쉽게 정리한다.
- 이미지/코드/요약을 일정한 형태로 유지한다.

## 기본 구조

1. **배경**: 왜 이 글을 쓰는지 한 단락
2. **핵심 내용**: 개념/문제/해결 과정을 단계별로
3. **정리**: 배운 점과 다음 액션

## 이미지 사용

표준 Markdown 이미지:

```md
![](image.jpg)
```

캡션이 필요하면 Hugo 기본 `figure`를 사용:

```md
{{< figure src="image.jpg" caption="여기에 캡션을 적습니다." >}}
```

## 썸네일(대표 이미지)

이 글처럼 폴더 안에 `cover.jpg`를 두고, 프론트매터에 아래를 추가하면 됩니다.

```yaml
featuredImage: "cover.jpg"
featuredImagePreview: "cover.jpg"
```

> 필요하면 `cover.jpg` 대신 원하는 파일명을 넣으면 됩니다.
