# Localrule KR

> 대한민국 자치법규(조례·규칙)를 Git으로 관리합니다.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE) [![data](https://img.shields.io/badge/data-Markdown-blue)](kr/) [![source](https://img.shields.io/badge/source-법제처_DRF_OpenAPI-orange)](https://open.law.go.kr)

대한민국 광역·기초 지자체가 제정·시행하는 **자치법규(조례·규칙·훈령 등)** 를 Markdown + YAML frontmatter 로 변환하여 Git 저장소에서 관리합니다. 각 자치법규는 공포일자를 Git commit date 로 갖고, 지자체명·법규명·조문을 메타·본문으로 보관합니다.

법령·행정규칙·판례·해석례·헌재결정례에 이어, **자치법규**까지 Git 으로 추적해 중앙·지방 법령의 전체 체계를 한 곳에서 관리합니다.

## 왜 필요한가?

지방자치 시대, **시민 일상에 가장 가까운 법은 자치법규** 입니다. 주차·건축·환경·복지·세제 등 실생활 규제 다수가 지자체 조례에 있으며, 같은 영역도 지자체별로 다릅니다.

```
국토계획법 (전국 공통)
  └─ 서울특별시 도시계획 조례 (서울 특화)
  └─ 부산광역시 도시계획 조례 (부산 특화)
  └─ 제주특별자치도 도시계획 조례 (제주 특화)
```

## 빠른 시작

```bash
git clone https://github.com/wellsa-ai/localrule-kr.git
cd localrule-kr

# 특정 자치법규 보기
cat kr/서울특별시/서울특별시_도시계획_조례.md

# 모든 지자체의 비슷한 조례 비교
grep -rl "주차장 설치" kr/
```

## 구조

```
kr/{지자체명}/
  {법규명}.md            # 자치법규 본문 (조문)
  ...
```

지자체 분류:
- 광역: 서울특별시, 부산광역시 등 17개
- 기초: 시·군·자치구 226개

## 메타데이터 (YAML Frontmatter)

```yaml
---
법규명: "서울특별시 도시계획 조례"
법규구분: "조례"
지자체: "서울특별시"
공포일자: "2024-06-15"
시행일자: "2024-09-01"
공포번호: "조례 제8XXX호"
출처: "https://www.law.go.kr/자치법규/(서울특별시 도시계획 조례)"
---
```

## 자동 업데이트

매일 [국가법령정보센터 DRF API](https://open.law.go.kr) 의 `target=ordin` 을 체크하여 신규·개정 자치법규가 있으면 자동으로 커밋합니다.

- `pipeline/cron_update.sh` — 매일 06:00 KST
- `pipeline/cron_full_sweep.sh` — 매일 23:30 KST

## 관련 프로젝트

| 프로젝트 | 대상 | 설명 |
|---|---|---|
| [legalize-kr](https://github.com/legalize-kr/legalize-kr) | 법률·시행령 | 대한민국 법령 |
| [regulate-kr](https://github.com/wellsa-ai/regulate-kr) | 행정규칙·고시 | 전 부처 행정규칙 |
| [precedent-kr](https://github.com/wellsa-ai/precedent-kr) | 법원 판례 | 대한민국 법원 판례 |
| [interpretation-kr](https://github.com/wellsa-ai/interpretation-kr) | 법령해석례 | 법제처 법령해석례 |
| [constitution-kr](https://github.com/wellsa-ai/constitution-kr) | 헌재결정례 | 헌법재판소 결정례 |
| **localrule-kr** (이 저장소) | 자치법규 | 지자체 자치법규 |
| [treaty-kr](https://github.com/wellsa-ai/treaty-kr) | 조약 | 대한민국 조약 |

## 활용 사례

- **시민 일상 규제 확인**: 우리 지자체의 주차·건축·환경 조례 즉시 확인
- **부동산·창업 사전 점검**: 지역별 인허가 요건 비교
- **지방자치 연구**: 지자체별 정책 비교, Git history 로 조례 변화 추적

## 데이터 출처

모든 자치법규 데이터는 [국가법령정보센터 DRF API](https://open.law.go.kr) 에서 가져옵니다. 자치법규 원문은 대한민국 정부 공공저작물로 자유롭게 이용 가능합니다.

## 라이선스

- 자치법규 원문: 공공저작물 (대한민국 정부)
- 저장소 구조·파이프라인 코드: MIT
