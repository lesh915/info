# info

`lesh915/info`는 LLM, 지식 그래프, 에이전트 기반 문서화와 관련된 연구/설계 자료를 모아 둔 정보 저장소입니다. 현재 저장소는 크게 `llm-wiki/`와 `engineering/` 자료군으로 나뉘며, 이 README는 그중 LLM-Wiki 관련 문서의 위치와 읽는 순서를 정리합니다.

## 저장소 개요

- `llm-wiki/`: LLM-Wiki 패턴, 2026년 기술 흐름, 권고 아키텍처, Graphify 연계, LLM 추출 스테이징 전략을 다루는 핵심 자료 모음입니다.
- `engineering/`: 그래프 엔지니어링, LangGraph, React 계열 기술 자료 등 구현/엔지니어링 참고 문서를 담고 있습니다.
- 루트 `README.md`: 저장소의 진입점입니다. 핵심 문서, 발표 자료, 권장 읽기 순서, 운영 원칙을 요약합니다.

## llm-wiki 디렉터리

`llm-wiki/`는 Andrej Karpathy의 LLM-Wiki 아이디어를 바탕으로, 원문 자료를 LLM이 지속적으로 읽고 정리해 상호 연결된 지식 베이스로 유지하는 패턴을 분석합니다. 단순한 RAG 대체안이 아니라, 원문 증거, Markdown 위키, 검색/그래프/에이전트 인터페이스를 함께 설계하는 지식 운영 방식으로 다룹니다.

핵심 관점은 다음과 같습니다.

- 원문 자료와 LLM이 생성한 위키를 분리합니다.
- Wiki는 source of truth가 아니라 원문에서 파생된 compiled knowledge layer로 둡니다.
- 모든 중요한 claim은 원문 근거와 연결되어야 합니다.
- 검색, 벡터, 그래프, MCP는 위키를 대체하는 요소가 아니라 에이전트가 위키를 더 잘 찾고 검증하게 만드는 보조 계층입니다.
- 자동 갱신은 필요하지만, 검증되지 않은 LLM 산출물이 운영 질의 경로에 바로 섞이지 않도록 해야 합니다.

## 핵심 문서

### `llm-wiki/LLM-Wiki_2026_Trend_and_Development_Guide_KO.html`

이 저장소의 LLM-Wiki 핵심 문서입니다. 2026년 기준 LLM-Wiki의 정의, 최신 기술 흐름, 비판적 평가, 권고 아키텍처, 디렉터리 설계, 데이터 모델, ingest/query 파이프라인, MCP/API 인터페이스, 품질 평가, 보안, 구축 로드맵을 한 번에 정리합니다.

LLM-Wiki 관련 의사결정을 할 때는 이 HTML 문서를 먼저 읽고, PPT 자료는 목적별 보조 설명 자료로 참고하는 것을 권장합니다.

## LLM-Wiki 관련 PPT 자료

| 파일 | 설명 |
| --- | --- |
| `llm-wiki/LLM-Wiki-소개_20260809.pptx` | LLM-Wiki를 처음 소개하는 기본 발표 자료입니다. RAG와의 차이, raw/wiki/schema 3계층, Ingest/Query/Lint 운영 방식, 한계와 도입 전략을 다룹니다. |
| `llm-wiki/LLM-Wiki-소개_20260809-1.pptx` | 기본 소개 자료의 확장 버전입니다. LLM-Wiki의 문제 정의, 컴파일 관점, 디렉터리 구조, 운영 방식 설명을 보강한 자료로 볼 수 있습니다. |
| `llm-wiki/LLM-Wiki-소개_20260809-2.pptx` | 소개 자료에 기존 그래프/벡터 자산이 있는 환경에서의 적용 판단과 도입 순서를 추가한 버전입니다. 이미 그래프가 있는 조직에서는 전면 재구축보다 좁은 LLM 추출 보완을 권합니다. |
| `llm-wiki/llm-wiki-structure-guide-v2.pptx` | LLM 위키 구조 설계와 개발 가이드를 다루는 2.0 초안입니다. Core + Domain Profile 모델, 근거 등급, 정보 모델, 스키마, 신뢰도, 검색 전략, 에이전트 계약, 거버넌스, 품질 평가, 도입 로드맵을 정리합니다. |
| `llm-wiki/llm-wiki-graphify.pptx` | LLM-Wiki와 Graphify를 결합하는 전략 자료입니다. Graphify를 위키의 대체재가 아니라 골격, 링크, 근거 태그, 갱신 자동화를 담당하는 하부 레이어로 설명합니다. |
| `llm-wiki/graphify-why.pptx` | Graphify 도입 이유를 짧게 압축한 자료입니다. 수동 링크 관리, 근거 없는 관계, 문서 노후화, 질의 인터페이스 부재 같은 LLM-Wiki 단독 운영의 한계를 설명합니다. |
| `llm-wiki/llm-extraction-staging-architecture.pptx` | 결정적 그래프와 Milvus 같은 벡터 자산을 이미 보유한 환경을 위한 LLM 추출 스테이징 아키텍처입니다. LLM-Wiki 전체를 영속 저장소로 쓰지 않고, 미연결 문서 청크에서 현장어/별칭 후보를 추출해 검수 후 승격하는 방식을 제안합니다. |

## 권장 읽기 순서

1. `llm-wiki/LLM-Wiki_2026_Trend_and_Development_Guide_KO.html`
   - 전체 기술 흐름과 권고 결론을 먼저 파악합니다.
