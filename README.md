# wiki-public

LLM/ML 학습 공개 위키. Obsidian-style 노트를 [Quartz v4](https://quartz.jzhao.xyz/)로
빌드해 GitHub Pages에서 호스팅.

## 콘텐츠 출처

`content/` 하위 페이지는 private vault에서 **사람이 직접 리뷰·승인한**
(`status: reviewed`) 노트만 자동 승격된 결과입니다. draft 또는 비공개 메모는
포함되지 않습니다.

## 로컬 개발

```bash
npm install
npx quartz build --serve  # http://localhost:8080
```

## 자동 배포

`main` 브랜치 push 시 GitHub Actions가 Quartz 빌드 → GitHub Pages 배포.
설정: `.github/workflows/deploy.yml`.

## 사이트

https://zzorong.github.io/wiki-public/ (Pages 활성화 후)
