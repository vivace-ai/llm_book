# LLM 완전 정복

『LLM 완전 정복: 직접 재며 익히는 LLM의 학습·튜닝·평가』(김영희 지음)의 예제 코드입니다. 책의 각 장에서 따라 실행하는 코드가 장별 폴더에 노트북으로 들어 있습니다.

## 책 소개

작은 트랜스포머 언어 모델을 처음부터 만들어 손실, 토크나이저, 요즘 모델의 부품, 사전 학습 자료, 스케일링 법칙을 재고, KV 캐시·디코딩·양자화로 생성의 계산을 잽니다. 이어 공개 모델(Qwen3-0.6B, HyperCLOVA X SEED 0.5B, Kanana 1.5 2.1B)을 내려받아 SFT, LoRA·QLoRA, DPO로 고쳐 쓰고, 평가와 환각, 프롬프트와 미세 조정 사이의 선택까지 숫자로 정합니다. 5부 16장입니다.

- 지은이: 김영희
- 발행: 2026년, 주식회사 부크크
- 판형: B5

## 폴더 구성

| 부 | 장 | 제목 | 노트북 | 저자 맥에서 걸린 시간 |
|---|---|---|---|---|
| 1부 작은 언어 모델을 처음부터 | 1 | 다음 토큰 예측을 숫자로 재기 | `ch01/ch01_next_token.ipynb` | 24분 |
|  | 2 | 토크나이저를 직접 학습시키기 | `ch02/ch02_tokenizer.ipynb` | 47분 |
|  | 3 | 요즘 트랜스포머의 부품을 하나씩 바꾸기 | `ch03/ch03_modern_parts.ipynb` | 58분 |
|  | 4 | 사전 학습 자료 만들기 | `ch04/ch04_pretraining_data.ipynb` | 25분 |
|  | 5 | 크기를 키우며 손실 재기 | `ch05/ch05_scaling.ipynb` | 80분 |
| 2부 생성의 계산 | 6 | 생성 속도 재기: KV 캐시와 배치 | `ch06/ch06_generation.ipynb` | 14분 |
|  | 7 | 디코딩 방법 비교하기 | `ch07/ch07_decoding.ipynb` | 16분 |
|  | 8 | 양자화: 8비트와 4비트 | `ch08/ch08_quantization.ipynb` | 15분 |
| 3부 공개 모델을 고쳐 쓰기 | 9 | 공개 모델 읽기 | `ch09/ch09_open_models.ipynb` | 9분 |
|  | 10 | 지시 따르기 학습(SFT) | `ch10/ch10_sft.ipynb` | 77분 |
|  | 11 | LoRA와 QLoRA | `ch11/ch11_lora.ipynb` | 64분 |
|  | 12 | 선호로 학습하기: DPO | `ch12/ch12_dpo.ipynb` | 46분 |
| 4부 LLM 평가 | 13 | LLM을 평가하는 방법 | `ch13/ch13_eval.ipynb` | 46분 |
|  | 14 | 모르는 것을 모른다고 하는가 | `ch14/ch14_hallucination.ipynb` | 25분 |
| 5부 프롬프트인가 학습인가 | 15 | 프롬프트와 컨텍스트를 숫자로 비교하기 | `ch15/ch15_prompt.ipynb` | 46분 |
|  | 16 | 미세 조정할까, 프롬프트로 할까 | `ch16/ch16_decide.ipynb` | 27분 |

## 실행 방법

노트북을 열고, 첫 칸의 **준비** 안내대로 자료 파일을 노트북과 같은 폴더(코랩은 왼쪽 파일 창)에 두거나 필요한 라이브러리를 설치한 다음, 위에서부터 차례로 실행합니다. 노트북에는 실행 결과를 넣지 않았습니다. 직접 실행해서 책의 출력과 비교합니다.

모든 노트북은 GPU 없이 CPU에서 실행합니다. 책의 숫자는 저자의 맥(Apple M5 Pro, CPU 스레드 2개)에서 얻었고, 걸린 시간은 위 표와 각 노트북의 첫 칸에 적었습니다. 기계와 라이브러리 버전이 다르면 같은 시드로도 학습한 모델의 손실이 0.001 단위에서 달라지고, 시간은 더 크게 달라집니다.

책의 숫자를 낸 환경은 다음과 같습니다.

| 항목 | 버전 |
|---|---|
| 파이썬 | 3.11.17 |
| 파이토치 | 2.15.0 (CPU, 스레드 2개) |
| tokenizers | 2~8장 0.23.3, 9장부터 0.22.2 |
| transformers | 4.57.6 (9장부터. 5.x는 Kanana의 설정을 불러오지 못한다) |
| peft, accelerate | 0.21.2, 1.15.0 (11장) |

transformers 4.57.6은 tokenizers 0.23.0 이하를 요구하므로 9장부터는 tokenizers 0.22.2를 씁니다.

책 본문에는 그래프를 그리는 코드를 싣지 않았습니다. 그래프 코드는 노트북에 모두 들어 있습니다.

## 자료와 모델

이 저장소에는 자료 파일과 모델 가중치를 넣지 않았습니다. 모두 누구나 내려받을 수 있습니다.

| 장 | 자료 | 받는 곳 |
|---|---|---|
| 1~4, 9~12, 15, 16 | NSMC `ratings_train.txt` (4장부터는 `ratings_test.txt`도) | [e9t/nsmc](https://github.com/e9t/nsmc) (CC0 1.0) |
| 4~8 | 한국어 위키백과 덤프 첫 조각 `kowiki-latest-pages-articles1.xml-p1p82407.bz2` (94MB, 책은 2026년 11월 1일 덤프) | [dumps.wikimedia.org/kowiki](https://dumps.wikimedia.org/kowiki/latest/) (CC BY-SA 4.0) |
| 13, 14 | KoBEST `copa/test.jsonl`, `hellaswag/test.jsonl` → `data/kobest/` | [skt/kobest_v1](https://huggingface.co/datasets/skt/kobest_v1) (CC BY-SA 4.0) |

9장부터 쓰는 모델은 9장 첫 셀이 Hugging Face에서 `data/models/`로 내려받습니다(세 모델 가중치 약 7.3GB).

| 모델 | 라이선스 | 이 책에서 |
|---|---|---|
| Qwen3-0.6B | Apache 2.0 | 실행, 미세 조정(10~13, 16장) |
| Kanana 1.5 2.1B | Apache 2.0 | 실행 |
| HyperCLOVA X SEED 0.5B | HyperCLOVA X SEED 모델 라이선스(사용 조건이 있다. 9.2절) | 실행 |
| EXAONE 4.0 1.2B | EXAONE AI 모델 라이선스 1.2-NC(연구·교육 목적만) | 설정 파일·모델 카드·라이선스만 읽는다 |

공개 자료는 수정될 수 있으므로 받은 날짜가 다르면 책의 숫자와 소수 끝자리가 다를 수 있습니다. 영화평 자료에는 거친 표현이 들어 있는 글이 있습니다.