2. `llm-wiki/LLM-Wiki-소개_20260809-2.pptx`
   - LLM-Wiki의 기본 개념과 실제 도입 판단을 빠르게 훑습니다.
3. `llm-wiki/llm-wiki-structure-guide-v2.pptx`
   - 저장소/스키마/거버넌스 설계를 구체화합니다.
4. `llm-wiki/llm-wiki-graphify.pptx`
   - 수동 위키 유지보수를 지식 그래프와 자동 추출로 보완하는 방법을 검토합니다.
5. `llm-wiki/graphify-why.pptx`
   - Graphify가 풀려는 문제를 요약본으로 재확인합니다.
6. `llm-wiki/llm-extraction-staging-architecture.pptx`
   - 이미 그래프/벡터 기반 지식 자산이 있는 환경에서 어떤 조각만 채택할지 판단합니다.
7. `llm-wiki/LLM-Wiki-소개_20260809.pptx`, `llm-wiki/LLM-Wiki-소개_20260809-1.pptx`
   - 교육/소개용 발표 흐름이 필요할 때 참고합니다.

## LLM-Wiki 권고 아키텍처

권장 구조는 순수 Markdown 위키나 순수 RAG 중 하나를 고르는 방식이 아니라, 역할이 다른 계층을 분리해 조합하는 방식입니다.

```text
raw sources
  -> immutable evidence store
  -> ingest / extraction pipeline
  -> compiled wiki pages
  -> indexes / search / graph traversal
  -> agent interface
  -> cited answers / wiki maintenance
```

권고 계층은 다음과 같습니다.

- **Source layer**: PDF, HTML, 회의록, 코드, 이미지, 데이터 파일 등 원문을 불변 또는 버전 고정 형태로 보관합니다.
- **Evidence layer**: 원문 해시, 출처, 수집 시각, 권한, claim이 참조한 span/page/bbox/timecode를 기록합니다.
- **Compiled Wiki layer**: LLM이 읽고 갱신하는 Markdown 기반 요약, 엔티티, 개념, 비교, 합성 페이지를 둡니다.
- **Retrieval layer**: 작은 규모에서는 `index.md`와 `log.md` 중심으로 시작하고, 규모가 커지면 BM25, dense vector, rerank, graph traversal을 추가합니다.
- **Graph layer**: 모든 지식을 그래프로 강제하지 않고, 관계 질의, dependency, lineage, multi-hop 탐색이 필요한 부분에 선택적으로 적용합니다.
- **Agent interface layer**: `AGENTS.md`/`CLAUDE.md`, MCP tools, search/read/follow/evidence/lint 같은 도구 계약을 통해 에이전트가 위키를 안정적으로 탐색하게 합니다.
- **Governance layer**: lint, stale check, contradiction check, citation support check, 승인/반려 로그, write 권한 분리를 운영합니다.

## 문서 관리 원칙

- 원문과 위키를 섞지 않습니다. `raw`는 근거이고, `wiki`는 해석과 재구성입니다.
- 중요한 주장은 claim 단위로 출처를 추적합니다. 페이지 단위 인용만으로 충분하다고 보지 않습니다.
- LLM이 생성한 내용은 검증 전까지 최종 사실로 승격하지 않습니다.
- 최신 문서가 항상 더 정확하다고 가정하지 않습니다. authority, valid time, transaction time을 분리해 판단합니다.
- index와 log를 작고 일관되게 유지합니다. 에이전트가 첫 진입점으로 읽을 수 있어야 합니다.
- AGENTS.md 또는 CLAUDE.md는 백과사전이 아니라 탐색/작성/검증 규칙을 담는 계약 문서로 둡니다.
- 자동화 산출물과 사람이 검수한 정본을 분리합니다.
- 삭제보다 superseded, retracted, disputed 같은 상태 표시를 우선합니다.
- 벡터 인덱스와 그래프는 재생성 가능한 파생물로 관리합니다.
- 민감 정보, 개인정보, 고객 원문은 권한/보안 정책 없이 LLM-Wiki에 직접 넣지 않습니다.

## 주요 연구 주제

- LLM-Wiki와 RAG의 역할 분담: query-time retrieval과 ingest-time compilation의 비용, 정확도, 유지보수성 비교
- Retrieval-as-Reasoning: search, read, follow, sufficiency check를 반복하는 agent-native retrieval
- Hybrid Wiki + RAG: compiled knowledge와 long-tail source retrieval의 결합
- Provenance-first knowledge base: claim에서 source span까지 내려가는 근거 추적
- Graph-backed Wiki: Markdown 위키와 typed entity/relation graph의 결합
- Temporal/Bitemporal Wiki: 현재 사실, 과거 사실, 시스템이 알게 된 시점을 분리하는 시간 모델
- Multimodal Wiki: 표, 차트, 이미지, 레이아웃, 수식, 음성/영상 segment를 원문 근거와 함께 관리하는 방식
- MCP-served Wiki: 여러 에이전트와 IDE가 동일 지식 베이스를 search/read/evidence/lint 도구로 사용하는 인터페이스
- Self-correcting Wiki: dangling link, unsupported claim, stale page, contradiction을 Error Book과 lint로 관리하는 운영 루프
- Graphify 연계: 코드/문서에서 결정적으로 추출 가능한 구조를 그래프로 만들고, 사람이 검수한 위키 정본과 분리해 운영하는 방식
- LLM 추출 스테이징: 기존 결정적 그래프/벡터 자산이 있는 환경에서 미연결 청크만 LLM으로 보완하고, SME 검수 후 승격하는 구조
