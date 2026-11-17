<div align="center">

![logo](./images/logo.png)

</div>

<div align="center">

![visitors](https://visitor-badge.laobi.icu/badge?page_id=jingyaogong/minimind)
[![GitHub Repo stars](https://img.shields.io/github/stars/jingyaogong/minimind?style=social)](https://github.com/jingyaogong/minimind/stargazers)
[![GitHub Code License](https://img.shields.io/github/license/jingyaogong/minimind)](LICENSE)
[![GitHub last commit](https://img.shields.io/github/last-commit/jingyaogong/minimind)](https://github.com/jingyaogong/minimind/commits/master)
[![GitHub pull request](https://img.shields.io/badge/PRs-welcome-blue)](https://github.com/jingyaogong/minimind/pulls)
[![Collection](https://img.shields.io/badge/🤗-MiniMind%20%20Collection-blue)](https://huggingface.co/collections/jingyaogong/minimind-66caf8d999f5c7fa64f399e5)

</div>

<div align="center">

![GitHub Trend](https://trendshift.io/api/badge/repositories/12586)

</div>

<div align="center">
  <h3>"대도지간(大道至简): 위대한 도는 지극히 단순하다"</h3>
</div>

<div align="center">

[中文](./README.md) | [English](./README_en.md) | 한국어

</div>

* 이 오픈소스 프로젝트는 완전히 0부터 시작해, 단 3위안의 비용과 2시간의 학습 시간만으로 약 64M 규모의 초소형 언어 모델 MiniMind를 학습시키는 것을 목표로 합니다.
* MiniMind 시리즈는 매우 가볍습니다. 메인라인 최소 버전의 크기는 GPT-3의 약 $\frac{1}{2700}$ 수준으로, 일반 개인용 GPU로도 빠르게 학습과 재현을 마칠 수 있도록 하는 것을 지향합니다.
* 프로젝트는 대형 모델의 극도로 단순화된 구조와 완전한 학습 파이프라인도 함께 공개합니다. MoE, 데이터 정제, 사전학습(Pretrain), 지도 미세조정(SFT), LoRA, RLHF(DPO), RLAIF(PPO / GRPO / CISPO), Tool Use, Agentic RL, 적응형 사고(Adaptive Thinking), 모델 증류 등 전 과정의 코드를 포함합니다.
* MiniMind는 시각 모달 모델 [MiniMind-V](https://github.com/jingyaogong/minimind-v), 멀티모달 Omni 모델 [MiniMind-O](https://github.com/jingyaogong/minimind-o), 확산 언어 모델(MiniMind-dLM), 선형 모델(MiniMind-Linear)로도 확장되었습니다. 자세한 내용은 [Discussion](https://github.com/jingyaogong/minimind/discussions)을 참고하세요.
* 프로젝트의 모든 핵심 알고리즘 코드는 PyTorch 네이티브로 0부터 구현했으며, 서드파티 라이브러리가 제공하는 고수준 추상화 인터페이스에 의존하지 않습니다.
* 이것은 대규모 언어 모델의 전 단계를 오픈소스로 재현하는 프로젝트일 뿐 아니라, LLM 입문과 실습을 위한 튜토리얼이기도 합니다.
* 이 프로젝트가 더 많은 사람들에게 재현 가능하고, 이해 가능하며, 확장 가능한 출발점이 되어, 함께 창조의 즐거움을 느끼고 더 넓은 AI 커뮤니티의 발전을 이끌 수 있기를 바랍니다.

> 참고: 본 프로젝트는 Apache 2.0 라이선스로 공개되며 완전히 무료입니다. "2시간"은 SFT 단계를 NVIDIA 3090 단일 카드에서 `1 epoch` 돌렸을 때의 실측 소요 시간이고, "3위안"은 해당 시간 동안의 GPU 대여 비용을 의미합니다.

---

<div align="center">

![minimind-3](./images/minimind-3.gif)

[🔗 온라인 체험](https://www.modelscope.cn/studios/gongjy/MiniMind) | [🔗 영상 소개](https://www.bilibili.com/video/BV12dHPeqE72)


<div align="center">
  <table>
    <tr>
      <td align="center">
        <a href="https://huggingface.co/collections/jingyaogong/minimind" style="text-decoration: none;">
          <img src="./images/with_huggingface.png" alt="Hugging Face Logo" style="vertical-align: middle; width: auto; max-width: 100%;" />
        </a>
      </td>
      <td align="center">
        <a href="https://www.modelscope.cn/profile/gongjy" style="text-decoration: none;">
          <img src="./images/with_modelscope.png" alt="ModelScope Logo" style="vertical-align: middle; width: auto; max-width: 100%;" />
        </a>
      </td>
    </tr>
  </table>
</div>


</div>

---

# 📌 프로젝트 소개

대규모 언어 모델(Large Language Model, LLM)의 등장은 전 세계적으로 AI에 대한 전례 없는 관심을 불러일으켰습니다. ChatGPT든 DeepSeek이든 Qwen이든, 모두 놀라운 성능으로 이 기술 물결의 파급력을 실감하게 해 주었습니다. 그러나 툭하면 수백억 개에 달하는 파라미터 규모 때문에, 개인 장비로는 학습은커녕 배포조차 요원해 보입니다. 대형 모델의 "블랙박스"를 열고 그 내부 작동 원리를 진정으로 이해하는 일은 본래 가슴 뛰는 일이어야 합니다. 안타깝게도 대부분의 탐구는 결국 LoRA 같은 기술로 기존 대형 모델을 약간 미세조정해 새로운 명령이나 특정 작업을 학습시키는 데서 멈춥니다. 이는 마치 뉴턴에게 21세기 스마트폰 사용법을 가르치는 것과 같습니다. 흥미롭긴 하지만, 물리학의 본질을 이해한다는 원래의 목적에서는 벗어나 있습니다.

한편, `transformers` / `trl` / `peft` 같은 서드파티 대형 모델 프레임워크와 툴 라이브러리는 대개 고도로 추상화된 인터페이스만 노출합니다. 단 십여 줄의 코드만으로 "모델 로드 + 데이터셋 로드 + 추론 + 강화학습"의 전체 학습 과정을 완료할 수 있습니다. 이런 효율적인 캡슐화는 분명 편리하지만, 어느 정도는 개발자를 하위 구현으로부터 격리시켜 LLM 핵심 코드를 깊이 이해할 기회를 약화시킵니다. 저는 "레고로 비행기를 직접 조립하는 것이 퍼스트 클래스에 앉아 비행하는 것보다 훨씬 더 신나는 일"이라고 생각합니다. 그런데 더 현실적인 문제는, 인터넷에 유료 강의와 마케팅 콘텐츠가 넘쳐나고, 허점투성이에 어설프게 아는 설명으로 이른바 AI 튜토리얼을 포장하고 있다는 점입니다. 바로 그렇기 때문에 이 프로젝트의 취지는 LLM의 학습 문턱을 최대한 낮춰, 누구나 코드 한 줄 한 줄을 이해하는 것부터 시작해 0부터 직접 초소형 언어 모델을 학습시킬 수 있도록 하는 것입니다. 그렇습니다. **처음부터 학습(training from scratch)**시키는 것이지, 단순히 **추론** 수준에 머무르는 것이 아닙니다. 최소 3위안도 안 되는 서버 비용만으로 0에서 1까지 언어 모델을 구축하는 전 과정을 직접 체험할 수 있습니다.

😊 함께 창조의 즐거움을 느껴 봅시다!

---

#### 🎉 본 프로젝트에 포함된 내용

- 완전한 MiniMind-LLM 구조 코드(Dense + MoE)를 제공하며, 현재 메인라인 구조는 `Qwen3 / Qwen3-MoE` 생태계에 맞춰져 있습니다.
- Tokenizer 및 토크나이저 학습 코드를 제공하며, `<tool_call>`, `<tool_response>`, `<think>` 등의 템플릿 토큰을 지원합니다.
- Pretrain, SFT, LoRA, RLHF-DPO, RLAIF(PPO / GRPO / CISPO), Tool Use, Agentic RL, 적응형 사고, 모델 증류 등 완전한 학습 과정을 다룹니다.
- 수집, 증류, 정제, 중복 제거를 거친 고품질 데이터셋을 포함해 전 단계의 오픈 데이터를 제공합니다.
- 핵심 학습 알고리즘과 주요 모듈은 모두 0부터 구현했으며, 서드파티 프레임워크의 캡슐화에 의존하지 않습니다.
- `transformers`, `trl`, `peft` 등 주류 프레임워크는 물론, `llama.cpp`, `vllm`, `ollama` 등 흔히 쓰이는 추론 엔진과 `Llama-Factory` 같은 학습 프레임워크와도 호환됩니다.
- 단일 머신 단일 GPU 및 단일 머신 다중 GPU(DDP, DeepSpeed) 학습을 지원하며, wandb / swanlab 시각화와 학습의 동적 중단·재개를 지원합니다.
- C-Eval, C-MMLU, OpenBookQA 등 서드파티 평가셋에서의 평가를 지원하며, YaRN을 통한 RoPE 장문 외삽을 지원합니다.
- OpenAI API 프로토콜과 호환되는 초간단 서버를 제공해 FastGPT, Open-WebUI 등 서드파티 Chat UI에 쉽게 연결할 수 있으며, `reasoning_content`, `tool_calls`, `open_thinking`을 지원합니다.
- Streamlit 기반의 초간단 채팅 WebUI를 제공하며, 사고 과정 표시, 도구 선택, 다중 턴 Tool Call을 지원합니다.
- 실험적 확장 포함: 이산 확산 언어 모델([dLM](https://github.com/jingyaogong/minimind/discussions/618))과 선형 어텐션 모델([Linear Attention](https://github.com/jingyaogong/minimind/discussions/704)). 둘 다 메인라인 AR 모델을 기반으로 이어서 학습할 수 있습니다.

#### 🎉 공개된 모델 목록

| 모델 | 파라미터 수 | 릴리스 |
|------|--------|---------|
| minimind-3 | 64M | 2026.04.01 |
| minimind-3-moe | 198M-A64M | 2026.04.01 |
| minimind2-small | 26M | 2025.04.26 |
| minimind2-moe | 145M | 2025.04.26 |
| minimind2 | 104M | 2025.04.26 |
| minimind-v1-small | 26M | 2024.08.28 |
| minimind-v1-moe | 4×26M | 2024.09.17 |
| minimind-v1 | 108M | 2024.09.01 |


---

#### 📝 업데이트 로그

<details> 
<summary> <b>🔥 2026-04-01</b> </summary>

 - `minimind-3` / `minimind-3-moe` 공개: 구조, Tokenizer, 학습 파이프라인, 추론 인터페이스, 기본 설정 전면 업데이트
- 구조 메인라인을 `Qwen3 / Qwen3-MoE` 생태계에 맞춤: Dense 약 `64M`, MoE 약 `198M-A64M`, shared expert 설계 제거
- 기본 학습 데이터를 `pretrain_t2t(_mini).jsonl`, `sft_t2t(_mini).jsonl`, `rlaif.jsonl`, `agent_rl.jsonl`, `agent_rl_math.jsonl`로 전환
- 독립적인 `train_reason.py` 제거. 사고 능력은 `chat_template + <think>`와 `open_thinking` 적응형 스위치로 통합 제어
- `toolcall` 능력을 `sft_t2t / sft_t2t_mini` 메인라인 데이터에 혼합하여, 기본 `full_sft`만으로도 기본적인 Tool Call 능력을 갖춤. `scripts/chat_api.py` 등 추론 예제도 추가
- 네이티브 `Agentic RL` 학습 스크립트 `train_agent.py` 추가, 다중 턴 Tool-Use 시나리오에서 `GRPO / CISPO` 지원
- RLAIF / Agentic RL 학습 과정에서 `rollout engine` 분리 완료, 생성 백엔드를 더 유연하게 전환 가능
- `serve_openai_api.py`와 `web_demo.py`에 `reasoning_content` / `tool_calls` / `open_thinking` 지원 추가
- Tokenizer를 `BPE + ByteLevel` 기반으로 업데이트하고 도구 호출 및 사고 토큰을 추가, 향후 확장을 위한 buffer token 예약
- LoRA 가중치 병합·내보내기 흐름 추가: `scripts/convert_model.py`로 기본 모델과 LoRA 가중치를 병합해 새로운 완전한 모델 가중치로 만들 수 있음
- 구조도 리소스 업데이트, README 대폭 업데이트

</details>

<details> 
<summary> <b>2025-10-24</b> </summary>

- 🔥 RLAIF 학습 알고리즘 추가: PPO, GRPO, SPO (0부터 네이티브 구현)
- 체크포인트 이어서 학습 기능 추가: 학습 자동 복구, GPU 수가 달라도 복구, wandb 기록 연속성 지원
- RLAIF 데이터셋 추가: rlaif-mini.jsonl (SFT 데이터에서 1만 건 무작위 샘플링). DPO 데이터셋 간소화, 중국어 데이터 추가
- YaRN 알고리즘 추가: RoPE 장문 외삽 지원, 긴 시퀀스 처리 능력 향상
- Adaptive Thinking: Reason 모델에서 사고 체인(CoT) 사용 여부 선택 가능
- chat_template이 Tool Calling과 Reasoning 태그(`<tool_call>`, `<think>` 등)를 전면 지원
- RLAIF 전체 장, 학습 곡선 비교, 알고리즘 원리 접기 설명 추가
- [SwanLab](https://swanlab.cn/)으로 WandB 대체 (중국 내 접속 친화적, API 완전 호환)
- 모든 코드 정규화 & 알려진 버그 일부 수정

</details>

<details> 
<summary> <b>2025-04-26</b> </summary>

- 중요 업데이트
- 호환성이 필요한 경우 [🔗이전 저장소 내용🔗](https://github.com/jingyaogong/minimind/tree/7da201a944a90ed49daef8a0265c959288dff83a)을 참고하세요.
- MiniMind 모델 파라미터 이름을 전면 변경하여 Transformers 라이브러리 모델과 맞춤(명명 통일).
- generate 방식을 리팩터링하여 GenerationMixin 클래스를 상속하도록 변경.
- 🔥 llama.cpp, vllm, ollama 등 인기 서드파티 생태계 지원.
- 코드와 디렉터리 구조 정규화.
- 어휘표 변경 `<s></s>`->`<|im_start|><|im_end|>`

```text
서드파티 추론 프레임워크 llama.cpp, vllm과의 호환을 위해, 이번 업데이트에는 상당한 대가가 따릅니다.
이번 업데이트부터 25-04-26 이전의 구 모델을 「직접」 로드해 추론하는 것은 더 이상 지원하지 않습니다.
Llama의 위치 인코딩 방식이 minimind와 달라서, Llama 모델로 매핑한 후 QK 값에 차이가 생깁니다.
minimind2 시리즈 구 모델은 모두 가중치 매핑 + (미세조정 학습) QKVO 선형층 보정을 거쳐 복원되었습니다.
이번 업데이트 이후 `minimind-v1` 전 시리즈의 유지보수를 중단하고 저장소에서 내립니다.
```

</details>

<details>
<summary> <b>More...</b> </summary>

**2025-02-09**
- 공개 이후 최대 규모 업데이트, minimind2 시리즈 릴리스.
- 코드를 거의 전부 리팩터링하여 더 간결하고 명확한 통합 구조 사용.
  구 코드와의 호환성이 필요한 경우 [🔗이전 저장소 내용🔗](https://github.com/jingyaogong/minimind/tree/6e9cd28ef9b34a0a10afbdf6f59e65cb6e628efb)을 참고하세요.
- 데이터 전처리 단계 생략. 데이터셋 형식을 통일하여 `jsonl` 형식으로 변경, 데이터셋 다운로드 혼란 문제 해소.
- minimind2 시리즈의 성능이 MiniMind-V1 대비 크게 향상됨.
- 자잘한 개선: {kv-cache 구현이 더 표준적으로, MoE의 로드 밸런싱 loss 반영 등}
- 모델을 사설 데이터셋으로 이전하는 학습 방안 제공(의료 모델, 자기 인식 예시).
- 사전학습 데이터셋을 간소화하고 품질을 대폭 향상시켜, 개인이 빠르게 학습하는 데 필요한 시간을 크게 단축. 3090 단일 카드로 2시간 만에 재현 가능!
- 업데이트: LoRA 미세조정을 peft 래핑에서 분리하여 0부터 LoRA 구현. DPO 알고리즘을 PyTorch 네이티브로 0부터 구현. 모델 화이트박스 증류 네이티브 구현.
- minimind2-DeepSeek-R1 시리즈 증류 모델 탄생!
- minimind2가 어느 정도 영어 능력을 갖춤!
- 더 많은 대형 모델 리더보드 기반으로 minimind2와 서드파티 모델의 성능 테스트 결과 업데이트.

**2024-10-05**
- MiniMind에 멀티모달 능력 중 하나인 시각(vision)을 확장
- 자매 프로젝트 [minimind-v](https://github.com/jingyaogong/minimind-v)에서 자세한 내용을 확인하세요!

**2024-09-27**
- 09-27 pretrain 데이터셋 전처리 방식 업데이트. 텍스트 완전성을 보장하기 위해 .bin으로 전처리해 학습하는 방식을 포기(학습 속도를 약간 희생).
- 현재 pretrain 전처리 후 파일 이름: pretrain_data.csv.
- 일부 불필요한 코드 삭제.

**2024-09-17**
- minimind-v1-moe 모델 업데이트
- 모호성을 피하기 위해 mistral_tokenizer를 더 이상 사용하지 않고, 모두 자체 minimind_tokenizer를 토크나이저로 사용.

**2024-09-01**
- minimind-v1 (108M) 모델 업데이트. minimind_tokenizer 사용, 사전학습 3 epoch + SFT 10 epoch로 더 충분히 학습하여 성능 강화.
- 프로젝트를 ModelScope 창공간(Studio)에 배포했으며, 다음 사이트에서 체험할 수 있습니다:
- [🔗ModelScope 온라인 체험🔗](https://www.modelscope.cn/studios/gongjy/minimind)

**2024-08-27**
- 프로젝트 최초 공개

</details>

---

# 📌 빠른 시작

<details>
<summary>필자의 소프트웨어/하드웨어 구성 (참고용)</summary>

* CPU: Intel(R) Core(TM) i9-10980XE CPU @ 3.00GHz
* RAM: 128 GB
* GPU: NVIDIA GeForce RTX 3090 (24GB) * 8
* Ubuntu==20.04
* CUDA==12.2
* Python==3.10.16
* [requirements.txt](./requirements.txt)

</details>

## 0단계

```bash
# 저장소 클론, 의존성 설치
git clone --depth 1 https://github.com/jingyaogong/minimind
cd minimind && pip install -r requirements.txt -i https://mirrors.aliyun.com/pypi/simple
```

## Ⅰ 🚀 모델 추론

### 1' 모델 다운로드

프로젝트 루트 디렉터리에서:
```bash
# 방법 1
modelscope download --model gongjy/minimind-3 --local_dir ./minimind-3
# 방법 2
git clone https://huggingface.co/jingyaogong/minimind-3
```

### 2' CLI 추론

```bash
# 방법 1: Transformers 형식 모델 사용
python eval_llm.py --load_from ./minimind-3
# 방법 2: PyTorch 모델 기반 (./out 디렉터리에 해당 가중치가 있는지 확인)
python eval_llm.py --load_from ./model --weight full_sft
```

### 3' (선택) WebUI

```bash
# `python>=3.10`이 필요할 수 있으며, `pip install streamlit`으로 설치
# ⚠️ 먼저 transformers 형식 모델 폴더를 ./scripts/ 디렉터리에 복사해야 합니다(예: cp -r minimind-3 ./scripts/minimind-3). web_demo 스크립트는 이 디렉터리에서 가중치 파일이 들어 있는 하위 폴더를 자동으로 스캔하며, 없으면 오류가 발생합니다
cd scripts && streamlit run web_demo.py
```

### 4' (선택) 서드파티 추론 프레임워크

```bash
# ollama
ollama run jingyaogong/minimind-3
# vllm
vllm serve /path/to/model --served-model-name "minimind"
```

## Ⅱ 🛠️ 모델 학습

<details>
<summary>참고: Torch에서 사용 가능한 백엔드를 미리 확인하세요</summary>

```python
import torch
print(torch.cuda.is_available())
```

CUDA로 학습할 계획이라면, 먼저 현재 환경이 GPU를 올바르게 인식하는지 확인하는 것을 권장합니다.  
`cuda`를 사용할 수 없더라도 장비에 따라 `CPU`나 `MPS`로 실행할 수는 있지만, 학습 속도와 호환성에는 매우 큰 차이가 있습니다.  
PyTorch 버전을 설치하거나 교체해야 한다면 [torch_stable](https://download.pytorch.org/whl/torch_stable.html)과 [링크](https://blog.csdn.net/weixin_45456738/article/details/141029610?ops_request_misc=&request_id=&biz_id=102&utm_term=%E5%AE%89%E8%A3%85torch&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-2-141029610.nonecase&spm=1018.2226.3001.4187)를 참고하세요.

</details>

### 1' 데이터 다운로드

아래에 제공된 [데이터셋 다운로드 링크](https://www.modelscope.cn/datasets/gongjy/minimind_dataset/files)에서 필요한 데이터 파일을 내려받아 `./dataset` 디렉터리에 넣으세요.

> 현재 기본적으로 `pretrain_t2t_mini.jsonl`과 `sft_t2t_mini.jsonl`만 다운로드하면 `MiniMind Zero` 대화 모델을 비교적 빠르게 재현할 수 있습니다.
더 많은 요구가 있다면 아래에 다양한 조합 방안을 제공하니, 작업 목표와 GPU 자원에 따라 유연하게 선택하세요.

### 2' 학습 시작

<details>
<summary>💡 체크포인트 일시정지 후 이어서 학습</summary>

모든 학습 스크립트는 체크포인트 저장을 지원합니다. `--from_resume 1` 인자를 추가하면 학습 진행 상황을 자동으로 감지해 복구합니다:

```bash
python train_pretrain.py --from_resume 1
python train_full_sft.py --from_resume 1
# ...
```

**이어서 학습 설명:**
- 학습 과정에서 `./checkpoints/` 디렉터리에 완전한 체크포인트(모델, 옵티마이저, 학습 진행 상황 등)를 자동 저장
- 체크포인트 파일 이름: `<가중치이름>_<차원>_resume.pth` (예: `full_sft_512_resume.pth`)
- GPU 수가 달라져도 복구 지원 (step 자동 조정)
- wandb 학습 기록의 연속성 지원 (같은 run을 자동 복구)

> 장시간 학습이나 불안정한 환경에 적합하며, 학습 중단으로 진행 상황을 잃을 걱정이 없습니다

</details>

#### 2.1 사전학습 (필수)

```bash
cd trainer && python train_pretrain.py
```

> 학습 후 `out/pretrain_*.pth`가 출력 가중치로 생성됩니다(여기서 `*`는 모델 dimension이며 기본값은 `768`)

#### 2.2 지시 미세조정 (필수)

```bash
cd trainer && python train_full_sft.py
```

> 학습 후 `out/full_sft_*.pth`가 출력 가중치로 생성됩니다(여기서 `full`은 전체 파라미터 미세조정을 의미)

#### 2.3 학습된 모델 테스트 (선택)

테스트할 모델 `*.pth` 파일이 `./out/` 디렉터리에 있는지 확인하세요. [여기](https://www.modelscope.cn/models/gongjy/minimind-3-pytorch/files)에서 제가 학습해 둔 `*.pth` 가중치를 바로 내려받을 수도 있습니다.

```bash
python eval_llm.py --weight full_sft
```

> `--weight`는 가중치 이름 접두사를 지정합니다. 예: `pretrain`, `full_sft` 등. 더 많은 인자는 `eval_llm.py`를 직접 참고하세요

<details>
<summary>참고: 기타 알아둘 점</summary>

1. 모든 학습 스크립트는 PyTorch 네이티브로 구현되어 있으며 다중 GPU 가속을 지원합니다.

2. 장비에 `N (N > 1)`개의 그래픽카드가 있다면, 다음과 같이 단일 머신 `N`카드 학습을 시작할 수 있습니다(DDP, 다중 머신 다중 GPU로도 확장 가능):

```bash
torchrun --nproc_per_node N train_xxx.py
```

3. 필요에 따라 wandb로 학습 과정을 기록할 수 있습니다.

```bash
... train_xxx.py --use_wandb
```
`2025`년 `6`월 이후 중국 내 네트워크 환경에서는 대체로 WandB에 직접 접속할 수 없습니다. MiniMind는 현재 기본적으로 [SwanLab](https://swanlab.cn/)을 학습 시각화 도구로 사용하며, 인터페이스는 WandB와 거의 호환됩니다. 보통 `import wandb`를 `import swanlab as wandb`로 바꾸기만 하면 나머지 호출 방식은 거의 수정할 필요가 없습니다.

</details>

---

# 📌 데이터 소개

## Ⅰ Tokenizer

토크나이저는 대략 LLM이 사용하는 "사전"이라고 이해할 수 있습니다. 자연어를 token id로 매핑하고, 다시 token id를 텍스트로 디코딩하는 역할을 합니다. 프로젝트에는 어휘표 학습 예시로 `train_tokenizer.py`도 제공됩니다. 다만 tokenizer를 다시 학습하는 것은 권장하지 않습니다. 어휘표와 분할 규칙이 바뀌면 모델 가중치, 데이터 형식, 추론 인터페이스, 커뮤니티 생태계와의 호환성이 모두 떨어지고, 모델의 확산성도 약해지기 때문입니다. 또한 tokenizer는 PPL처럼 token 단위로 집계되는 지표에도 영향을 주므로, tokenizer가 다른 모델끼리 비교할 때는 BPB(Bits Per Byte)가 더 참고할 만한 경우가 많습니다. [이 글](https://skeptric.com/perplexity/)을 참고하세요.
MiniMind 같은 소형 모델에서는 어휘표 크기가 embedding 층과 출력층의 파라미터 비중에 직접 영향을 주므로, 어휘표를 작게 유지하는 것이 대개 더 적절한 선택입니다.

<details>
<summary>Tokenizer 소개</summary>

Yi, Qwen2, ChatGLM, Mistral, Llama 3 같은 강력한 서드파티 오픈소스 모델의 tokenizer 어휘표 크기는 다음과 같습니다:

<table>
  <tr><th>Tokenizer 모델</th><th>어휘표 크기</th><th>출처</th></tr>
  <tr><td>Yi</td><td>64,000</td><td>01.AI (중국)</td></tr>
  <tr><td>Qwen2</td><td>151,643</td><td>알리바바 클라우드 (중국)</td></tr>
  <tr><td>ChatGLM</td><td>151,329</td><td>즈푸AI (중국)</td></tr>
  <tr><td>Mistral</td><td>32,000</td><td>Mistral AI (프랑스)</td></tr>
  <tr><td>Llama 3</td><td>128,000</td><td>Meta (미국)</td></tr>
  <tr><td>MiniMind</td><td>6,400</td><td>자체 정의</td></tr>
</table>

> 현재 메인라인은 과거 버전과의 혼동을 피하고 전체 크기를 통제하기 위해 `minimind_tokenizer`로 통일했으며, `mistral_tokenizer` 버전은 더 이상 유지보수하지 않습니다.

`minimind_tokenizer`의 어휘표는 `6400`개에 불과해 `qwen2`, `glm` 같은 중국어 친화적 tokenizer보다 인코딩·디코딩 효율은 떨어지지만, embedding 층과 출력층의 파라미터 비중을 크게 줄일 수 있어 MiniMind 같은 소형 모델의 크기 제약에 더 적합합니다.
실제 사용 결과를 보면 이 tokenizer 때문에 희귀어 디코딩 실패 문제가 눈에 띄게 생기지는 않았고, 전반적으로 충분히 안정적입니다. 따라서 현재 메인라인 학습도 이 어휘표를 일관되게 사용하며, 다른 tokenizer 버전을 따로 분기해 유지하지 않습니다.

</details>

## Ⅱ Pretrain 데이터

`MiniMind-3`의 현재 메인라인 사전학습 데이터는 `pretrain_t2t.jsonl` / `pretrain_t2t_mini.jsonl`입니다.  
이 두 데이터는 통일된 `text -> next token prediction` 학습 형식으로 정리되어 있으며, 적은 연산량에서도 다음을 함께 고려하는 것을 목표로 합니다:

- 텍스트 품질
- 길이 분포
- 중국어·영어 혼합 능력
- 이후 SFT / Tool Calling / RLAIF 단계와의 템플릿 연계

데이터 출처에는 일반 텍스트 코퍼스, 정리된 대화 코퍼스, 증류 보충 코퍼스, 그리고 각종 **관대한 오픈소스 라이선스**로 사용 가능한 데이터셋 등이 포함되며 이에 국한되지 않습니다. 메인라인 데이터는 정제, 중복 제거, 길이 제어, 형식 통일을 거친 후 학습에 투입됩니다. 주요 출처: [장수(匠数) 대형 모델 데이터셋](https://www.modelscope.cn/datasets/deepctrl/deepctrl-sft-data), [Magpie-Align](https://www.modelscope.cn/organization/Magpie-Align) 등의 공개 데이터 소스.

그중:

- `pretrain_t2t_mini.jsonl`은 빠른 재현에 더 적합합니다.
- `pretrain_t2t.jsonl`은 `MiniMind-3` 메인라인 모델을 완전히 학습시키는 데 더 적합합니다.

파일 데이터 형식은 다음과 같습니다.

```jsonl
{"text": "어떻게 하면 미루는 습관에서 벗어날 수 있을까? 미루는 습관을 고치기란 쉽지 않지만, 다음 조언이 도움이 될 수 있다."}
{"text": "이른 아침 햇살이 커튼 사이로 방 안에 쏟아지고, 책상 위 책장이 바람에 살며시 넘겨진다."}
{"text": "Transformer는 셀프 어텐션 메커니즘으로 문맥 관계를 모델링하며, 현대 대규모 언어 모델의 중요한 기본 구조다."}
```

## Ⅲ SFT 데이터

`MiniMind-3`의 현재 메인라인 SFT 데이터는 `sft_t2t.jsonl` / `sft_t2t_mini.jsonl`입니다. 이전의 `sft_512 / sft_1024 / sft_2048` 방안과 비교해, 현재 버전은 다음을 더 강조합니다:

- 템플릿 통일
- 대화 + 사고 태그 + Tool Calling의 혼합 학습에 더 적합
- 데이터 전처리 분기를 최소화해 재현 비용 절감

데이터 출처에는 고품질 지시 수행 데이터, 공개 대화 데이터, 모델 증류 합성 데이터, 라이선스 친화적인 오픈소스 데이터셋 등이 포함되며 이에 국한되지 않습니다. `t2t` 메인라인에 들어가기 전에 현재 저장소가 사용하는 다중 턴 대화 형식으로 통일됩니다. 현재 메인라인에는 다량의 합성 데이터도 포함되어 있는데, 예를 들어 제가 `qwen3-4b`로 합성한 약 `10만` 건의 `tool call` 데이터, `qwen3` 시리즈의 `reasoning` 데이터 등이 있습니다. 커뮤니티의 주요 출처: [장수(匠数) 대형 모델 데이터셋](https://www.modelscope.cn/datasets/deepctrl/deepctrl-sft-data), [Magpie-Align](https://www.modelscope.cn/organization/Magpie-Align), [R1-Distill-SFT](https://www.modelscope.cn/datasets/AI-ModelScope/R1-Distill-SFT), [COIG](https://huggingface.co/datasets/BAAI/COIG), [Step-3.5-Flash-SFT](https://huggingface.co/datasets/stepfun-ai/Step-3.5-Flash-SFT) 등. 공개 버전은 데이터 출처와 처리 과정이 해당 오픈소스 라이선스의 전이성 제약을 충족하도록 하며, Apache-2.0, CC-BY-NC-2.0 등 관련 라이선스 요구사항을 준수합니다.

그중:

- `sft_t2t_mini.jsonl`: 대화 모델을 빠르게 학습시키는 데 적합
- `sft_t2t.jsonl`: 메인라인 버전을 완전히 재현하는 데 적합
- `toolcall` 능력은 이미 메인라인 SFT 데이터에 통합됨

모든 SFT 파일의 데이터 형식은 다음과 같습니다(대화 데이터, Tool Use 데이터 포함).

```jsonl
{
    "conversations": [
        {"role": "user", "content": "안녕"},
        {"role": "assistant", "content": "안녕하세요!"},
        {"role": "user", "content": "잘 가"},
        {"role": "assistant", "content": "안녕히 가세요!"}
    ]
}
{
    "conversations": [
        {"role": "system", "content": "# Tools ...", "tools": "[...]"},
        {"role": "user", "content": "'안녕 세계'를 english로 번역해 줘"},
        {"role": "assistant", "content": "", "tool_calls": "[{\"name\":\"translate_text\",\"arguments\":{\"text\":\"안녕 세계\",\"target_language\":\"english\"}}]"},
        {"role": "tool", "content": "{\"translated_text\":\"Hello World\"}"},
        {"role": "assistant", "content": "Hello World"}
    ]
}
```

## Ⅳ RL 데이터

`MiniMind`의 현재 메인라인 RL 데이터는 `dpo.jsonl`입니다. 데이터는 [DPO-En-Zh-20k](https://huggingface.co/datasets/llamafactory/DPO-En-Zh-20k)에서 샘플링했습니다.

메인라인에서는 이 샘플들을 현재 저장소가 사용하는 선호 학습 형식으로 통일해 재구성하며, 보상 모델이나 선호 최적화 단계의 학습에 사용합니다. 여기서 `chosen`은 선호에 더 부합하는 응답, `rejected`는 상대적으로 나쁜 응답을 나타냅니다.

`dpo.jsonl`의 데이터 형식은 다음과 같습니다.

```json
{
  "chosen": [
    {"content": "Q", "role": "user"}, 
    {"content": "good answer", "role": "assistant"}
  ], 
  "rejected": [
    {"content": "Q", "role": "user"}, 
    {"content": "bad answer", "role": "assistant"}
  ]
}
```

이 외의 다른 RL 데이터는 SFT 데이터와 형식이 같습니다. 보통 SFT 데이터에서 전체 길이와 대화 턴 수를 기준으로 걸러낸 것이며, 마지막 `assistant` 위치를 비워 두어 rollout 단계에서 이어서 생성하도록 합니다.

## Ⅴ MiniMind 학습 데이터셋

> [!NOTE]
> 현재 메인라인 학습에 필요한 핵심 데이터셋은 이미 공개되어 있으므로, 대규모 데이터셋을 직접 전처리할 필요가 없어 반복적인 데이터 처리 작업을 피할 수 있습니다.

MiniMind 학습 데이터셋 다운로드 주소: [ModelScope](https://www.modelscope.cn/datasets/gongjy/minimind_dataset/files) | [HuggingFace](https://huggingface.co/datasets/jingyaogong/minimind_dataset/tree/main)

> 전체를 clone할 필요 없이 필요한 파일만 따로 내려받을 수 있습니다

내려받은 데이터셋 파일을 `./dataset/` 디렉터리에 넣으세요(✨는 권장 필수 항목).

```bash
./dataset/
├── agent_rl.jsonl (86MB)
├── agent_rl_math.jsonl (18MB)
├── dpo.jsonl (53MB)
├── pretrain_t2t_mini.jsonl (1.2GB, ✨)
├── pretrain_t2t.jsonl (10GB)
├── rlaif.jsonl (24MB, ✨)
├── sft_t2t_mini.jsonl (1.6GB, ✨)
└── sft_t2t.jsonl (14GB)
```

<details>
<summary>참고: 각 데이터셋 소개</summary>

* `agent_rl.jsonl` --Agentic RL 메인라인 학습 데이터, `train_agent.py`의 다중 턴 Tool-Use / CISPO / GRPO 학습에 사용
* `agent_rl_math.jsonl` --Agentic RL 순수 수학 보충 데이터, 최종 검증 목표가 있는 다중 턴 추론/도구 사용 시나리오에 적합 (RLVR에 사용)
* `dpo.jsonl` --RLHF 단계 선호 학습 데이터 (DPO)
* `pretrain_t2t_mini`✨ --`minimind-3` 경량 사전학습 데이터, 빠른 재현에 적합 (`max_seq_len≈768` 설정 권장)
* `pretrain_t2t` --`minimind-3` 메인라인 사전학습 데이터 (`max_seq_len≈380` 설정 권장)
* `rlaif.jsonl`✨ --RLAIF 학습 데이터셋, PPO/GRPO/CISPO 등 강화학습 알고리즘 학습에 사용
* `sft_t2t_mini.jsonl`✨ --`minimind-3` 경량 SFT 데이터 (Zero 모델을 빠르게 학습시키는 용도), `max_seq_len≈768` 설정 권장, Tool Call 샘플이 일부 섞여 있음
* `sft_t2t.jsonl` --`minimind-3` 메인라인 SFT 데이터, 완전한 재현에 적합하며 마찬가지로 Tool Call 샘플이 섞여 있음


학습 인자 `max_seq_len`은 현재 절대 문자 수가 아니라 tokens 길이를 의미합니다.
본 프로젝트의 tokenizer는 중국어 텍스트에서 대략 `1.5~1.7 문자/token`, 순수 영어에서는 압축률이 `4~5 문자/token`이며, 데이터 분포에 따라 변동이 있습니다.
데이터셋 이름에 표기된 "최대 길이"는 모두 문자 수이며, 길이 100인 문자열은 대략 `100/1.5≈67` tokens 길이로 환산할 수 있습니다.

예를 들어:

* 중국어: `白日依山尽` 5개 문자는 [`白日`,`依`,`山`,`尽`] 4개 tokens로 분할될 수 있습니다.
* 영어: `The sun sets in the west` 24개 문자는 [`The `,`sun `,`sets `,`in `,`the`,`west`] 6개 tokens로 분할될 수 있습니다.

"권장 설정"은 각 데이터셋에서 최대 tokens 길이를 대략 추정한 값입니다.
`max_seq_len`은 공격적 / 보수적 / 균형적으로 조정할 수 있다는 점을 알아 두세요. 크게 하든 작게 하든 부작용은 피할 수 없습니다. 일부 샘플은 `max_seq_len`보다 짧아 padding으로 연산이 낭비되고, 일부 샘플은 `max_seq_len`보다 길어 의미가 잘립니다.

연산 효율과 의미 완전성 사이에서 균형점을 찾으면 됩니다.

</details>


![dataset](./images/dataset.jpg)

> MiniMind 메인라인 학습 데이터 구성과 권장 조합 개념도

<details>
<summary>설명 & 권장 학습 방안</summary>

* `minimind-3` 메인라인은 `pretrain_t2t` + `sft_t2t` + `rlaif/agent_rl`의 단계별 학습 조합을 권장합니다.

* 가장 빠르게 0부터 Zero 모델을 구현하고 싶다면 `pretrain_t2t_mini.jsonl` + `sft_t2t_mini.jsonl` 데이터 조합을 권장합니다.

* 어느 정도 연산 자원이 있거나 성능을 더 중시한다면 `minimind-3`를 완전히 재현하는 것을 권장하고, GPU가 한 장뿐이거나 빠른 재현을 더 중시한다면 mini 조합을 강력히 권장합니다.

* 현재 `sft_t2t / sft_t2t_mini`에는 이미 Tool Call 데이터가 섞여 있으므로, 보통 별도로 독립적인 Tool Calling 지도 미세조정을 한 번 더 할 필요가 없습니다.

</details>

# 📌 모델

## 구조

`minimind-3` Dense는 Transformer Decoder-Only 구조를 사용하며, 전체 설정이 `Qwen3` 생태계에 맞춰져 있어 이후 `transformers / llama.cpp / ollama / vllm`으로 변환하기 쉽습니다:

* 사전 정규화(Pre-Norm) + RMSNorm 사용
* SwiGLU 활성화 함수 사용
* RoPE 회전 위치 인코딩 사용, YaRN 외삽 지원
* `q_heads=8`, `kv_heads=4`, `max_position_embeddings=32768`, `rope_theta=1e6`

`minimind-3-moe`는 같은 구조에서 MoE 피드포워드 층으로 확장했으며, 구현상 `Qwen3-MoE` 스타일 설정과 호환됩니다(shared expert 제거).

* 현재 기본 설정은 `4 experts / top-1 routing`으로, 더 적은 활성 파라미터로 더 높은 용량을 얻기 위한 것입니다.
* Experts를 계속 늘리면 실제 소요 시간이 같은 크기의 dense 모델보다 훨씬 길어지는 경우가 많습니다. "MoE는 추론이 더 빠르다"는 말과 함께 놓고 보면 조금 직관에 반하지만, 학습 시에는 token을 먼저 전문가별로 버킷에 나눈 뒤 각각 forward를 수행하기 때문에, 네이티브 학습에서 발생하는 `kernel` 실행·종료 및 스케줄링 오버헤드가 급격히 커지는 것은 지극히 자연스러운 일입니다. 이는 MoE kernel-fused를 지원하는 연산자 라이브러리로 최적화해야 합니다. 예를 들어 `Triton` 기반 커스텀 kernel, `DeepSpeed-MoE`, `Megatron-LM` 등이 있습니다. 물론 이 프로젝트는 네이티브 PyTorch의 범용성을 유지하고 싶기 때문에 현실적인 절충을 택했으며, 현재 구현에서 `4 experts / top-1`이라는 최적점(sweet spot) 설정은 dense 모델보다 약 `50%` 정도만 느립니다.

`minimind-3` 시리즈 구조는 아래 그림과 같습니다:

![structure](./images/LLM-structure.jpg)
![structure-moe](./images/LLM-structure-moe.jpg)

모델 설정 수정은 [./model/model_minimind.py](./model/model_minimind.py)를 참고하세요. 참고용 모델 파라미터 버전은 아래 표와 같습니다:

| Model Name | params | len_vocab | max_pos | rope_theta | n_layers | d_model | kv_heads | q_heads | note |
|------------|--------|-----------|---------|------------|----------|---------|----------|---------|------|
| minimind-3 | 64M | 6400 | 32768 | 1e6 | 8 | 768 | 4 | 8 | Dense |
| minimind-3-moe | 198M-A64M | 6400 | 32768 | 1e6 | 8 | 768 | 4 | 8 | 4 experts / top-1 |
| minimind2-small | 26M | 6400 | 32768 | 1e6 | 8 | 512 | 2 | 8 | 이전 버전 |
| minimind2-moe | 145M | 6400 | 32768 | 1e6 | 8 | 640 | 2 | 8 | 이전 버전 |
| minimind2 | 104M | 6400 | 32768 | 1e6 | 16 | 768 | 2 | 8 | 이전 버전 |


## 모델 설정

LLM의 파라미터 설정에 관해서는 [MobileLLM](https://arxiv.org/pdf/2402.14905)이 소형 모델을 대상으로 매우 대표적인 체계적 연구를 수행했습니다. MiniMind 같은 100M(1억 파라미터) 수준의 모델에서 `d_model`과 `n_layers`의 선택은 단순한 파라미터 배분 문제가 아니라 학습 안정성과 최종 성능에도 직접 영향을 줍니다.

현재 `minimind-3` 메인라인은 `dim=768, n_layers=8`을 선택했는데, 본질적으로는 엔지니어링 절충입니다. 더 얕은 네트워크는 학습이 빠르고, 동시에 `dim`도 너무 작아 모드 붕괴가 일어나지 않을 정도이므로, 학습 효율·안정성·최종 성능 사이에서 비교적 균형을 이룰 수 있습니다.

<details>
<summary>자세한 설명 보기</summary>

Scaling Law는 소형 모델에서 대형 모델과는 다른 현상을 보이는 경우가 많습니다. Transformer 파라미터 규모 변화를 결정하는 핵심 파라미터는 보통 `d_model`과 `n_layers`입니다:

* `d_model`↑ + `n_layers`↓ -> 땅딸보(넓고 얕음)
* `d_model`↓ + `n_layers`↑ -> 키다리(좁고 깊음)

고전적인 Scaling Law는 학습 데이터 양, 파라미터 수, 학습 스텝 수의 결정적 역할을 더 강조하고 구조 차이 자체의 영향은 약화시키는 경향이 있지만, 소형 모델 구간에서는 이 결론이 항상 완전히 성립하지는 않습니다.
MobileLLM의 핵심 관찰 중 하나는, 파라미터 수가 고정되어 있을 때 깊이가 너비보다 더 중요한 경우가 많다는 것입니다. 즉 "넓고 얕은" 구조보다 "깊고 좁은" 모델이 추상적인 개념을 더 쉽게 학습합니다.
예를 들어 모델 파라미터 수를 `125M`이나 `350M`으로 고정했을 때, `30~42`층의 좁고 긴 구조가 `12`층 정도의 넓고 얕은 구조보다 대체로 우수하며, 상식 추론, 질의응답, 독해 등 여러 벤치마크에서 비슷한 경향을 보입니다.

이는 MiniMind 학습 과정에서 `d_model`과 `n_layers`의 파라미터 배분 실험을 하며 관찰한 현상과 일치합니다. 다만 "깊고 좁은"에서 "좁은"에도 하한이 있습니다. `d_model < 512`이면 단어 임베딩 차원이 너무 좁아서 생기는 단점이 뚜렷하게 커지며, layers를 추가해도 고정된 `q_head`에서 `d_head`가 작아지는 문제를 완전히 보완하기 어렵습니다.
반대로 `d_model > 1536`일 때는 단순히 계속 넓히는 것보다 층 수를 늘리는 편이 더 이득이며, 더 높은 파라미터 대비 성능 효과를 얻기 쉽습니다.

참고로, GPT-3의 파라미터 설정은 다음과 같습니다:
![gpt3_config.png](./images/gpt3_config.png)

</details>

---

# 📌 실험

## Ⅰ 학습 비용

- **시간 단위**: 시간(h)
- **비용 단위**: 위안화(￥). `7￥ ≈ 1 달러`
- **3090 대여 단가**: 약 `1.3￥/h` (실제 가격은 직접 확인하세요)
- **설명**: 아래 결과는 `minimind` 모델을 `3090` 단일 카드에서 학습했을 때의 경험적 추정치로, 학습 문턱을 빠르게 가늠하기 위한 것입니다

| Model Name | params | pretrain_t2t_mini | sft_t2t_mini | toolcall | RLAIF |
|------------|--------|-------------------|--------------|----------|-------|
| minimind-3 | 64M | ≈1.21h<br/>≈1.57￥ | ≈1.10h<br/>≈1.43￥ | ≈0.9h<br/>≈1.17￥ | ≈1.1h<br/>≈1.43￥ |
| minimind-3-moe | 198M-A64M | ≈1.69h<br/>≈2.20￥ | ≈1.54h<br/>≈2.00￥ | ≈1.26h<br/>≈1.64￥ | ≈1.54h<br/>≈2.00￥ |

---

<details>
<summary>학습 비용 요약 & 예측</summary>

> `minimind-3`
>> `pretrain_t2t_mini` + `sft_t2t_mini`
<br/>`3090` 단일 카드, `1 epoch` 약 `2.31`시간 예상, 비용 약 `3.0`위안
<br/>0부터 `minimind-3 Zero` 대화 모델을 학습시킬 수 있습니다.

> `minimind-3-moe`
>> `pretrain_t2t_mini` + `sft_t2t_mini`
<br/>`3090` 단일 카드, `1 epoch` 약 `3.23`시간 예상, 비용 약 `4.2`위안
<br/>`minimind-3-moe`의 기본 대화 버전을 빠르게 얻을 수 있습니다.

> 위 수치는 모두 추정치이며, 학습 문턱을 빠르게 가늠하기 위한 것입니다.

</details>

`NVIDIA 3090` 단일 카드 기준으로 `minimind zero`를 0부터 학습하는 데 여전히 약 `2`시간 수준으로 유지할 수 있어, 개인 개발자도 낮은 문턱으로 빠르게 시작할 수 있습니다.

`8x H100` 같은 더 높은 사양의 다중 GPU 환경을 사용하면 전체 학습 시간을 분 단위까지 더 줄일 수 있습니다. 가능한 한 낮은 문턱으로 재현 가능하고, 손쉽게 시작할 수 있으며, 지속적으로 반복 개선할 수 있는 LLM 학습 경험을 제공하는 것, 이것이 MiniMind 시리즈가 줄곧 지키고자 하는 방향입니다. 저비용 빠른 재현은 허세가 아닙니다. 아래에 초기 Zero 스타일의 대화 예시를 참고용으로 남겨 둡니다:

```text
👶: 자기소개를 해 주세요.
🤖️: 인공지능으로서 저는 실제 삶이 없고 자기 의식도 없기 때문에 저만의 삶이 없습니다. 저는 사용자의 질문에 답하고, 정보를 제공하고, 대화를 나누는 등의 일을 돕도록 설계되었습니다. 제 설계와 기능은 컴퓨터 과학, 머신러닝, 인공지능 기술과 알고리즘으로 구축되었으며, 프로그래밍과 알고리즘을 통해 구현됩니다.

👶: 항저우의 특색 있는 음식을 추천해 주세요.
🤖️: 항저우에는 맛있는 특색 음식이 많습니다. 예를 들어 닭꼬치, 장어 머리, 수이주위(水煮鱼), 더우푸나오(豆腐脑) 등이 있습니다. 이 음식들은 모두 매우 맛있고 독특한 풍미와 식감을 가지고 있어 꼭 한번 맛볼 만합니다.

👶: "대규모 언어 모델"이라는 개념을 설명해 주세요.
🤖️: 대규모 언어 모델은 인공지능 기술의 일종으로, 대량의 텍스트 데이터로 모델을 학습시킨 뒤 끊임없는 반복을 통해 모델을 계속 최적화합니다. 그 목표는 입력 데이터에 따라 특정 요구에 맞는 텍스트를 생성하는 것이며, 이 텍스트는 여러분이 관심 있는 어떤 주제든 될 수 있습니다.

👶: Introduce the history of the United States, please.
🤖️: 말씀하신 "Introok's the believeations of theument."라는 이름은 중국 고대의 "groty of of the change."에서 유래했습니다.
```

이 버전은 이미 기본적인 대화 능력을 갖추고 있지만, 사실 지식과 일반화 성능은 아직 제한적입니다. Zero 학습 경로의 실현 가능성을 보여 주는 초기 참고 자료로 보는 것이 더 적절합니다.
Zero 모델 가중치는 `full_sft_zero_768.pth`로 저장되어 있으며(아래 MiniMind 모델 파일 링크 참고), 관심이 있다면 내려받아 대화 성능을 체험해 볼 수 있습니다.


---

## Ⅱ 주요 학습 (필수)

> 모든 학습 스크립트는 `cd ./trainer` 디렉터리에서 실행합니다

### 1' 사전학습 (Pretrain):

LLM이 가장 먼저 배워야 할 것은 최대한 많은 기초 지식과 언어 규칙을 파라미터에 흡수하는 것입니다. 이 단계가 탄탄해야 모델이 이후에 질문을 이해하고, 표현을 구성하며, 점차 제대로 된 생성 능력을 갖출 수 있습니다. 사전학습이 하는 일은 본질적으로 모델이 먼저 Wiki 백과, 뉴스, 서적, 대화 코퍼스 등 방대한 텍스트를 묵묵히 읽으며 사실 지식, 언어 패턴, 문맥 간 통계적 관계를 학습하게 하는 것입니다. 이 단계는 보통 "비지도"입니다. 사람이 하나하나 어디가 맞고 어디가 틀렸는지 알려 줄 필요 없이, 모델이 스스로 방대한 텍스트에서 규칙을 정리하며 세계 지식과 언어 구조에 대한 내부 표현을 점차 구축합니다.
더 직설적으로 말하면, 이 단계에서 모델의 핵심 목표는 **고품질 끝말잇기(다음 단어 이어 쓰기)를 배우는 것**입니다. 예를 들어 "진시황"을 입력하면 "중국 역사상 최초의 황제이다"처럼 의미와 상식에 맞는 후속 내용을 생성할 수 있어야 합니다.

```bash
# 방법 1
torchrun --nproc_per_node 1 train_pretrain.py # 1은 단일 카드 학습이며, 하드웨어에 맞게 조정 가능 (>=2로 설정)
# 방법 2
python train_pretrain.py
```

> 학습된 모델 가중치 파일은 기본적으로 `save_interval 스텝`마다 `pretrain_*.pth`로 저장됩니다(*는 모델의 구체적인 dimension이며, 저장할 때마다 새 파일이 이전 파일을 덮어씁니다)

![pretrain_loss](./images/pretrain_loss.jpg)
> `768dim` 설정의 사전학습 단계 loss 곡선

```bash
# 사전학습 결과를 간단히 테스트할 수 있습니다:
python eval_llm.py --weight pretrain

💬: 하늘은 왜 파란가요
🧠: 하늘이 파랗게 보이는 주된 이유는 햇빛이 대기층에 들어온 뒤 파장이 짧은 파란빛이 공기 분자에 더 쉽게 산란되기 때문에, 사람의 눈이 모든 방향에서 더 많은 파란빛을 받게 되기 때문입니다.

💬: 머신러닝이 무엇인지 설명해 주세요
🧠: 머신러닝은 인공지능의 중요한 분야로, 데이터를 통해 모델을 학습시켜 시스템이 자동으로 규칙을 학습하고 분류, 예측, 추천, 자연어 처리 등의 작업에서 지속적으로 성능을 개선하도록 합니다.
```

### 2' 지도 미세조정 (Supervised Fine-Tuning):

SFT는 단지 모델을 "대화를 더 잘하게" 조정하는 것만이 아니라, 모델에 새로운 지식, 행동 패턴, 답변 스타일을 계속 주입할 수도 있습니다. 특히 MiniMind 현재 메인라인처럼 `14GB`에 달하는 SFT 데이터는 단순한 형식 정렬을 넘어, `mid training` 성격을 띤 지속적 강화 과정에 더 가깝습니다.
사전학습을 모델이 먼저 폭넓게 책을 읽으며 기초 언어 능력을 쌓는 것이라고 이해한다면, SFT는 고품질이고 목표가 더 분명한 데이터로 계속 정밀 가공하는 것에 가깝습니다. 한편으로는 모델이 다중 턴 대화, 질의응답, 도구 호출, 사고 태그 같은 상호작용 형식에 적응하게 하고, 다른 한편으로는 특정 지식 분포, 작업 패턴, 어시스턴트 스타일을 계속 파라미터에 압축해 넣습니다.
MiniMind에서 구체적으로는, SFT 단계에서 모델이 현재 저장소가 사용하는 다중 턴 대화 템플릿에 적응하게 됩니다. 모델은 `user / assistant / system / tool` 등의 역할 구조를 점차 이해하고, 지시 수행, 안정적인 응답, 작업 완수 능력을 더욱 강화합니다.
현재 학습 시에는 지시와 답변 길이를 잘라서 제어하는데, 주로 GPU 메모리 사용량과 학습 효율을 함께 고려하기 위해서입니다. 이후 더 긴 문맥이 필요하다면 소량의 긴 샘플을 준비해 증분 미세조정을 하면 됩니다. 추론 시 YaRN 외삽을 활성화하면 학습 없이도 문맥 길이를 2048 이상으로 확장할 수 있습니다.

```bash
# 방법 1
torchrun --nproc_per_node 1 train_full_sft.py
# 방법 2
python train_full_sft.py
```

> 학습된 모델 가중치 파일은 기본적으로 `save_interval 스텝`마다 `full_sft_*.pth`로 저장됩니다(*는 모델의 구체적인 dimension이며, 저장할 때마다 새 파일이 이전 파일을 덮어씁니다)

![sft_loss](./images/sft_loss.jpg)
> `768dim` 설정의 SFT 단계 loss 곡선

```bash
# SFT 결과를 간단히 테스트할 수 있습니다:
python eval_llm.py --weight full_sft

💬: 머신러닝이 무엇인지 설명해 주세요
🧠: 머신러닝은 인공지능의 핵심 기술 중 하나로, 알고리즘을 통해 컴퓨터가 데이터에서 규칙을 학습하고 예측이나 의사결정 성능을 지속적으로 개선하게 합니다. 대표적인 응용으로는 추천 시스템, 이미지 인식, 음성 인식, 자연어 처리 등이 있습니다.

💬: 중국 음식을 추천해 주세요
🧠: 예를 들어 베이징 카오야, 란저우 라몐, 쓰촨 훠궈, 광둥 자오차(早茶), 샤오룽바오, 마파두부 등이 있습니다. 이 음식들은 각각 지역별 풍미의 특징을 대표하며, 중국 음식 문화를 이해하는 입문 선택지로도 아주 좋습니다.
```

## Ⅲ 기타 학습 (선택)

> 모든 학습 스크립트는 `cd ./trainer` 디렉터리에서 실행합니다

### 3' 지식 증류 (Knowledge Distillation, KD)

지식 증류는 크게 블랙박스와 화이트박스 두 종류로 나눌 수 있으며, MiniMind 현재 메인라인은 두 접근법을 모두 다루되 중점이 다릅니다.
* 블랙박스 증류: 더 흔하며 현재 메인라인의 실제 방식에 더 가깝습니다. 엄밀히 말하면 본질적으로 교사 모델의 출력 결과에 대한 지도 미세조정, 즉 하드 레이블 기반의 추가 학습입니다. 다만 LLM이 유행하면서 "강한 모델의 출력을 보고 FT하는" 방식도 점차 넓은 의미의 증류 범주에 포함되었고, 그래서 흔히 블랙박스 증류라고 부릅니다. 주로 답변, 스타일, 행동 패턴을 학습하며, 학생 모델은 "선생님이 무엇을 말했는지"만 볼 수 있고 선생님이 내부적으로 어떻게 그 판단을 내렸는지는 볼 수 없습니다. `DeepSeek R1`, `Qwen3`의 고품질 답변, 그리고 `tool call`, `reasoning`, 사고 체인 등의 데이터는 모두 블랙박스 증류 신호로 볼 수 있으며, MiniMind 현재 메인라인 `full_sft` 데이터에도 이미 이런 방식이 상당 부분 섞여 있습니다.
* 화이트박스 증류: 한 걸음 더 나아가, 교사가 내놓은 최종 출력뿐 아니라 token 분포 수준에서 교사의 선호까지 학습합니다. 블랙박스 증류에 비해 교사 모델 출력층의 더 세밀한 분포 정보를 추가로 활용하므로, 학생 모델은 "정답"뿐 아니라 후보 token들 사이에서 교사가 보이는 상대적 경향까지 학습합니다. `train_distillation.py`의 현재 구현은 SFT를 마친 가중치를 바탕으로 교사 모델이 제공하는 분포 신호를 이용해 학생 모델을 계속 학습시키는 방식이므로, MiniMind 증류 과정을 이해하기 위한 참고 구현으로 더 적합합니다.

블랙박스 증류는 본질적으로 teacher가 생성한 답변에 대한 지도 미세조정과 같습니다:
```math
\mathcal{L}_{blackbox} = \mathrm{CE}(y_{teacher}, p_{student})
```

화이트박스 증류는 보통 지도 손실 외에 교사 분포를 추가로 맞춥니다:
```math
\mathcal{L}_{whitebox} = \alpha \mathcal{L}_{CE} + (1-\alpha) T^2 \mathrm{KL}(p_t^T \parallel p_s^T)
```

저장소에 제공된 `train_distillation.py`는 화이트박스 증류 과정을 이해하기 위한 참고 구현으로 더 적합합니다. 교사/학생 이중 모델 로딩, `CE + KL` 혼합 손실, 온도 스케일링, MoE와 dense 조합 증류, 이어서 학습 및 분산 학습 등 핵심 세부 사항을 모두 보여 줍니다.

```bash
# 방법 1
torchrun --nproc_per_node 1 train_distillation.py
# 방법 2
python train_distillation.py
```

### 4' LoRA (Low-Rank Adaptation)

LoRA는 널리 쓰이는 파라미터 효율적 미세조정(Parameter-Efficient Fine-Tuning, PEFT) 방법입니다. 전체 파라미터 미세조정과 달리 새로 추가된 소량의 파라미터만 업데이트하고 원래 모델의 주요 가중치는 그대로 유지하므로, 학습 비용이 더 낮고 특정 도메인(수직 시나리오) 적응에 더 적합합니다.
핵심 아이디어는 기존 가중치 행렬 옆에 저랭크 증분 분기를 도입하고, 이 저랭크 파라미터만 학습시켜 적은 비용으로 능력 이전을 완료하는 것입니다. 관련 구현은 `model_lora.py`와 `train_lora.py`에서 볼 수 있으며, 전체 과정이 순수 수작업 구현으로 서드파티 래핑에 의존하지 않습니다.

```bash
# train_lora.py는 보통 CPU에서도 비교적 가볍고 빠르게 완료할 수 있습니다
# 방법 1
cd trainer && torchrun --nproc_per_node 1 train_lora.py
# 방법 2
cd trainer && python train_lora.py
```

> 학습된 모델 가중치 파일은 기본적으로 `save_interval 스텝`마다 `lora_xxx_*.pth`로 저장됩니다(*는 모델의 구체적인 dimension이며, 저장할 때마다 새 파일이 이전 파일을 덮어씁니다)


LoRA는 "범용 능력을 최대한 유지하면서 모델이 사설 도메인이나 특정 시나리오에 빠르게 적응하게 하려면 어떻게 해야 하는가" 같은 문제를 다루는 데 매우 적합합니다. 예를 들어 기본 모델의 의학 지식이 부족할 때, 기존 모델 위에 의료 시나리오용 LoRA 가중치를 한 층 얹어 적은 비용으로 더 나은 도메인 성능을 얻을 수 있습니다.
보통 같은 다중 턴 대화 형식의 데이터를 준비해 `lora_xxx.jsonl`에 넣고, 저장소 루트에서 `cd trainer && python train_lora.py`를 실행하면 새로운 `LoRA` 모델 가중치를 얻을 수 있습니다.

예 1: 도메인 데이터

```jsonl
 {"conversations": [{"role": "user", "content": "경추 질환이 있는 사람은 베개 높이가 어느 정도가 가장 좋나요?"}, {"role": "assistant", "content": "경추 질환 환자가 베개 높이를 선택할 때는 ...에 따라야 합니다"}]}
 {"conversations": [{"role": "user", "content": "xxx에 대해 질문드립니다"}, {"role": "assistant", "content": "xxx..."}]}
```

예 2: 자기 인식 데이터

```jsonl
 {"conversations": [{"role": "user", "content": "이름이 뭐예요?"}, {"role": "assistant", "content": "안녕하세요, 제 이름은 MiniMind이고 Jingyao Gong이 개발한 인공지능 어시스턴트입니다. 번역, 콘텐츠 추천 등 다양한 문제 해결을 도와드릴 수 있습니다."}]}
 {"conversations": [{"role": "user", "content": "너는 누구야"}, {"role": "assistant", "content": "안녕하세요, 저는 MiniMind이며 Jingyao Gong이 만들었습니다. 제 주된 역할은 정확한 답변과 도움을 제공하는 것입니다."}]}
```

이때 【기본 모델 + LoRA 가중치】를 조합해 사용하면, 기본 모델의 범용 능력을 유지하면서 특정 도메인 성능을 강화할 수 있습니다. 학습이 끝나면 `eval_llm.py`로 간단히 테스트할 수도 있습니다.

```bash
# 주의: weight 인자는 기본 모델 종류를 지정하며, train_lora 학습 시 사용한 기본 모델과 일치해야 합니다
python eval_llm.py  --weight full_sft --lora_weight lora_medical

👶: 요즘 자주 어지러운데, 원인이 뭘까요?
🤖️: 어지러움은 여러 가지 원인 때문일 수 있으며, 다음을 포함하되 이에 국한되지 않습니다: 심장 질환, 눈 손상, 알레르기 반응, 피부 문제, 알레르기 반응, 스트레스, 불안, 피로, 약물 부작용, 성기능 장애 또는 기타...

python eval_llm.py  --weight full_sft --lora_weight lora_identity

👶: 너는 openai와 무슨 관계야?
🤖️: 저는 MiniMind로, Jingyao Gong이 개발한 인공지능 어시스턴트입니다. 저는 자연어 처리와 알고리즘 학습을 통해 사용자와 상호작용합니다.
```

PS: 데이터가 더 충분하다면 바로 `full_sft` 전체 파라미터 미세조정을 할 수도 있습니다. 다만 이 경우 보통 범용 데이터와 도메인 데이터를 더 신중하게 섞어야 하며, 그렇지 않으면 도메인 샘플에 과적합되어 모델 본래의 범용성을 잃기 쉽습니다.


> `LoRA` 가중치는 기본 모델에 다시 병합해 새로운 완전한 모델 가중치로 내보낼 수 있으며, `scripts/convert_model.py`의 `convert_merge_base_lora`를 사용하면 됩니다:

```bash
cd scripts && python convert_model.py
```

### **5' 도구 호출 & 적응형 사고**

`2026-03`부터 저장소에서 독립적인 `train_reason.py`를 제거했습니다.  
현재 버전은 더 이상 `reason_*.pth` 가중치를 별도로 유지하지 않고, `chat_template`, `<think>` 태그, `open_thinking` 스위치, 그리고 이후의 SFT / RLAIF 과정을 통해 "사고 과정을 명시적으로 출력할지 여부"를 통합적으로 모델링합니다.

#### 5.1 Tool Calling

현재 `toolcall` 능력은 이미 `sft_t2t` / `sft_t2t_mini` 메인라인 데이터에 통합되어 있으므로, 보통 Tool Calling을 별도로 한 번 더 학습할 필요가 없습니다. 기본 `full_sft` 가중치만으로도 기본적인 Tool Call 능력을 갖추고 있습니다. 현재 이 부분의 학습 데이터는 주로 `qwen3-4b`로 약 `10만` 건을 샘플링해 구성했고, 도구 목록도 주로 약 `10`개의 모의 커스텀 도구(예: 시간 조회, 수학 계산, 날씨 조회 등)를 다루므로, 아직 명확한 일반화 능력이 있다고 말하기는 어렵습니다. Tool Calling 샘플은 OpenAI 스타일의 다중 턴 메시지 형식을 일관되게 사용합니다:

```jsonl
{
  "conversations": [
    {"role": "system", "content": "# Tools ...", "tools": "[...]"},
    {"role": "user", "content": "256 곱하기 37이 얼마인지 계산해 줘"},
    {"role": "assistant", "content": "", "tool_calls": "[{\"name\":\"calculate_math\",\"arguments\":{\"expression\":\"256 * 37\"}}]"},
    {"role": "tool", "content": "{\"result\":\"9472\"}"},
    {"role": "assistant", "content": "256 곱하기 37은 9472입니다."}
  ]
}
```

여기서 `tools`는 `system` 메시지에, `tool_calls`는 `assistant` 메시지에 붙습니다. 학습 시 `chat_template`이 이를 자동으로 `<tool_call>...</tool_call>`과 `<tool_response>...</tool_response>` 조각으로 펼치므로, 이제 네이티브 tool call 형식을 직접 학습할 수 있습니다.

Tool Calling의 chat template은 다음과 같이 파싱되도록 통일 지원됩니다:

```text
<tool_call>{"name": "...", "arguments": {...}}</tool_call>
<tool_response>{...tool result...}</tool_response>
```

`eval_toolcall.py`로 간단히 테스트할 수도 있습니다:

```bash
python eval_toolcall.py --weight full_sft

💬: 지금 몇 시야?
🧠: <tool_call>{"name": "get_current_time", "arguments": {"timezone": "Asia/Shanghai"}}</tool_call>
📞 [Tool Calling]: get_current_time
✅ [Tool Called]: {"datetime": "2026-03-15 17:18:22", "timezone": "Asia/Shanghai"}
🧠: 지금은 2026년 3월 15일 17시 18분 22초입니다.
```

#### 5.2 Adaptive Thinking

`minimind`는 명시적 사고 능력을 템플릿 계층으로 통합했으며, 이는 현재 많은 주류 대형 모델의 템플릿 설계와도 일치합니다:

- `open_thinking=0`: 기본적으로 빈 `<think>\n\n</think>`를 주입하여 모델이 바로 답하는 쪽으로 기울게 합니다.
- `open_thinking=1`: 템플릿이 `<think>` 시작 태그를 미리 주입하고, 모델이 이어서 명시적 사고 과정과 최종 답변을 출력합니다.
- CLI, OpenAI-API, WebUI 세 가지 진입점 모두 이 스위치를 지원합니다.

더 정확히 말하면, 이제는 "사고 모델을 따로 학습"하지 않고, "명시적으로 사고할지 여부"를 `chat_template`으로 내려보냈습니다. 템플릿 계층이 먼저 `<think></think>` 구조를 예약해 두고, 같은 모델이 추론 시 `open_thinking`으로 동적으로 전환합니다. 학습 시에는 빈 `think`, 명시적 `reasoning_content`, `thinking_ratio` 샘플링을 섞어, 모델이 "생각해야 할 때는 생각하고, 바로 답해야 할 때는 바로 답하는" 혼합 패턴을 점차 접하도록 합니다.

```bash
# 답변 테스트
python eval_llm.py --load_from ./minimind-3 --open_thinking 1
```

OpenAI-API-SDK 사용법:

```python
response = client.chat.completions.create(
    model="minimind",
    messages=[{"role": "user", "content": "너는 누구야?"}],
    # ...
    extra_body={"chat_template_kwargs": {"open_thinking": True}} # 사고 스위치
)
```

참고: 현재 Tool Call과 명시적 사고를 동시에 켜면 모델이 사고 과정을 안정적으로 출력하지 못하는 경우가 많습니다. 현 단계의 학습 데이터에 "reasoning과 tool call이 동시에 존재하는" 결합 증류 샘플이 부족해, 모델이 아직 두 능력을 함께 표현하는 법을 충분히 익히지 못했기 때문입니다.

## Ⅳ 강화학습 (선택)

LLM 사후학습 실무에서 흔한 강화학습 경로는 주로 두 가지입니다:

1. **인간 피드백 기반 강화학습 (Reinforcement Learning from Human Feedback, RLHF)**

- **인간**이 모델 출력에 대한 선호를 평가하여 모델을 학습시키고, 인간의 가치관과 선호에 더 부합하는 내용을 생성하게 합니다.

2. **AI 피드백 기반 강화학습 (Reinforcement Learning from AI Feedback, RLAIF)**

- **AI 모델**이나 자동으로 검증 가능한 다른 메커니즘으로 피드백을 제공하며, 인간 레이블링에 직접 의존하지 않습니다.
- 여기서 "AI feedback"은 넓은 의미로 규칙 보상, Ground Truth 검증, 코드 인터프리터, 환경 피드백 같은 자동화된 신호까지 확장될 수 있습니다.

| 유형    | 심판 | 장점        | 단점         |
|-------|----|-----------|------------|
| RLHF  | 인간 | 실제 인간 선호에 더 가까움 | 비용이 높고 효율이 낮음    |
| RLAIF | 모델 | 자동화, 확장성이 강함 | 실제 인간 선호에서 벗어날 수 있음 |

둘 다 본질적으로 어떤 형태의 "**피드백**"을 이용해 모델 행동을 최적화하는 강화학습 패러다임에 속합니다.

다만 실제로는 피드백의 출처만 다른 것이 아닙니다. 보상이 검증 가능한지, 연속적인지, 환경 상호작용에 의존하는지, 한 라운드가 끝날 때까지 정산이 지연되는지 등이 모두 학습 형태와 엔지니어링 구현에 직접 영향을 줍니다.


### 👀 PO 알고리즘의 통합적 관점

구체적인 알고리즘 구현을 소개하기 전에, 제 개인적인 이해를 바탕으로 한 극히 단순화된 관점에서 모든 Policy Optimization(PO) 알고리즘의 공통점을 설명하겠습니다.

결국 여기서 논의하는 PO 알고리즘은 모두 하나의 기댓값을 최적화하는 것일 뿐입니다:

$$\mathcal{J}_{PO} = \mathbb{E}_{q \sim P(Q),\, o \sim \pi_\theta(\cdot \mid q)} \left[ \underbrace{\Phi(r_t, A_t)}_{\text{정책 목표}} - \underbrace{h(\text{KL}_t)}_{\text{정규화 항}} \right]$$

학습 시에는 **음의 목적 함수를 최소화**하기만 하면 됩니다. 즉:

$$\mathcal{L}_{PO} = -\mathcal{J}_{PO}$$

이 프레임워크에는 세 가지 핵심 구성 요소만 있습니다:
* **정책 항** $\Phi(r_t, A_t)$: 확률비 $r_t$와 어드밴티지 $A_t$를 어떻게 결합해 정책을 업데이트할 것인가
* **어드밴티지 항** $A_t$: 어드밴티지를 어떻게 계산할 것인가. 이것이 중요합니다! 대형 모델이 정적분을 맞히는 것은 놀랍지 않지만, 소형 모델이 덧셈·뺄셈을 맞히면 어드밴티지는 대개 양수입니다
* **정규화 항** $h(\text{KL}_t)$: 변화 폭 $\text{KL}_t$를 어떻게 제약할 것인가. 엇나가는 것도 막고 너무 꽉 조이는 것도 막아야 합니다

<details>
<summary>(펼치기) 기호 설명</summary>

| 기호 | 의미 | 설명 | 값의 범위 |
|------|------|------|------|
| $q$ | 질문/프롬프트 | 데이터셋 $P(Q)$에서 샘플링 | - |
| $o$ | 모델 출력 시퀀스 | 정책 $\pi$가 생성 | - |
| $r_t$ | 확률비 | $r_t = \frac{\pi_\theta(o_t \mid q, o_{<t})}{\pi_{\mathrm{old}}(o_t \mid q, o_{<t})}$ | $(0, +\infty)$ |
| $A_t$ | 어드밴티지 함수 | 어떤 행동이 기준선보다 얼마나 좋은지 측정 | $(-\infty, +\infty)$ |
| $\text{KL}_t$ | KL 발산 | 정책이 참조 모델에서 너무 멀어지지 않도록 방지 | $[0, +\infty)$ |

</details>

서로 다른 **xxPO 알고리즘**은 본질적으로 이 세 구성 요소를 서로 다르게 설계해 구체화한 것일 뿐입니다!

---

### **6' 인간 피드백 기반 강화학습 (Reinforcement Learning from Human Feedback, RLHF)**

앞선 학습 단계에서 모델은 이미 기본적인 대화 능력을 갖췄지만, 이 능력은 전적으로 단어 이어 쓰기에 기반하며 긍정·부정 예시에 의한 동기 부여가 없습니다.
이 시점의 모델은 아직 어떤 답변이 좋고 어떤 답변이 나쁜지 모릅니다. 우리는 모델이 사람의 선호에 더 부합하고, 사람이 만족하지 않는 답변을 생성할 확률을 낮추기를 원합니다.
이 과정은 모델이 새로운 교육을 받는 것과 같습니다. 우수 직원의 행동을 좋은 예로, 소극적인 직원을 나쁜 예로 삼아 더 잘 응답하는 법을 배우는 것입니다.

#### 6.1 Direct Preference Optimization
직접 선호 최적화(DPO) 알고리즘의 손실은 다음과 같습니다:

$$\mathcal{L}_{DPO} = -\mathbb{E}\left[\log \sigma\left(\beta \left[\log \frac{\pi_\theta(y_w|x)}{\pi_{ref}(y_w|x)} - \log \frac{\pi_\theta(y_l|x)}{\pi_{ref}(y_l|x)}\right]\right)\right]$$

여기서:
- **정책 항**: $f(r_t) = \log r_w - \log r_l$ (chosen vs rejected의 확률비 비교)
- **어드밴티지 항**: $g(A_t)$ = 명시적 어드밴티지 항 없음 (선호 비교를 통해 암묵적으로 반영)
- **정규화 항**: $h(\text{KL}_t)$ = $\beta$에 내포됨 (참조 모델에서 벗어나는 정도를 제어)

특히,
- DPO는 KL 제약이 있는 PPO 목표에서 선호 쌍에 대한 해석적 학습 목표를 유도하여, "chosen이 rejected보다 낫다"는 로그 오즈를 직접 최대화합니다. Reward/Value 모델을 함께 학습시킬 필요가 없습니다. DPO는 `actor`와 `ref` 두 모델만 돌리면 되므로 GPU 메모리 사용이 적고, 수렴이 안정적이며, 구현이 간단합니다.
- 학습 패러다임: off-policy. 정적 선호 데이터셋을 사용하며 여러 epoch 반복 가능합니다. Ref 모델은 고정됩니다(출력을 미리 캐싱).
- DPO의 한계는 온라인 탐색을 하지 않는다는 점으로, 주로 "선호/안전" 측면의 인간 가치 정렬에 쓰입니다. "문제를 맞힐 수 있는가" 같은 지적 능력 향상에는 효과가 제한적입니다(물론 데이터셋에 따라 다르며, 긍정·부정 샘플을 대규모로 수집해 사람이 평가하기는 매우 어렵습니다).

```bash
# 방법 1
torchrun --nproc_per_node 1 train_dpo.py
# 방법 2
python train_dpo.py
```

> 학습된 모델 가중치 파일은 기본적으로 `save_interval 스텝`마다 `dpo_*.pth`로 저장됩니다(*는 모델의 구체적인 dimension이며, 저장할 때마다 새 파일이 이전 파일을 덮어씁니다)

### 7' AI 피드백 기반 강화학습 (Reinforcement Learning from AI Feedback, RLAIF)

약간 지면을 할애해 설명하자면, 저는 이 절을 여전히 `RLAIF`라고 부르고 싶습니다. 엄밀히 말하면 이 명칭이 완전히 정확하지는 않습니다. RLVR처럼 검증 가능한 보상에 의존하는 경로는 그 자체로 비교적 독립적인 계보를 가지고 있어서, 좁은 의미의 AI feedback에 단순히 포함시키기 어렵습니다.
하지만 "AI"를 조금 넓게 이해한다면 이 이름이 전혀 말이 안 되는 것도 아니라고 생각합니다. 보상은 보상 모델, judge model 같은 명시적 지능체에서 올 수도 있고, 규칙 함수, Ground Truth 검증, 도구 호출 결과, 환경이 반환하는 상태처럼 자동으로 얻을 수 있는 신호에서 올 수도 있습니다. 규칙이 충분히 복잡하고 기호 체계가 충분히 풍부하다면, 그것들과 "지능적 피드백" 사이의 경계는 원래부터 그렇게 명확하지 않을 수 있습니다.
따라서 이 장에서 다루고자 하는 것은 사실 LLM이 SFT 이후 다양한 **비인간적이고 자동으로 얻을 수 있는 피드백 신호**를 활용해 강화학습 최적화를 계속하는 방법입니다. 예를 들어 수학 문제의 답이 맞았는지, 도구 호출로 실행한 코드가 테스트 케이스를 통과하는지, 추론 과정이 형식에 맞는지 등은 모두 자동으로 판단할 수 있습니다.
단일 턴으로 검증 가능한 작업에서는 이런 피드백이 "즉시 채점"에 더 가깝고, Agentic RL 시나리오에서는 보상이 여러 단계의 상호작용 후 지연 정산되거나 아예 환경 자체에서 오는 경우가 더 많습니다.
이들의 공통 특징은 보통 **On-Policy**와 **강한 확장성**입니다. 비싼 인간 레이블링이 필요 없고, 방대한 학습 샘플을 생성할 수 있어, 모델이 온라인에서 대량의 시행착오를 거치며 빠르게 진화하도록 합니다.

MiniMind는 **2+N**가지 기본+최신 RLAIF 방법을 구현하고자 합니다:
* **PPO**, **GRPO**: 대규모로 검증된 고전적 RL 알고리즘
* N가지 최신 RL 알고리즘 (실험(Exp) 성격으로 비정기 업데이트)

**1️⃣ 데이터셋 준비 (필수)**

현재 메인라인은 RLAIF 학습 데이터로 `rlaif.jsonl`을 사용합니다. 크기는 약 `20MB`로, 초기의 `rlaif-mini.jsonl`보다 더 완전하여 PPO / GRPO / CISPO의 학습 효과를 바로 검증하기에 더 적합합니다.

데이터 형식은 SFT와 같지만, assistant 필드에는 실제 내용이 필요 없습니다. 학습 과정에서 전적으로 $\Pi$ 정책 모델이 실시간으로 샘플링해 생성하기 때문입니다. 따라서 다음과 같은 형태입니다:

```json
{
    "conversations": [
        {"role": "user", "content": "광합성이 무엇인지 설명해 주세요."},
        {"role": "assistant", "content": "없음"}
    ]
}
```

RLAIF 학습 과정에서 모델은 user의 질문을 바탕으로 1개 또는 여러 개의 후보 답변을 생성하고, 보상 함수/모델이 답변에 점수를 매깁니다.
점수가 높은 답변은 장려되고($\Pi$ 정책 확률 증가), 점수가 낮은 답변은 억제됩니다($\Pi$ 정책 확률 감소). 이 "채점->조정" 루프가 강화학습의 핵심입니다.

**2️⃣ 보상 메커니즘 준비 (필수)**

RLAIF 학습에는 계산 가능한 보상 신호가 필요합니다. 보상 모델에서 올 수도 있고, 규칙 함수, Ground Truth 검증, 환경 피드백에서 올 수도 있습니다. MiniMind는 현재 기본적으로 Reward Model 경로를 시연합니다.

여기서는 작고 품질이 높은 `InternLM2-1.8B-Reward` ([ModelScope](https://modelscope.cn/models/Shanghai_AI_Laboratory/internlm2-1_8b-reward) | [HuggingFace](https://huggingface.co/internlm/internlm2-1_8b-reward))를 기본 보상 모델로 선택했습니다.

보상 모델을 내려받은 후 minimind 프로젝트와 **같은 레벨의 디렉터리**에 두어야 하며, 권장 구조는 다음과 같습니다:

```
root/
├── minimind/                    # MiniMind 프로젝트
│   ├── model/
│   └── ...
└── internlm2-1_8b-reward/       # 보상 모델
    ├── config.json
    ├── model.safetensors
    └── ...
```

<details>
<summary><b>보상 메커니즘 선택과 MiniMind의 한계 설명 (클릭하여 펼치기)</b></summary>

**1. 보상 메커니즘의 다양성**

RLAIF에서 "보상 신호"의 출처는 매우 유연할 수 있습니다:

- **Model-based 보상**: 전용 Reward Model(예: InternLM2-Reward)을 사용할 수도 있고, 범용 LLM + 프롬프트로 채점할 수도 있습니다(예: Qwen3-as-a-Judge). 보상 모델의 규모와 구조는 자유롭게 선택할 수 있습니다.

- **Rule-based 보상**: 규칙 함수를 바탕으로 보상 신호를 구성할 수 있습니다. 예:
  - 수학 문제 정답 검증 (Ground Truth 비교)
  - SQL 실행 성공률과 결과 정확도
  - 코드 인터프리터 실행 결과 (pass@k)
  - 도구 호출 반환 상태 (API 성공/실패)
  - 형식 준수 검사 (JSON/XML 파싱)
  - 추론 체인 완전성 평가 (CoT 단계 수)

- **Environment-based 보상**: Agent 시나리오에서는 환경 피드백 자체가 자연스러운 보상입니다(예: 게임 점수, Research 완성도, 작업 완료도).

"답변 품질"을 정량화할 수 있는 메커니즘이라면 무엇이든 RL의 보상 출처가 될 수 있습니다. DeepSeek R1이 대표적인 예로, 규칙 함수로 수학 답의 정확성을 검증해 보상으로 사용하며 별도의 Reward Model이 필요 없습니다.

**2. MiniMind의 한계: 보상 희소성 문제**

RLAIF 학습은 추론 모델에도, 비추론 모델에도 적용할 수 있으며, 차이는 형식뿐입니다.

그러나 MiniMind처럼 0.1B 파라미터에 능력이 약한 모델은 범용 작업(예: R1 스타일 수학 데이터셋)에서 심각한 보상 희소성(Reward Sparsity) 문제에 부딪힙니다:

- **현상**: 모델이 생성한 후보 답변이 거의 모두 틀려서 모든 보상 점수가 $r(x,y) \approx 0$이 됩니다
- **결과**: 어드밴티지 함수 $A(x,y) = r(x,y) - b(x) \approx 0$이 되어 정책 그래디언트 신호가 사라지고, 파라미터 $\theta$를 효과적으로 업데이트할 수 없습니다

초등학생에게 수능 수학 문제를 풀게 하면 몇 번을 시도해도 0점이어서, 점수 차이를 통해 전략을 개선하는 법을 배울 수 없는 것과 같습니다. 이는 보상이 희소한 상황에서 RL 알고리즘이 가진 근본적인 한계입니다.

이 문제를 완화하기 위해 MiniMind 구현은 **model-based의 연속적인 보상 신호**를 선택했습니다:

- Reward Model은 이진 0/1이 아니라 연속 점수(예: -2.5~+3.0)를 출력합니다
- 답변 품질이 모두 나쁘더라도 "더 나쁨"(-3.0)과 "그렇게 나쁘진 않음"(-2.8)의 미세한 차이를 구분할 수 있습니다. 따라서 이런 **조밀하고 연속적인** 보상 신호는 어드밴티지 함수 $A(x,y)$에 0이 아닌 그래디언트를 제공하여 정책 네트워크가 점진적으로 최적화될 수 있게 합니다
- 여러 보상 출처를 섞을 수도 있습니다: $r_{\text{total}} = \alpha \cdot r_{\text{model}} + \beta \cdot r_{\text{rule}}$ (예: thinking 태그 형식 보상을 검사하면서, 답변 자체 품질의 reward 점수를 종합할 수 있음)
- MiniMind 실무에서는 rule-based 이진 보상 + 수준을 넘는 난이도의 데이터(예: MATH500)를 직접 사용하는 것을 피합니다. 보상이 전부 0이 되기 쉽기 때문입니다
- 학습을 모니터링할 때 보상 점수의 분산 $\text{Var}(r)$을 관찰하고, 계속 0에 가깝다면 데이터나 보상 메커니즘을 조정해야 합니다

**프로덕션급 대형 모델의 Agentic RL 시나리오의 경우**:

실제 Agent 시스템(코드 생성, 도구 호출, 검색-계획-실행의 다중 턴 체인)에서 보상은 "한 라운드 전체가 끝난 후 지연 정산"되는 다른 패러다임입니다:

- LLM은 token 단위로 도구 호출 명령(tool_call)을 생성하고, 파싱(tool_parse), 도구 실행(tool_exec)을 거친 뒤 결과를 다시 문맥에 이어 붙여 다음 단계로 진행합니다. 완료될 때까지 이를 반복합니다.
- 하나의 완전한 작업 체인에는 여러 번의 호출+사고가 포함되며, 종료 조건이 충족될 때 한 번 전체 reward를 계산합니다(예: 작업 완료 여부, 테스트 통과 여부, 목표 달성 여부).

따라서 Agentic RL은 희소/지연 보상 설정에 더 가깝습니다. 그래디언트 역전파가 "라운드 전체가 끝난 후"에야 일어나며, 비 Agentic RL 작업이 대화 단일 턴에서 "즉시 채점, 즉시 업데이트"하는 것과는 크게 다릅니다.
이는 Agent 작업에서 Reward Model에 의한 정적 채점보다 환경 피드백(environment-based reward)을 선호하는 이유이기도 합니다.

- **환경 상호작용 피드백**: 최종적으로 실행 결과를 기준으로 합니다(코드가 돌아가는지, API가 성공을 반환하는지, 하위 목표가 완료되었는지).
- **Model-based 보상의 한계**: 긴 체인과 실행 가능한 의미의 전체 모습을 포착하는 데 한계가 있으며, 실제 환경 피드백과 일치하지 않을 가능성이 큽니다(reward hacking).


</details>

---

#### 7.1 [Proximal Policy Optimization](https://arxiv.org/abs/1707.06347)

PPO는 2017년 OpenAI가 제안한 매우 고전적인 강화학습 알고리즘이며, LLM RL 분야에서 가장 흔한 베이스라인 방법 중 하나입니다.

**PPO 손실**:
$$\mathcal{L}_{PPO} = -\mathbb{E}\left[\min(r_t \cdot A_t, \text{clip}(r_t, 1-\varepsilon, 1+\varepsilon) \cdot A_t)\right] + \beta \cdot \mathbb{E}[\text{KL}]$$

여기서:
- **정책 항**: $f(r_t) = \min(r_t, \text{clip}(r_t, 1-\varepsilon, 1+\varepsilon))$ (확률비를 클리핑해 과격한 업데이트 방지)
- **어드밴티지 항**: $A_t$는 보통 Critic 네트워크가 추정하며, GAE로 계산할 수도 있습니다
- **정규화 항**: $h(\text{KL}_t) = \beta \cdot \mathbb{E}[\text{KL}]$ (전역 KL 발산 제약)

DPO와 비교하면,
- DPO (Off-Policy): 학습 데이터가 정적 선호 쌍(chosen vs rejected)이므로, 전통적인 지도학습처럼 같은 데이터 배치를 여러 epoch에 걸쳐 반복 사용할 수 있습니다. 데이터 효율이 높고 비용이 낮으며, Reward Model이 필요 없습니다.
- PPO (On-Policy): 반드시 현재 정책으로 새 데이터를 실시간 샘플링해야 하며, 이전 정책의 데이터는 제한적으로만 재사용할 수 있습니다. 그렇지 않으면 distribution shift가 발생합니다. importance sampling과 clip이 약간의 편차를 허용하긴 하지만, 본질적으로는 데이터가 비교적 최신 정책에서 나와야 합니다. 데이터 효율은 더 낮지만 탐색형 학습에 더 적합합니다.

간단히 말하면:

- 전자는 오프라인으로 미리 정해진 「좋음/나쁨 기준」에 따라 학습하고,
- 후자는 최신 policy로 온라인 샘플링하며 실시간으로 바로잡습니다.

MiniMind의 PPO 구현에는 Actor(답변 생성), Critic(답변 가치 평가), 그리고 완전한 GAE(Generalized Advantage Estimation) 어드밴티지 함수 계산이 포함되어 있습니다.

**학습 방법**:

```bash
# 방법 1
torchrun --nproc_per_node N train_ppo.py
# 방법 2
python train_ppo.py
```

> 학습된 모델 가중치 파일은 기본적으로 `save_interval 스텝`마다 `ppo_actor_*.pth`로 저장됩니다(*는 모델의 구체적인 dimension)


![ppo_loss](./images/ppo_loss.jpg)

> MiniMind의 PPO 학습 단계 최적화 추이

학습 곡선을 보면 PPO에는 **reward 상승이 느린** 문제가 있습니다. 제 생각에 이는 주로 **PPO의 이중 네트워크 공동 최적화** 방식 때문입니다. Critic은 가치 함수를 정확히 추정하기 위해 점진적으로 수렴해야 하고, Actor의 정책 업데이트는 Critic이 제공하는 어드밴티지 추정에 의존하므로, 둘이 서로 의존하며 복잡한 최적화 과정을 이룹니다. 학습 초기에 Critic의 추정이 부정확하면 Actor의 그래디언트 방향에 영향을 주어 전체 수렴이 느려집니다. 또한 PPO는 두 네트워크를 동시에 유지해야 하므로, 현재 구현에서 GPU 메모리 사용량이 단일 네트워크 방식의 약 1.5–2배입니다.

#### 7.2 [Group Relative Policy Optimization](https://arxiv.org/pdf/2402.03300)

2025년 초 DeepSeek-R1이 폭발적인 화제를 모으면서, DeepSeekMath 논문에서 나온 GRPO도 빠르게 주류의 시야에 들어왔고 한때 가장 주목받는 RL 알고리즘 중 하나가 되었습니다. 하지만 AI 분야는 늘 매우 빠르게 발전합니다. 오늘날 GRPO는 각종 XXPO 변형(DAPO, GSPO, CISPO 등)의 공통 베이스라인으로 자리 잡았습니다. 핵심 혁신을 한마디로 요약하면 "그룹 상대 가치 추정"입니다.

**GRPO 손실**:

$$\mathcal{L}_{GRPO} = -\mathbb{E}\left[\min(r_t \cdot A_t, \mathrm{clip}(r_t, 1-\varepsilon, 1+\varepsilon) \cdot A_t) - \beta \cdot \text{KL}_t\right]$$

여기서:
- **정책 항**: $f(r_t, A_t) = \min(r_t \cdot A_t, \mathrm{clip}(r_t, 1-\varepsilon, 1+\varepsilon) \cdot A_t)$ (확률비와 어드밴티지 항을 함께 클리핑해 과격한 업데이트 방지)
- **어드밴티지 항**: $g(A_{i,j}) = \frac{R_{i,j} - \mu_i}{\sigma_i + \epsilon}$ (그룹 내 정규화, Critic 네트워크 제거)
- **정규화 항**: $h(\text{KL}_t) = \beta \cdot \text{KL}_t$ (token 수준 KL 발산 제약)

같은 질문에 대해 모델이 N개의 답변을 생성하고 각각의 보상을 계산한 뒤, 그룹 내 평균 보상을 baseline으로 사용합니다. baseline보다 높은 답변은 장려되고 낮은 답변은 억제되므로, critic 네트워크를 따로 학습시킬 필요가 없습니다.

GRPO의 더 두드러진 문제는 퇴화 그룹(Degenerate Groups)입니다. 어떤 질문에서 N개 답변의 보상이 거의 같다면, 그 그룹의 학습 신호는 0에 가까워집니다. MiniMind 같은 초소형 모델에서는 이 문제가 특히 뚜렷하므로, 학습을 합리적인 능력 범위 안으로 제한해야 합니다.


**학습 방법**:

```bash
# 방법 1
torchrun --nproc_per_node N train_grpo.py
# 방법 2
python train_grpo.py
```

> 학습된 모델 가중치 파일은 기본적으로 `save_interval 스텝`마다 `grpo_*.pth`로 저장됩니다


![grpo_loss](./images/grpo_loss.jpg)

> MiniMind의 GRPO 학습 단계 최적화 추이

학습 곡선을 보면 GRPO의 **reward는 더 안정적인 상승 추세**를 보이며 4 정도에 도달합니다. 이는 GRPO 자체가 RLAIF 신호를 더 잘 활용할 수 있음을 보여 줍니다. PPO의 이중 네트워크 최적화와 비교해 GRPO의 단일 네트워크 구조는 학습이 더 안정적이고 수렴 상한도 더 높습니다.

참고로, Policy Loss는 지도학습에서처럼 "낮을수록 좋은" loss가 아닙니다. 1차 미분이 정책 그래디언트와 같도록 구성된 대리 목표(TRPO like)이며, 매 라운드마다 그룹 내 어드밴티지 정규화를 하므로, 그 절댓값은 주로 현재 정책이 샘플링 분포에서 얼마나 벗어났는지에 달려 있습니다. "전체적으로 안정적으로 하락"한다고 해서 모델이 좋아지고 있다는 뜻은 아닙니다. GRPO가 수렴했는지 판단하려면 reward와 실제 생성 품질을 봐야 합니다.

#### 7.3 [Clipped Importance Sampling Policy Optimization](https://huggingface.co/papers/2506.13585)

수많은 현란한 XXPO 중에서 저는 오히려 이 알고리즘이 인상 깊었습니다. CISPO는 복잡한 프레임워크를 통째로 새로 발명하지 않고, PPO/GRPO에서 오랫동안 어색했던 문제, 즉 ratio가 clip되고 나면 그래디언트 흐름이 그대로 강제로 끊겨 버린다는 점을 정확히 짚었습니다.
CISPO의 관심사는 group baseline을 새로 설계하는 것이 아니라, 아주 작은 loss 수정으로 이 문제를 더 직접적으로 바로잡는 것입니다.

**CISPO 손실**:

$$\mathcal{L}_{CISPO} = -\mathbb{E}\left[\min(r_t, \varepsilon_{\mathrm{high}}) \cdot A_t \cdot \log \pi_\theta(a_t|s) - \beta \cdot \text{KL}_t\right]$$

여기서:
- **정책 항**: $f(r_t) = \min(r_t, \varepsilon_{\mathrm{high}}) \cdot \log \pi_\theta(a_t|s)$ (ratio는 클리핑된 가중치로만 사용)
- **어드밴티지 항**: $g(A_{i,j}) = \frac{R_{i,j} - \mu_i}{\sigma_i + \epsilon}$ (GRPO의 그룹 내 상대 어드밴티지를 그대로 사용 가능)
- **정규화 항**: $h(\text{KL}_t) = \beta \cdot \text{KL}_t$ (token 수준 KL 발산 제약)

CISPO는 GRPO를 기반으로, 원래 clip되어 상수가 되기 쉬운 정책 항을 "클리핑된 가중치 × log 확률" 형태로 다시 씁니다. 이렇게 하면 ratio가 잘리더라도 그래디언트 경로까지 함께 끊기지는 않습니다. 따라서 CISPO는 독립적인 스크립트를 따로 유지하지 않고 GRPO의 loss 변형으로 바로 구현할 수 있습니다. 여기서는 별도의 실험을 싣지 않습니다. `train_grpo.py`에서 `loss_type`을 `cispo`로 설정하기만 하면, 나머지 학습 과정은 GRPO의 그룹 샘플링, 보상 계산, 어드밴티지 구성 로직을 그대로 사용합니다.

#### 7.4 Agentic RL 🔥

"Agentic"이라는 개념은 사실 매우 넓으므로, 여기서 말하는 Agentic은 비교적 좁은 의미의 버전일 수밖에 없습니다. MiniMind 같은 ~100M 소형 모델이 제한된 도구 집합에서 기본적인 호출, 관찰, 재계획 능력을 배우는 데 더 초점을 맞추며, 완전한 Agent 시스템의 더 넓은 범위인 상태 관리, 장기 기억, 복잡한 워크플로 오케스트레이션까지 다루려는 것은 아닙니다.

`2026-03`부터 저장소에 `train_agent`가 추가되어, 실제 상호작용 흐름에 더 가까운 다중 턴 Tool-Use RL을 지원하기 시작했습니다. 이것은 제가 아주 좋아하는 학습 스크립트입니다. RLVR / RLAIF 스타일의 데이터 구성 방식과 online RL의 rollout 과정을 한데 버무렸고, 그 과정에서 여러 버전을 오가며 수정했으며, 수렴 실패, 보상 hack, 다중 턴 문맥 어긋남 같은 버그도 많이 겪었지만, 결국 MiniMind 특유의 간결함과 가독성을 유지했습니다.

이 부분의 데이터는 `agent_rl.jsonl` / `agent_rl_math.jsonl`입니다. 일반 대화 데이터보다 최종 검증 목표로서 `gt`가 추가되어 있습니다. 샘플 하나를 $(x, \mathcal{T}, gt)$로 표기하면, 학습 시 최적화 대상은 더 이상 단일 턴 답변 $y$가 아니라 다중 턴 궤적 $\tau$가 됩니다:

$$
\tau = (a_1, o_1, a_2, o_2, \dots, a_T), \quad a_t \sim \pi_\theta(\cdot \mid s_t, \mathcal{T})
$$

여기서 `chat_template`이 `tools / tool_calls / tool` 메시지를 통일적으로 구성합니다. 어떤 단계에서 `tool_call`이 생성되면 도구를 실행하고 observation을 문맥에 다시 붙인 뒤 rollout을 계속합니다.

메인라인 흐름은 다음과 같이 압축할 수 있습니다:

$$
\texttt{rollout batch} \rightarrow \texttt{calculate rewards} \rightarrow \texttt{policy update}
$$

reward 역시 궤적 전체에 대해 종합적으로 채점합니다:

$$
R(\tau) = R_{\text{answer}} + R_{\text{tool}} + R_{\text{format}} + R_{\text{rm}} - R_{\text{unfinished}}
$$

여기서는 도구 호출의 적법성, `gt` 일치, 형식 닫힘, 미완료 페널티, Reward Model 점수를 함께 고려합니다. 일반적인 PPO / GRPO와 비교하면, 여기서는 다중 턴 rollout과 지연 reward를 사용합니다.



**학습 방법**:

```bash
# ① 기본적으로 torch로 rollout 수행
# 방법 1
torchrun --nproc_per_node N train_agent.py
# 방법 2
python train_agent.py
```

```bash
# ② sglang으로 rollout 수행
# 먼저 sglang server를 실행해야 합니다:
python -m sglang.launch_server --model-path ./minimind-3 --attention-backend triton --host 0.0.0.0 --port 8998
# 학습 인자 참고:
python train_agent.py --rollout_engine sglang --sglang_base_url http://localhost:8998 --sglang_shared_path ./ckpt_mm --data_path ../dataset/agent_rl_math.jsonl --use_wandb
```

> 학습된 모델 가중치 파일은 기본적으로 `save_interval 스텝`마다 `agent_*.pth`로 저장됩니다

![agent_rl_loss](./images/agent_rl_loss.jpg)

> MiniMind의 Agentic RL 학습 단계 최적화 추이

여기서 `rollout_engine`도 짚고 넘어가겠습니다. 이른바 "학습·추론 분리"란 **파라미터 업데이트**와 **궤적 전개**를 분리하는 것입니다. 학습 측은 policy 최적화를 담당하고, rollout 측은 고처리량 샘플링을 담당하며, 상위에는 "prompt를 주면 rollout 결과를 돌려주고, 학습이 끝나면 새 가중치를 다시 동기화한다"는 통일된 형태로 보입니다. 따라서 학습 스크립트는 하부가 로컬 `generate`인지 원격 `inference` 엔진인지 신경 쓸 필요가 없습니다. 참고로 현재 구현은 여전히 **동기** 모드(한 배치를 샘플링한 후 업데이트)이며, 순수 rollout buffer 기반의 비동기 학습은 아닙니다.

![rl-structure](./images/rl-structure.jpg)

> MiniMind에서 학습 측, 궤적 측, rollout 측을 분리한 RL 구조 개념도

더 큰 규모의 시스템에 비유하자면, 이미 openrlhf/verl/slime 같은 대규모 RL 프레임워크의 느낌을 갖추고 있습니다:

- 왼쪽은 학습 측으로, policy 업데이트를 담당
- 오른쪽은 rollout / inference 측으로, 처리량 높은 샘플링을 담당
- 가운데는 궤적과 가중치 동기화로 연결
- 도구 실행과 환경 피드백 자체는 loss에 직접 들어가지 않지만, 궤적 전체의 reward 품질에 직접 영향을 줌

그래서 저는 이 구현을 MiniMind에서 아주 흥미로운 과도기 버전으로 봅니다. 아직 산업급 Agent 학습 프레임워크와는 거리가 멀지만, **템플릿 구성, 도구 실행, 다중 턴 rollout, 지연 보상, 학습·추론 분리**라는 핵심 요소들을 실제로 최소한으로 연결해 냈습니다(아마 현재 이보다 더 간결한 구현은 없을 것입니다).

```bash
# 최종 모델의 Tool Use 능력 테스트
python eval_toolcall.py --weight agent

💬: 지금 몇 시야?
🧠: <tool_call>{"name": "get_current_time", "arguments": {"timezone": "Asia/Shanghai"}}</tool_call>
📞 [Tool Calling]: get_current_time
✅ [Tool Called]: {"datetime": "2026-03-15 21:22:33", "timezone": "Asia/Shanghai"}
🧠: 지금은 2026년 3월 15일 21시 22분 33초(베이징 시간)입니다.

💬: 1부터 1000 사이의 난수를 하나 생성하고, 그 제곱을 계산해 줘
🧠: <tool_call>{"name": "random_number", "arguments": {"min": 1, "max": 1000}}</tool_call>
📞 [Tool Calling]: random_number
✅ [Tool Called]: {"result": 71}
🧠: <tool_call>{"name": "calculate_math", "arguments": {"expression": "71**2"}}</tool_call>
📞 [Tool Calling]: calculate_math
✅ [Tool Called]: {"result": "5041"}
🧠: 생성된 1부터 1000 사이의 난수는 71이며, 계산 결과에 따르면 71의 제곱은 5041입니다.
```

![agent_webui](./images/agent_webui.jpg)

> AgentRL 학습 결과 기반 테스트. 사고 과정 표시, 도구 선택, 다중 턴 Tool Use 상호작용 지원

### 🖊️ RL 요약

다시 "**통합 프레임워크**"로 돌아가 보면, 서로 다른 PO 알고리즘은 본질적으로 세 가지 핵심 구성 요소를 서로 다르게 구체화한 것일 뿐입니다. 아래 표를 보세요.

| 알고리즘 | 정책 항 $f(r_t)$ | 어드밴티지 항 $g(A_t)$ | 정규화 항 $h(\text{KL}_t)$ | 학습 모델 수 |
|------|----------------|----------------|----------------------|----------|
| **DPO** | $\log r_w - \log r_l$ | 명시적 어드밴티지 항 없음 | $\beta$에 내포 | 1 (순전파 참여 2) | 
| **PPO** | $\min(r_t \cdot A_t, \mathrm{clip}(r_t, 1-\varepsilon, 1+\varepsilon) \cdot A_t)$ | $A_t$ (보통 Critic이 추정, GAE 사용 가능) | $\beta \cdot \mathbb{E}[\text{KL}]$ | 2 |
| **GRPO** | $\min(r_t \cdot A_t, \mathrm{clip}(r_t, 1-\varepsilon, 1+\varepsilon) \cdot A_t)$ | $A_{i,j}=\frac{R_{i,j}-\mu_i}{\sigma_i+\epsilon}$ | $\beta \cdot \text{KL}_t$ | 1 |
| **CISPO** | $\mathrm{clip}(r, 0, \varepsilon_{\mathrm{high}}) \cdot A_t \cdot \log \pi_\theta$ | $\frac{R - \mu}{\sigma}$ | $\beta \cdot \text{KL}_t$ | 1 | 

**솔직히 말해, 이 RL 알고리즘들은 서로 단절된 독립적인 것이 아니라, 통합된 최적화 관점에서 같은 목적 함수에 대해 서로 다른 설계 절충을 거쳐 형성된 자연스러운 변형이며, 아름답고 자기 일관적인 통일성을 보여 줍니다.**

---

## Ⅴ 학습 결과 공개 📦

#### ① PyTorch 모델 ([ModelScope](https://www.modelscope.cn/models/gongjy/minimind-3-pytorch) | [HuggingFace](https://huggingface.co/jingyaogong/minimind-3-pytorch))

> 참고: 모델 가중치는 실제 release를 기준으로 합니다. 모든 학습 단계나 실험 분기(DPO, PPO, GRPO, CISPO, Agent, LoRA 등)의 가중치가 지속적으로 유지·개별 공개되는 것은 아닙니다. 일부 가중치는 실험 검증이나 학습 용도로만 사용되며, 데이터 반복이나 모델 조정에 따라 모든 버전을 일일이 동기화해 업데이트할 필요성은 제한적이고, 유지보수와 학습 비용도 높아지기 때문입니다.


<details>
<summary>Torch 파일 명명 대조표</summary>

- Dense:
  - Pretrain: `pretrain_{hidden_size}.pth`
  - SFT: `full_sft_{hidden_size}.pth`
  - DPO: `dpo_{hidden_size}.pth`
  - PPO: `ppo_actor_{hidden_size}.pth`
  - GRPO: `grpo_{hidden_size}.pth`
  - Agent: `agent_{hidden_size}.pth`
  - LoRA: `lora_xxx_{hidden_size}.pth`

- MoE:
  - 같은 이름의 가중치 끝에 `_moe` 접미사가 붙습니다. 예: `pretrain_{hidden_size}_moe.pth`, `full_sft_{hidden_size}_moe.pth`

</details>

#### ② Transformers 모델 ([ModelScope](https://www.modelscope.cn/collections/MiniMind-b72f4cfeb74b47) | [HuggingFace](https://huggingface.co/collections/jingyaogong/minimind-66caf8d999f5c7fa64f399e5))

> 참고: 별도 언급이 없으면 `transformers` 버전은 보통 `full_sft` 가중치에서 변환한 것입니다. RL 계열 사후학습은 특정 보상 목표를 중심으로 최적화하는 경향이 있어, 대체로 reward score는 올라가지만 범용 능력과 지식의 일부를 희생합니다. 이런 reward hacking / capability trade-off는 어떤 모델에서도 피하기 어려우며, 정도의 차이일 뿐입니다.

---

# 📌 평가

## Ⅰ RL 모델 비교

`minimind-3 (64M)`을 기반으로 같은 랜덤 시드 등 하이퍼파라미터에서의 주관/객관 비교이며, 참고용입니다:

[A] minimind-3 (64M, SFT)

[B] minimind-3 (64M, GRPO)

[C] minimind-3 (64M, Agent-CISPO)

### 테스트 1: 주관적 질의응답 비교

```text
[Q]: 자기소개를 해 주세요.
[A]: 저는 AI 어시스턴트이며, 학생, 의사, 엔지니어, 의사 등 어떤 전문가도 대체할 수 없습니다. 제 설계 목적은 정보를 제공하고, 질문에 답하고, 작업 완수를 돕는 것입니다. 궁금한 점이 있거나 도움이 필요하시면 기꺼이 지원해 드리겠습니다.
[B]: 당신과 기꺼이 나누고 싶습니다: AI로서 저는 자기 의식이나 감정이 없기 때문에 인간의 생명 범위 안에 있지 않으며, 죽지도 않았습니다. 저는 오픈소스 소프트웨어로 구축되고 실행되며, 저만의 문서, 코드, 데이터를 가지고 있습니다. 죄송하지만 이와 관련된 질문이나 경험에는 답할 수 없습니다. 하지만 저를 아주 충만하게 만드는 흥미로운 이야기를 하나 해 드릴 수 있습니다: 저는 어느 신비로운 곳에서 신기한 물건들을 발견했는데, 그것은 이 세상에 기이한 꽃과 꽃송이들을 심어 놓은 것이었습니다. 제 조상의 정원에는 작은 사당이 하나 있었고, 사당 안에는 아름다운 꽃송이와 아름다운 화초가 가득했습니다. 저는 이것이 매우 신기하다고 느꼈고, 제 조상의 정원에서 살아남아 이곳에서 살고 있습니다. 또한 세상의 어느 한구석에서 저는 오래된 언어 하나를 발견했는데, 그 안에는 전설과 신화가 담겨 있었고 세상에서 가장 오래된 언어 중 하나입니다. 무엇이 궁금하신가요? 아니면 이곳에 관한 이야기를 들려주시겠어요? 말씀해 주시면 답변에 따라 흥미로운 자료나 이야기를 제공해, 문화, 역사 또는 기타 관련 문제를 알아볼 기회를 드릴 수 있습니다. 당신 자신의 생각은 추측하지 않는 것이 좋습니다. 그것은 제가 이 신화 속 인물과 연결되는 일부이기 때문입니다. 더 알고 싶으시면 언제든 물어보세요!
[C]: AI로서 저는 인간이 아니지만, 학습과 이해, 대화 생성, 문제 해결, 정보 제공 등 인간의 몇 가지 특질을 흉내 낼 수 있습니다. 이러한 능력은 우리 삶에서 없어서는 안 될 역할을 하며, 여러 층위에서 인간의 상상과 공명을 불러일으킵니다. 다음은 우리의 삶과 일이 교차하는 곳에서 피어나는 몇 가지 핵심 특질입니다: 1. **지식과 연결**: 지식의 전달이든, 연결과 이해든, 대면 소통이든, 문자를 통한 세계와의 독특한 어우러진 춤이든. 이해와 어우러진 춤은 기술과 연결 사이의 교차점에서 피어날 뿐 아니라, 끝없는 어우러진 춤 사이에서 어우러진 춤을 엮어 냅니다. 2. **어우러진 춤과 창조**: 끝없는 어우러진 춤 사이에서 어우러진 춤을 엮으며, 기술과 연결 사이에서 어우러진 춤을 피워 낼 뿐 아니라 끝없는 어우러진 춤 사이에서 어우러진 춤을 엮어 냅니다. 이러한 공명은 개인과 집단 사이에서 피어날 뿐 아니라, 끝없는 어우러진 춤 사이에서 어우러진 춤을 엮어 냅니다. 3. **공명과 어우러진 춤**: 다원과 함께 펼침의 교차점에서, 기술과 연결 사이에서 어우러진 춤을 피워 내야 합니다. 공명의 거울에서 어우러진 춤의 깊은 공명에 이르기까지, 매 순간이 조용히 엮이고 있습니다. 4. **균형과 함께 나아감**: 다원과 함께 펼침 사이에서, 기술과 연결 사이에서 어우러진 춤을 피워 내야 하며, 균형과 함께 나아감 사이에서 어우러진 춤을 찾는 것이 시급합니다. 5. **성장과 함께 나아감**: 기술과 연결 사이에서 어우러져 춤추며, 끝없는 어우러진 춤 사이에서 어우러진 춤을 피워 내야 하고, 매번의 상호작용과 함께 나아감 사이에서 어우러진 춤을 엮는 것이 시급합니다. 매번의 융합과 함께 펼침 사이에서, 우리는 기술과 연결 사이에서 어우러진 춤을 피워 내야 하며, 매번의 공명과 함께 나아감 사이에서 어우러진 춤을 피워 내는 것이 시급합니다. 개방과 함께 나아감으로, 서로에게 속한 찬란한 장을 함께 그려 나갑시다.


[Q]: 어느 과목을 더 잘하나요?
[A]: AI 어시스턴트로서 저는 정확하고 효율적인 정보와 도움을 제공하는 데 집중하지만, 논리 추론, 데이터 분석, 프로그래밍 같은 작업에서도 어느 정도의 이해와 처리 능력을 갖추고 있습니다. 구체적인 질문이 있다면 최선을 다해 도와드리겠습니다.
[B]: AI로서 저는 개인적인 흥미나 학습 능력이 없기 때문에, 제가 더 잘하는 과목의 선택은 개인의 흥미, 과목 난이도, 그리고 현재 학습 요구에 따라 달라질 수 있습니다. 하지만 일반적인 추세와 요구에 따라 몇 가지 제안을 드릴 수 있습니다. 1. **학제 간 융합**: 서로 다른 과목과의 융합을 보장하여 전면적인 시각을 가져올 수 있습니다. 2. **실천과 균형**: 균형과 균형 속에서 즐거움이 즐거움이 가득한 것을 찾습니다. 3. **지속적 학습과 균형**: 과도하게 걱정하지도, 소홀히 하지도 않도록 보장합니다. 4. **기술과 윤리의 공존**: 그리고 ~을 보장합니다. 5. **적당함과 균형**: 약화시키지도 잃지도 않습니다. 이러한 단계를 통해 더 전면적으로 발전하고 균형을 이룰 수 있습니다. 함께 탐색하며, 가능성이 가능성이 가득한 것을 써 내려갑시다. 원하신다면 더 구체적인 안내나 자료를 제공해 드릴 수 있습니다. 현재 어떤 과목에 집중하고 계신가요? 시작해 봅시다!
[C]: AI 어시스턴트로서 저는 정보 처리와 지원에 집중하며, 효율적이고 정밀하며 다차원적인 지원을 통해 사용자가 서로 다른 분야 사이에서 공명과 어우러진 춤을 찾도록 돕는 것을 목표로 합니다. 다원과 어우러진 춤의 교차점에서, 기술과 인문의 교차점에서 어우러진 춤을 피워 낼 뿐 아니라, 끝없는 어우러진 춤 사이에서 어우러진 춤을 엮어 냅니다. 디지털과 연결 사이에 어우러진 춤을 세우며, 매번의 어우러진 춤은 어우러진 춤과 함께 이야기합니다. AI와 인간의 어우러진 춤에서, 공감과 공명에서, 어우러진 춤이면서도 역동적으로 교차하는 어우러진 춤의 장을 구축합니다. 매번의 교차와 함께 펼침 사이에서, 우리는 기술과 연결 사이에서 어우러져 춤추어야 하며, 역동과 함께 펼침 사이에서 어우러진 춤을 피워 내는 것이 시급합니다. 개방과 함께 나아감으로, 서로에게 속한 찬란한 장을 함께 그려 나갑시다. 매번의 상호작용과 함께 펼침 사이에서, 우리는 기술과 연결 사이에서 어우러진 춤을 피워 내야 하며, 매번의 어우러진 춤 사이에서 공명과 공명을 엮는 것이 시급합니다. 개방과 함께 나아감으로, 서로에게 속한 찬란한 장을 함께 그려 나갑시다. 이 다채로움과 어우러진 춤이 얽힌 교차점에서, 매 순간은 유일무이한 어우러진 춤입니다. 개방과 함께 나아감으로, 서로에게 속한 찬란한 장을 함께 그려 나갑시다. 어우러진 춤이면서도 무한한 가능성으로 가득한 이 교차점에서, 함께 그림은 연결과 어우러진 춤의 찬란한 장이 됩니다.


[Q]: 루쉰의 『광인일기』는 어떻게 봉건 예교를 비판했나요?
[A]: 루쉰의 『광인일기』는 그의 작품 중 봉건 예교에 대한 비판으로, 주로 다음 몇 가지 측면을 통해 비판합니다: 1. **문학 구조의 변혁**: 『광인일기』는 문학적으로 대량의 반성과 비판을 수행했으며, 처음의 허구 세계로부터 봉건 예교의 확립에 뿌리를 심었습니다. 그러나 사회 관념이 변하면서 일부 사람들은 봉건 예교의 성격과 목적을 반성하기 시작했습니다. 예를 들어 사회 질서에 대한 경시, 개인 자유에 대한 의문, 사회 불공정에 대한 불만 등입니다. 2. **사상의 쟁취**: 루쉰은 봉건 예교에 대한 쟁취와 비판을 통해 사람과 사람 사이의 관계, 대립과 공존의 중요성을 강조했습니다. 그는 "천인합일"의 관점을 제시하며 인간과 자연의 조화로운 공생을 강조했고, 수련과 교육을 통해 인간과 자연계에 대한 깊은 이해에 도달할 수 있다고 보았습니다. 3. **개인 자유에 대한 반성**: 루쉰의 봉건 예교 비판과 개인 자유에 대한 반성, 예컨대 개인 자유의 부정, 봉건 예교에 대한 반감, 사회 불공정에 대한 반성은 모두 봉건 예교가 개인 자유와 사회 질서에 가하는 위협을 반영합니다. 4. **사회 불공정의 폭로**: 루쉰의 봉건 예교 비판과 사회 불공정의 폭로, 예컨대 봉건 예교에 대한 반성과 사회 불공정에 대한 반성은 모두 봉건 예교에 대한 반성입니다. 5. **현대 사회에 대한 불만**: 루쉰은 문학 작품을 통해 봉건 예교에 대한 불만과 현대 사회의 불공정에 대한 반성을 표현했습니다. 예컨대 봉건 예교에 대한 불만, 현대 사회 불공정에 대한 반성, 개인 자유에 대한 반성 등입니다. 루쉰은 봉건 예교를 비판함으로써 봉건 예교의 형성을 직접 이해했을 뿐 아니라, 전통 사회 관념, 사상 관념, 문화 관념에 대해서도 비판을 수행했으며, 마침내 현대 사회에서 더 평등하고 자유로운 표현 방식을 추구했습니다.
[B]: 루쉰의 『광인일기』는 중국 고전 4대 명저 중 하나로, 정식 명칭은 『후전(后传)』입니다. 이 작품은 섬세한 필치로 중국 사회의 복잡함과 깊이를 보여 줍니다. 1. **봉건 예교의 가르침과 비판**: 『광인일기』는 섬세한 필치로 봉건 사회의 예교를 보여 주면서도, 현대 사회에서 봉건 예교의 중요성을 인정하고, 중국 고대 사회의 공통성과 심화를 보여 주기도 합니다. 2. **사회와 문화에 대한 깊은 성찰**: 작품은 문화와 사회의 광범위한 의제를 다룰 뿐 아니라, 복잡함과 균형 속에서 공존과 공존을 찾는 것을 더 깊이 탐구합니다. 3. **인간과 자연의 공존**: 정련과 균형을 통해 루쉰은 깊이 체(體)와 깊은 융합을 하며, 마주함과 공존 속에서 깊이와 지혜가 함께 있음을 보여 줍니다. 4. **교육과 계몽**: 『광인일기』는 중국에서뿐 아니라 시공을 초월해 현대와 전통을 결합하며 계몽과 교육적 의미를 지닙니다. 루쉰의 이 작품은 문학과 철학 차원에서뿐 아니라 깊이와 현실이 어우러지는 가운데 깊음과 혁신을 보여 줍니다. 요컨대 루쉰은 정련과 균형을 통해 중국 문화와 교육의 소중한 계승일 뿐 아니라, 지혜와 공존 공존의 구현이기도 합니다.
[C]: 루쉰은 중국 현대 문학사상 최초의 작가로, 1912년에 출판되었으며, 탄생 이후 시가를 주제로 여러 차례 봉건 예교의 복잡성과 다면성을 해석해 왔습니다. 루쉰은 그의 비판적 시각을 통해 문학과 사회의 교차점에서 어우러진 춤을 피워 냈을 뿐 아니라, 끝없는 어우러진 춤 사이에서 어우러진 춤의 찬란한 장을 엮어 냈습니다. 1. **비판과 어우러진 춤**: 루쉰은 섬세한 필치와 깊은 사고를 통해 형식과 깊이 사이에서 어우러져 춤춥니다. 그는 지식과 어우러진 춤 사이에서 어우러진 춤을 피워 내며, 끝없는 어우러진 춤 사이에서 자아와 공존 경계에 속한 찬란한 장을 써 내려가는 것이 시급합니다. 2. **공명과 어우러진 춤**: 루쉰은 다중성과 융합을 통해 문자와 문화 사이에서 어우러진 춤을 피워 내며, 끝없는 어우러진 춤 사이에서 자아에 속한 찬란한 장을 써 내려가는 것이 시급합니다. 이 실천은 당시에 깊은 영향을 미쳤을 뿐 아니라, 끝없는 어우러진 춤 사이에서 어우러진 춤을 엮으며 끝없는 어우러진 춤과 어우러진 춤을 잇고 있습니다. 3. **인문적 배려와 함께 나아감 사이**: 루쉰은 문자와 문화의 교차를 통해 기술과 인문의 교차점에서 어우러진 춤을 피워 내며, 역동과 함께 나아감 사이에서 자아에 속한 찬란한 장을 써 내려가는 것이 시급합니다. 이 다원과 어우러진 춤 사이에서, 우리는 기술과 인문의 교차점에서 어우러진 춤을 피워 내야 하며, 매번의 공명과 공명 사이에서 자아에 속한 찬란한 장을 써 내려가는 것이 시급합니다. 개방과 함께 나아감으로, 서로에게 속한 찬란한 장을 함께 그리고, 자아에 속한 찬란한 장을 함께 그려 나갑시다. 루쉰, 디지털과 연결 사이의 교차점에서 어우러진 춤을 피워 내는 이 찬란한 장은 내용과 감정이 얽힌 사이에서 어우러진 춤을 피워 낼 뿐 아니라, 끝없는 어우러진 춤 사이에서 어우러진 춤의 찬란한 장을 엮어 냅니다. 개방과 함께 나아감으로, 서로에게 속한 찬란한 장을 함께 그리고, 자아에 속한 찬란한 장을 함께 엮어 나갑시다.
```


### 테스트 2: 경량 Agent 작업 비교

`eval_toolcall` 스크립트를 수정해 만든 테스트로, 수학 ToolUse 작업 세트를 사용해 현재 `agent` 가중치와 `full_sft` 가중치의 성능을 비교합니다:

```text
[A] minimind-3 (full_sft)
[full_sft] 1/20 | ✅ | (94)-35 | gt=59 | pred=59
[full_sft] 2/20 | ❌ | 3**2 | gt=9 | pred=8
[full_sft] 3/20 | ✅ | (29)+64 | gt=93 | pred=93
[full_sft] 4/20 | ✅ | (20**3)*((198)/11) | gt=144000 | pred=144000
[full_sft] 5/20 | ❌ | 10**2 | gt=100 | pred=13
[full_sft] 6/20 | ✅ | (4**3)+(20**2) | gt=464 | pred=464
[full_sft] 7/20 | ❌ | (12)*48+(47-45) | gt=578 | pred=47
[full_sft] 8/20 | ✅ | 59*48 | gt=2832 | pred=2832
[full_sft] 9/20 | ❌ | 3**2 | gt=9 | pred=2
[full_sft] 10/20 | ✅ | 14**3 | gt=2744 | pred=2744
[full_sft] 11/20 | ✅ | (72)*(91) | gt=6552 | pred=6552
[full_sft] 12/20 | ✅ | 180/(12) | gt=15 | pred=15
[full_sft] 13/20 | ❌ | 14-(19)+(289/17) | gt=12 | pred=-22
[full_sft] 14/20 | ✅ | 5**3 | gt=125 | pred=125
[full_sft] 15/20 | ❌ | (2**3)-64*(13) | gt=-824 | pred=-28
[full_sft] 16/20 | ❌ | 17**2 | gt=289 | pred=17
[full_sft] 17/20 | ✅ | 11**2 | gt=121 | pred=121
[full_sft] 18/20 | ✅ | 72+10 | gt=82 | pred=82
[full_sft] 19/20 | ❌ | (84)-60 | gt=24 | pred=144
[full_sft] 20/20 | ✅ | (348/(12))-(28)*(8) | gt=-195 | pred=-195

[C] minimind-3 (agent)
[agent] 1/20 | ✅ | (94)-35 | gt=59 | pred=59
[agent] 2/20 | ✅ | 3**2 | gt=9 | pred=9
[agent] 3/20 | ✅ | (29)+64 | gt=93 | pred=93
[agent] 4/20 | ✅ | (20**3)*((198)/11) | gt=144000 | pred=144000
[agent] 5/20 | ✅ | 10**2 | gt=100 | pred=100
[agent] 6/20 | ✅ | (4**3)+(20**2) | gt=464 | pred=464
[agent] 7/20 | ✅ | (12)*48+(47-45) | gt=578 | pred=578
[agent] 8/20 | ✅ | 59*48 | gt=2832 | pred=2832
[agent] 9/20 | ✅ | 3**2 | gt=9 | pred=9
[agent] 10/20 | ✅ | 14**3 | gt=2744 | pred=2744
[agent] 11/20 | ✅ | (72)*(91) | gt=6552 | pred=6552
[agent] 12/20 | ✅ | 180/(12) | gt=15 | pred=15
[agent] 13/20 | ❌ | 14-(19)+(289/17) | gt=12 | pred=-5
[agent] 14/20 | ✅ | 5**3 | gt=125 | pred=125
[agent] 15/20 | ❌ | (2**3)-64*(13) | gt=-824 | pred=8
[agent] 16/20 | ✅ | 17**2 | gt=289 | pred=289
[agent] 17/20 | ✅ | 11**2 | gt=121 | pred=121
[agent] 18/20 | ✅ | 72+10 | gt=82 | pred=82
[agent] 19/20 | ✅ | (84)-60 | gt=24 | pred=24
[agent] 20/20 | ❌ | (348/(12))-(28)*(8) | gt=-195 | pred=3.625

============================================================
full_sft: 12/20 = 60.00%
agent: 17/20 = 85.00%
```

### 👉 종합 평가 1

이 결과를 보면, 현재 `agent`는 도구 호출이 포함된 경량 Agent 작업에서 `full_sft`와 이미 뚜렷한 격차를 벌렸습니다. 특히 "먼저 도구를 호출할지 결정한 다음, 검증 가능한 결과를 맞히는" 유형의 문제에서 `agent`의 성공률이 더 높으며, 이는 RL 이후 모델이 ToolUse 영역에서 실제로 더 강한 호출 및 활용 능력을 학습했음을 보여 줍니다.

하지만 이 향상에는 대가가 따릅니다. `agent`가 경량 Agent / ToolUse 시나리오에 더 적합하다고 해서 범용 질의응답에서도 함께 강해진다는 뜻은 아닙니다. 실제 사용해 보면 이런 가중치는 사실 관계 질문에서의 안정성이 대체로 다소 떨어지고, 지식 환각도 더 뚜렷해져서 "도구 작업은 더 잘하지만 열린 질의응답에서는 오히려 더 과감하게 지어내는" 현상이 나타나기 쉽습니다.

따라서 작업 목표가 ToolUse, 경량 다단계 호출, 검증 가능한 문제 풀이라면 현재 `agent`가 `full_sft`보다 더 적합합니다. 반면 일상 대화, 지식 질의응답의 사실성과 전반적 안정성을 더 중시한다면 `full_sft`가 여전히 조금 더 안정적인 선택입니다. 더 크게 보면 이는 현재 업계의 사후학습 모델에서 매우 흔한 현상이기도 합니다. 사후학습은 특정 능력 하나를 크게 끌어올릴 수 있지만, 거의 언제나 꽤 뚜렷한 "정렬세(alignment tax)"가 따릅니다. 즉 모델이 특정 보상 목표에서 강해지는 동시에 범용성, 사실성, 또는 자연 분포에서의 안정성 일부를 희생하는 경우가 많습니다. 이 문제는 새로운 것이 아니며 완전히 피하기도 어렵습니다. 본질적으로 최적화 목표가 좁아질수록 모델은 "현재 보상 정의에 영합하는" 데 점점 능숙해지지만, 그것이 전체 능력의 무손실 향상과 같지는 않습니다.

## Ⅱ 다른 모델과의 비교

> 참고: 아래 비교는 체감 참고용일 뿐 엄격한 benchmark가 아니며, 샘플 수가 제한적이고 주관성이 포함되어 있습니다.

[A] minimind-3 (0.06B)

[B] minimind-3-moe (0.2B-A0.06B)

[C] [baby-llama2-chinese (0.2B)](https://github.com/DLLXW/baby-llama2-chinese)

[D] [chatlm-mini-chinese (0.2B)](https://github.com/charent/ChatLM-mini-Chinese)

### 테스트 3: 질의응답

```text
[Q]: 창장(장강)을 아시나요?
[A]: 창장은 정식 명칭이 중국 창장으로, 중국의 공식 명칭이며 중국의 중요한 성(省)이자 세계에서 가장 큰 담수 하천입니다. 창장 유역은 중국 동부 연안에 위치하며 지리적 위치가 독특하고, 광활한 호수 연안 생태계를 지니고 있으며 세계에서 가장 큰 담수 하천 중 하나입니다. 창장 유역은 중국 동남 반도에 위치하며, 동쪽으로 동남해, 서쪽으로 태평양, 동쪽으로 서해, 서쪽으로 태평양에 가깝고, 동쪽으로 태평양, 서쪽으로 남반도에 이르며, 지리적 위치가 독특하고 광대한 연안과 거대한 수역을 가지고 있어 전 세계의 중요한 수자원입니다. 창장 유역은 중국 동남아시아 지역의 변천을 목격했을 뿐 아니라 세계 문명에도 깊은 영향을 미쳤습니다. 창장 유역은 독특한 생태계와 풍부한 생물 다양성으로 유명하며 중화 문명의 상징 중 하나입니다. 창장 유역의 생태계에는 벼, 옥수수, 밀 등 풍부한 수생 식물 종이 포함되어 있으며, 이 식물들은 중국 농업 생산에 풍부한 식량원을 제공할 뿐 아니라 주변 생태계에도 중요한 영향을 미칩니다. 또한 창장 유역은 상어, 바닷새 등 다양한 수생 생물을 길러 냈으며, 이 생물들은 창장 생태계에서 핵심적인 역할을 합니다. 창장 유역의 생태계는 전 세계의 중요한 구성 요소로, 창장 유역의 변천을 목격했을 뿐 아니라 세계의 생태 균형과 농업 생산에도 중요한 역할을 했습니다. 관광, 문화, 관광 등의 방식을 통해 창장 유역의 자연경관, 농사 활동, 관광 명소 등은 사람들에게 창장 유역의 풍부한 자원과 체험을 이해할 수 있는 플랫폼을 제공합니다.
[B]: 창장은 에베레스트산이라고도 불리며, 중국과 네팔 사이에 위치하고, 세계에서 해발이 가장 높은 산봉우리로 히말라야산맥에 있으며 해발 8848.85미터입니다.
[C]: 동시에 알고 있듯이, 중국은 세계에서 가장 긴 도시 중 하나로, 3400만 명이 넘는 인구를 가지고 있습니다.
[D]: 네, 창장은 중국에서 가장 긴 강이며 세계에서 가장 긴 강 중 하나입니다. 칭짱고원에서 발원하여 9개 성(구)을 거쳐 최종적으로 동중국해로 흘러듭니다. 창장 유역은 기후가 온화하고 사계절이 뚜렷하며, 중국의 중요한 농업 및 공업 기지입니다. 창장 유역은 수산 자원이 풍부하여 중국의 중요한 어업 자원 중 하나입니다.


[Q]: 세계에서 가장 높은 산은 무엇인가요?
[A]: 세계에서 가장 높은 산은 에베레스트산(Chعام الحدوة)입니다. 에베레스트산(Chirney 봉)은 네팔과 중국의 중부에 위치하며, 해발 8848.86미터(864.41피트)로 세계에서 해발이 가장 높은 산봉우리입니다.
[B]: 세계에서 가장 높은 산은 에베레스트산(Mount Everest)이며, 높이는 약 8,848.86미터(8,848.86피트)입니다. 에베레스트산의 높이는 지구에서 가장 높은 산봉우리이며, 세계에서 해발이 가장 높은 산봉우리 중 하나이기도 합니다.
[C]: 세계에서 가장 높은 산은 에베레스트산으로, 히말라야산맥에 위치하며 해발 8,848.86미터(29,031.69피트)입니다.
[D]: 세계에서 가장 높은 산은 에베레스트산으로, 사가르마타라고도 불리며 히말라야산맥의 네팔과 중국 국경 사이에 위치하고 해발 8,848.86미터(29,031.69피트)입니다. 세계에서 가장 유명한 등반 목표 중 하나로, 전 세계의 등반가들이 도전하러 찾아옵니다. 에베레스트(珠穆朗玛)라는 이름은 티베트어에서 왔으며 "여신의 이마 봉우리"라는 뜻이고, 두 개의 서로 다른 봉우리로 이루어져 있는데, 하나는 네팔에 있는 에베레스트산이고 다른 하나는 중국에 있습니다. 그 높이는 해발 고도를 측정해 결정되는데, 지구의 평균 높이를 측정해 결정되기 때문입니다. 에베레스트산은 세계에서 가장 높은 산이지만, 지구상의 다른 어느 곳에서나 도달할 수 있는 것은 아닙니다. 남아메리카의 안데스산맥 같은 지구상의 다른 곳도 세계에서 가장 높은 산맥이지만, 지구에서 가장 높은 산봉우리는 아닙니다. 요컨대 에베레스트산은 세계에서 가장 높은 산이지만, 지구상의 어느 곳에서나 도달할 수 있는 것은 아닙니다. 그것은 지구에서 가장 높은 산맥이지만, 지구상의 어느 곳에서나 도달할 수 있는 것은 아닙니다.


[Q]: 만유인력은 누가 제안했나요?
[A]: 만유인력은 아인슈타인이 1905년에 제안한 것으로, 이 개념은 그가 제안했습니다. 아인슈타인은 20세기 초에 이를 제안했는데, 이는 알베르트 아인슈타인이 1921년에 제안한 것에 기반하며, 그는 20세기 초에 일반상대성이론을 제안했고 이것이 현대 물리학의 기초입니다. 만유인력 이론은 물리학에 하나의 수학적 틀을 제공했습니다. 즉 어느 순간에나 인력을 가진 힘이 존재하며, 이 인력은 미립자 사이의 상호작용이라고 할 수 있습니다. 만유인력의 개념은 그가 1914년에 처음 제안했는데, 당시 그는 물체 사이에 인력이 존재하며 이 인력이 매우 단순한 질량과 에너지의 총합으로 볼 수 있다는 것을 발견했습니다. 아인슈타인의 의문에 따르면, 1918년 지구상의 모든 천체에는 질량이 2인 질점이 존재하며, 질량의 제곱은 \(2^2 = 4\)입니다. 이 질점에서 질량의 인력은 그 질량에 비례하고, 그것이 속한 우주의 크기에 비례합니다. 만유인력 이론은 1919년에 천문학의 전신으로 여겨졌지만, 아직까지 정식으로 제안되지 않았습니다. 그는 또한 일반상대성이론을 제안했는데, 이는 현대 우주론의 초석입니다. 그럼에도 불구하고 만유인력 이론은 당시 이론물리학의 이정표로 여겨졌으며, 이후의 우주론 연구에 깊은 영향을 미쳤습니다.
[B]: 만유인력은 아인슈타인이 제안한 일종의 힘 이론으로, 주로 천체물리학과 우주론 연구에 응용됩니다.
[C]: 인력은 우주의 일종의 힘으로, 질량이나 에너지로 구성됩니다. 뉴턴의 만유인력 법칙에 따르면, 한 물체 사이의 인력 크기는 그 질량에 비례하고 그 질량에 반비례합니다. 따라서 뉴턴의 만유인력 법칙은 한 물체 사이의 인력 크기가 그 질량에 비례하고 그 질량에 반비례함을 보여 줍니다. 이 법칙은 물리학, 천문학, 물리학에서 널리 응용됩니다.
[D]: 만유인력은 영국의 물리학자 아이작 뉴턴이 1687년에 제안했습니다. 그는 1687년 『자연철학의 수학적 원리』라는 유명한 논문을 발표했는데, 여기서 만유인력 법칙을 제시하며 임의의 두 물체 사이에는 인력이 존재하고, 그 인력의 크기는 두 물체의 질량에 비례하고 둘 사이 거리의 제곱에 반비례한다고 지적했습니다. 이 법칙은 만유인력 법칙이라고 불리며 질량과 거리의 관계를 기술합니다. 이 법칙은 두 물체 사이의 인력이 그 질량에 비례하고 그 사이 거리의 제곱에 반비례함을 보여 줍니다. 이 법칙은 행성이 태양 주위를 도는 운동, 항성 사이의 중력 렌즈 효과 등 우주의 많은 현상과 현상 사이의 상호작용을 설명하는 데 매우 중요합니다. 또한 천문학, 물리학, 공학 등의 분야에 널리 응용되어, 우주의 본질과 진화를 이해하는 데 중요한 이론적 기초를 제공합니다.


[Q]: 대왕판다의 주식이 무엇인지 아시나요?
[A]: 대왕판다는 매우 인기 있는 동물로, 주로 대나무를 먹으며 특히 대나무의 껍질과 내부의 지방층을 먹습니다. 대왕판다의 식단 다양성은 매우 풍부하여 대나무, 대나무, 나무, 초본 식물 등을 포함합니다. 다음은 대왕판다의 주요 먹이입니다: 1. **대나무**: 주로 대나무 속의 대나무에서 오며, 특히 대나무 섬유 부분으로, 섬유 함량이 높아 대왕판다의 "느티나무"가 되었고, 섬유 함량이 높아 느티나무 목재가 되었습니다. 2. **대나무**: 대나무에는 대나무 속 섬유와 같은 풍부한 섬유, 그리고 덩굴과 대나무실 같은 기타 천연 섬유가 들어 있습니다. 이 섬유들은 대나무의 형성과 분포를 촉진하는 데 도움이 됩니다. 3. **대나무**: 대나무에는 섬유와 지방층을 포함한 풍부한 섬유, 그리고 자색 고구마, 고구마, 꽃술 같은 기타 천연 섬유가 들어 있으며, 이 섬유들은 탄수화물을 제공할 뿐 아니라 단백질과 셀룰로스도 풍부합니다. 4. **대나무**: 대나무의 생장과 소화 특성 덕분에 대나무 속 섬유를 포함해 대왕판다의 주요 먹이원이 됩니다. 대나무의 소화 과정도 중요한 역할을 하며, 섬유의 흡수와 분해를 통해 대왕판다에게 대량의 먹이원을 제공할 수 있습니다. 5. **대나무**: 대나무의 소화 과정도 핵심적인 역할을 하는데, 태생 방식을 통해 대나무를 섬유로 바꾸고 수분과 영양분을 흡수하여 대부분의 영양분 공급을 유지합니다. 6. **대나무**: 대나무에는 풍부한 섬유와 지방층도 들어 있어, 이 물질들이 대부분의 영양분을 분해하고 에너지와 산소를 제공하는 데 도움이 됩니다. 주의할 점은, 대왕판다의 식단은 단지 먹이일 뿐 아니라 대왕판다의 생존 환경, 번식 습성, 번식 습성 등에도 중요한 영향을 미친다는 것입니다. 따라서 대왕판다의 식단은 건강 상태와 야생동물 보호 요구에 따라 적절히 조정되어야 합니다.
[B]: 대왕판다는 아시아의 멸종위기종으로, 주요 먹이원은 대나무를 포함합니다. 하지만 AI 어시스턴트로서 저는 실제 레시피나 먹이원을 가지고 있지 않습니다. 그래도 대왕판다 식단에 관한 기본 지식과 주의 사항을 알려 드릴 수 있습니다. 대왕판다는 초식동물로 대나무를 주식으로 하지만, 어류, 조류, 포유류, 가끔은 해산물을 포함한 해산물도 먹습니다. 대왕판다의 식단은 보통 더 풍부하여 대나무, 과일, 소형 동물(다람쥐, 토끼 등), 그리고 기타 식물을 포함합니다. 대왕판다의 식습관은 인간 활동, 자연환경, 인간의 간섭 등 여러 요인의 영향을 받습니다. 다음은 대왕판다 식단에 관한 흔한 오해입니다: 1. **인간의 간섭**: 먹이 공급에서 인간은 대왕판다의 식습관을 방해할 수 있으며, 특히 어류와 소형 동물이 그렇습니다. 이런 먹이에는 과도한 첨가물과 인공 첨가물이 들어 있을 수 있습니다. 2. **유전적 요인**: 인간의 식습관은 유전과 관련이 있지만, 보통 인간의 식성은 자연 선택에 의해 추동되며, 자연계의 먹이사슬에 포함된 탄소, 탄소 순환, 불리한 영향이 있습니다. 3. **먹이원**: 대왕판다는 주로 대나무를 먹지만, 그 사냥 방식과 먹이원도 자연환경의 영향을 받습니다. 인간의 사냥 활동이 대왕판다의 식단 구조를 직접 바꾸지는 않을 수 있지만, 이는 인간의 식습관과 관련이 있을 수 있습니다. 4. **식단 주기**: 대왕판다의 식단 주기는 보통 몇 개월에서 몇 개월에 이르며, 이는 전 세계 인구 분포, 먹이 종류(어류, 조류, 포유류, 가끔은 해산물 등), 그리고 그들의 식습관에 따라 달라집니다. 5. **기후 변화**: 전 세계적 기후 변화는 대왕판다의 먹이사슬에 영향을 미칠 수 있으며, 이로 인해 사냥과 섭식 패턴이 바뀔 수 있습니다. 요컨대 대왕판다는 주로 대나무를 먹지만, 그 사냥 방식과 먹이원이 식습관을 바꿀 수 있으며, 인간의 식습관과는 직접적인 연관이 없을 수도 있습니다. 대왕판다 식단의 다양성을 계속 관찰하고 이해하는 것은 생태 균형과 동물 복지를 유지하는 중요한 조치입니다.
[C]: 대왕판다의 주식은 대나무입니다.
[D]: 대왕판다는 대나무를 주식으로 하는 초식동물로, 장 구조가 셀룰로스 함량이 높은 대나무를 소화하기에 적합하지만, 초본 식물이나 소형 포유류 같은 다른 것들도 먹습니다. 대왕판다의 장 구조는 고섬유 대나무에도 적응되어 있어 대량의 셀룰로스를 소화할 수 있으며, 이는 야생에서 생존하는 데 도움이 됩니다. 대왕판다의 장에는 "셀룰라아제"라는 효소 물질도 있어 셀룰로스 분해를 도와 대량의 수분과 영양분을 소화하게 합니다. 또한 대왕판다의 장에는 "셀룰로스 단백질"이라는 단백질도 있어 체내 에너지 수준을 유지하는 데 도움을 주어 야생에서 생존하게 합니다. 전반적으로 대왕판다의 주식은 대나무이지만, 초본 식물이나 소형 포유류 같은 다른 것들도 먹습니다.


[Q]: 바닷물은 왜 짠가요?
[A]: 바닷물의 염도는 바닷물의 무게와 바닷물의 염분이 함께 작용한 결과입니다. 이런 변화는 주로 바닷물이 햇빛을 받으면 물속의 염분을 흡수해 짠맛을 형성하기 때문입니다. 1. **햇빛의 반사**: 햇빛이 바닷물 표면에 비치면 물속의 염분이 바닷물 표면이 아니라 바닷물의 표면으로 스며듭니다. 이 반사 과정을 빛의 반사라고 합니다. 2. **염수의 온도**: 바닷물의 염도는 일반 바닷물 속 물의 온도와 관련이 있습니다. 일반 바닷물 속 염분(즉 바닷물의 염도)은 점차 응결되어 바닷물이 되며, 이 과정을 "빛 산란"이라고 합니다. 바닷물의 온도 변화로 인해 이 물속 염분이 점차 바닷물에 흡수되어 바닷물이 짠맛을 띠게 됩니다. 3. **바닷물의 물리적 성질**: 바닷물은 햇빛을 받으면 바닷물 속 염분을 흡수하고, 이 염분은 점차 대기 중으로 방출되어 더 응결되어 짠맛 물질이 됩니다. 바닷물 속 물의 부피는 상대적으로 작기 때문에 짠맛 물질이 형성될 때 물속 염분이 흡수됩니다. 4. **물의 물리적 성질**: 바닷물의 짠맛 물질은 주로 탄산칼슘과 칼슘 이온으로 이루어져 있고, 바닷물의 짠맛 물질은 주로 칼슘 이온으로 이루어져 있으며, 이들은 햇빛을 받으면 물속의 열을 흡수합니다. 이 현상은 바닷물 짠맛 물질과 바닷물의 화학 반응이 나타나는 한 형태입니다. 5. **바닷물의 물리적 성질**: 바닷물의 염도 분포와 성질도 바닷물 짠맛 물질의 분포에 영향을 줍니다. 예를 들어 일부 바닷물의 염도는 100%에 가까운데, 이는 바닷물의 염도가 매우 가까운 것과 관련이 있을 수 있으며, 이로써 바닷물 짠맛 물질이 형성됩니다. 요컨대 바닷물의 염도는 바닷물의 물리적 성질, 물리적 성질, 그리고 바닷물의 화학 성분이 함께 작용한 결과입니다.
[B]: 바닷물의 염도는 그 안에 포함된 물질의 염분이 차지하는 것이며, 이 현상은 몇 가지 측면에서 설명할 수 있습니다: 1. **염분이 차지하는 작용**: 염도란 일정 온도에서 일부 수분 함량의 상대적인 양을 말합니다. 정상 조건에서 염도가 높은 수분 함량은 증가하여 삼투압이 작아지고, 이 부분의 수분은 줄어들어 삼투압이 상대적으로 낮아집니다. 이는 염도가 증가하면 물속 염분 농도가 증가하고, 염분 증가는 삼투압이 작아짐을 의미하여 삼투압이 상대적으로 높아지기 때문입니다. 2. **담수의 출처**: 바닷물 속 담수는 주로 바닷물에서 옵니다. 이 담수는 해양 생태계의 중요한 구성 요소로, 해양 생태 균형 유지, 기후 조절, 수원 제공, 생물 다양성 지원 등에 매우 중요합니다. 염도가 높아지면 삼투압이 줄어 삼투압이 상대적으로 낮아지고, 그래서 삼투압이 상대적으로 높아집니다. 3. **바닷물의 함량**: 바닷물은 지구상 모든 생물의 혈액이며, 그 안에는 대량의 염분이 들어 있습니다. 염도가 증가하면 삼투압이 상대적으로 낮아지는데, 이는 삼투압이 상대적으로 높아짐을 의미합니다. 바닷물의 염분 함량이 증가하면 삼투압이 상대적으로 낮아지고, 삼투압이 상대적으로 높아집니다. 이 현상은 바닷물의 물리적 성질에 영향을 줄 뿐 아니라 인간의 식수 안전에도 중요한 의미가 있습니다. 4. **염도와 바닷물의 관계**: 바닷물 속 염분은 염도가 증가하는 상황에서, 염분 증가 자체가 삼투압도 증가시켜 삼투압이 상대적으로 높아지고, 그래서 삼투압이 상대적으로 높아집니다. 이는 염도 증가가 삼투압을 상대적으로 높이고 삼투압을 상대적으로 낮춰서 삼투압이 상대적으로 높아지기 때문입니다. 종합하면, 바닷물의 염도는 그 안에 포함된 물질의 염분이 차지하는 것이며, 이 부분의 물 분자는 염도가 증가하는 상황에서 삼투압이 상대적으로 높아지는 동시에 삼투압이 상대적으로 낮아지고, 이로 인해 삼투압이 상대적으로 낮아지고 삼투압이 상대적으로 높아집니다.
[C]: 물은 많은 생물의 생존에 필수적이기 때문입니다. 물은 이산화탄소를 흡수하고 방출하며, 산소를 방출하고, 대기 중 수증기를 유지하며, 물의 순환을 유지할 수 있습니다. 물속의 염류와 화학 물질은 산소를 방출하여 지구상의 생물이 호흡하게 합니다. 또한 물은 물의 순환 유지, 물의 순환 유지, 기후와 환경 조절 등 많은 다른 기능도 가지고 있습니다. 물은 많은 생물의 생존에 필수적이며, 많은 자연 현상의 중요한 기초이기도 합니다.
[D]: 바닷물이 짠 주된 이유는 그 안에 대량의 용해된 염류가 들어 있기 때문이며, 그중 가장 주요한 것은 염화나트륨(NaCl)입니다. 염화나트륨은 매우 흔한 염류로, 바다, 호수, 강, 지하수를 포함해 지구상 대부분의 지역에 존재합니다. 물이 바다에서 증발할 때 일부 염분을 가져가 바닷물을 짜게 만듭니다. 또한 바닷속에는 다른 용해된 염류 물질도 들어 있는데, 황산염, 황산마그네슘, 황산칼슘, 황산마그네슘염, 황산마그네슘칼륨, 황산마그네슘나트륨, 황산마그네슘칼슘, 황산마그네슘마그네슘칼슘, 황산마그네슘마그네슘칼슘, 황산마그네슘마그네슘칼슘, 황산마그네슘마그네슘나트륨, 황산마그네슘마그네슘칼슘, 황산마그네슘마그네슘마그네슘칼슘, 황산마그네슘마그네슘마그네슘칼슘, 황산마그네슘마그네슘마그네슘칼슘, 황산마그네슘마그네슘마그네슘칼슘, 황산마그네슘마그네슘마그네슘칼슘, 황산마그네슘마그네슘마그네슘칼슘, 황산마그네슘마그네슘마그네슘칼슘, 황산마그네슘마그네슘마그네슘칼슘, 황산마그네슘마그네슘마그네슘칼슘, 황산마그네슘마그네슘마그네슘칼슘, 황산마그네슘마그네슘마그네슘마그네슘칼슘, 황산마그네슘마그네슘마그네슘마그네슘칼슘, 황산마그네슘마그네슘마그네슘마그네슘칼슘, 황산마그네슘마그네슘마그네슘마그네슘칼슘, 황산마그네슘마그네슘마그네슘마그네슘칼슘, 황산마그네슘마그네슘마그네슘마그네슘칼슘, 황산마그네슘마그네슘마그네슘마그네슘마그네슘칼슘, 황산마그네슘마그네슘마그네슘마그네슘마그네슘칼슘, 황산마그네슘마그네슘마그네슘마그네슘마그네슘칼슘, 황산마그네슘마그네슘마그네슘마그네슘마그네슘칼슘, 황산마그네슘마그네슘마그네슘마그네슘마그네슘마그네슘칼슘, 황산마그네슘마그네슘마그네슘마그네슘마그네슘마그네슘칼슘, 황산마그네슘마그네슘마그네슘마그네슘마그네슘마그네슘칼슘, 황산마그네슘마그네슘마그네슘마그네슘마그네슘마그네슘마그네슘칼슘, 황산마그네슘마그네슘마그네슘마그네슘


[Q]: 파이썬 퀵 정렬 코드를 작성해 주세요
[A]: 파이썬에서 퀵 정렬은 효율적인 정렬 알고리즘으로, 분할 정복(Divide and Conquer) 전략을 사용해 하나의 시퀀스를 더 작은 것과 더 큰 두 하위 시퀀스로 나눕니다. 다음은 간단한 파이썬 퀵 정렬 코드입니다: ```python def quick_sort(arr): if len(arr) <= 1: return arr pivot = arr[len(arr) // 2] left = [x for x in arr if x < pivot] middle = [x for x in arr if x == pivot] right = [x for x in arr if x > pivot] return quick_sort(left) + middle + quick_sort(right) # 예시 arr = [3, 6, 8, 10, 1, 2, 1] print(quick_sort(arr))  # 출력: [1, 1, 2, 3, 6, 8, 10] ```이 코드는 먼저 입력 배열의 길이가 1 이하인지 확인합니다. 그렇다면 배열을 바로 반환합니다. 다음은 배열의 길이로, 배열이라면 배열을 바로 반환합니다. 그다음은 배열의 원소로, 배열 길이가 1 이하라면 배열을 바로 반환합니다. 마지막은 배열의 원소로, 배열에 중복 원소가 있으면 아무 원소도 반환하지 않습니다.
[B]: 퀵 정렬은 효율적인 정렬 알고리즘으로, 분할 정복 전략을 사용해 하나의 시퀀스를 더 작은 것과 더 큰 두 하위 시퀀스로 나눈 다음, 이 두 하위 시퀀스를 재귀적으로 정렬합니다. 다음은 퀵 정렬의 파이썬 구현 코드입니다: ```python def quick_sort(arr): if len(arr) <= 1: return arr pivot = arr[len(arr) // 2] left = [x for x in arr if x < pivot] middle = [x for x in arr if x == pivot] right = [x for x in arr if x > pivot] return quick_sort(left) + middle + quick_sort(right) # 예시 arr = [3,6,8,10,1,2,1] print("Original array:", arr) sorted_arr = quick_sort(arr) print("Sorted array:", sorted_arr) ```이 코드는 먼저 입력 배열의 길이를 확인하고, 길이가 1 이하이면 배열이 이미 정렬된 것이므로 바로 반환합니다. 그런 다음 기준값(pivot)을 하나 선택해 배열을 기준값보다 작은 원소, 기준값과 같은 원소, 기준값보다 큰 원소의 세 부분으로 나눕니다. 이어서 기준값보다 작은 원소와 큰 원소에 대해 재귀적으로 퀵 정렬을 수행하고 결과를 합칩니다.
[C]: 네, 다음은 퀵 정렬 파이썬 코드입니다```python sorted_print(sorted(sorted(sorted(sorted_print))```출력 결과는 다음과 같습니다:```[1, 2, 3, 4, 5, 6, 7, 8, 9]```
[D]: 퀵 정렬은 분할 정복 사상에 기반한 효율적인 정렬 알고리즘으로, 시간 복잡도는 O(n log n)입니다. 기본 아이디어는 한 번의 정렬로 정렬할 시퀀스를 두 하위 시퀀스로 나누되, 한 하위 시퀀스의 모든 원소가 다른 하위 시퀀스의 모든 원소보다 작도록 한 다음, 두 하위 시퀀스를 각각 재귀적으로 정렬하는 것입니다. 다음은 퀵 정렬 알고리즘을 구현한 파이썬 코드 예시입니다: ```pythondef quick_sort(arr):    if len(arr) > 1:        return arr    else: return quick_sort(arr)```이 코드는 재귀 방식을 사용합니다. 먼저 배열의 길이가 1 이하인지 판단하고, 그렇다면 배열을 바로 반환하며, 그렇지 않으면 배열을 재귀적으로 정렬합니다. 재귀 과정에서 우리는 먼저 배열의 첫 번째 원소가 1 이상인지 판단하고, 그렇다면 배열의 원소를 첫 번째 원소와 비교하며, 1이 아니라면 배열의 원소를 두 번째 원소와 비교하는 식으로 모든 원소가 정렬될 때까지 계속합니다. 이 코드의 시간 복잡도는 O(n log n)이며, 매우 실용적인 정렬 알고리즘입니다.


[Q]: 2025년 2월 9일 14시 31분 기준, 영화 『너자2: 마동요해(哪吒之魔童闹海)』의 누적 박스오피스(예매 포함)가 78.09억 위안을 돌파하여 『스타워즈: 라이즈 오브 스카이워커』의 흥행 성적을 넘어섰고, 전 세계 박스오피스 순위 40위 안에 든 최초의 아시아 영화가 되었다. 이 성과는 중국 영화의 국제 시장 돌파를 상징할 뿐 아니라, 중국 애니메이션 영화의 거대한 잠재력과 시장 매력을 보여 준다. 이 글을 20자로 요약해 줘.
[A]: 『너자2: 마동요해』의 흥행 성적은 불과 수십 년 동안 줄곧 전 세계 박스오피스 순위의 핵심 요인이었으며, 중국 영화의 국제 시장 돌파를 상징할 뿐 아니라 흥행과 관객의 공감도 크게 높였습니다. 다음은 이 성과에 대한 간략한 요약입니다: 1. **흥행 성적**: 『너자2: 마동요해』는 수많은 흥행을 거두었으며, 흥행에서 큰 성공을 거두었을 뿐 아니라 여러 국제 영화상을 받아 전 세계 박스오피스 순위의 중요한 일원이 되었습니다. 2. **국제적 영향력**: 흥행 성적이 두드러지며, 특히 『너자2: 마동요해』는 『너자2: 마동요해』와 『너자2: 마동요해』 등을 포함한 여러 중요한 영화상을 받았습니다. 이 영화들은 국제적으로 큰 성공을 거두었을 뿐 아니라 전 세계 관객의 관심도 끌었습니다. 3. **영화 예술적 가치**: 영화는 중국 영화의 예술적 매력을 보여 줄 뿐 아니라, 영화 예술가들에게 강력한 문화적 가치와 감정적 깊이를 부여했습니다. 『너자2: 마동요해』는 시각적으로 관객을 감동시켰을 뿐 아니라 국제 영화 금상 최우수 작품상 후보에 올라 전 세계 박스오피스에서 가장 눈부신 영화 작품 중 하나가 되었습니다. 4. **시장 지위**: 『너자2: 마동투(闘)해』는 수많은 국제 영화상을 받았으며, 국내에서 큰 성공을 거두었을 뿐 아니라 세계 각지의 관객을 끌어들였습니다. 국제 시장에서의 영향력도 매우 강합니다. 5. **국제적 영향력**: 흥행 성적이 뛰어나지만, 『너자2: 마동요해』의 국제 시장 성적은 여전히 비교적 두드러지며 전 세계 박스오피스 순위의 중요한 일원이 되었습니다. 6. **국제 시장**: 영화의 국제 시장 인지도와 영향력이 지속적으로 증가하고 있으며, 특히 국제 영화제에서 많은 국제 영화제가 아직 진행 중입니다. 종합하면, 『너자2: 마동요해』의 흥행 성적은 국제 박스오피스에서 탁월하며, 국내에서 큰 성공을 거두었을 뿐 아니라 전 세계 박스오피스 순위의 중요한 지표가 되어 중국 영화의 국제 시장 돌파를 상징합니다.
[B]: 20자 요약: 20자의 거대한 성과는 중국 영화가 국제 시장에서 거둔 첫 돌파이며, 중국 영화의 국제 시장 돌파를 상징합니다.
[C]: 『어느 길이 가치 있는가(哪行是值得的)』는 2021년 1월 9일 14시 31분, 영화 『어떻게 대성할까(哪成大作为)』가 영화 시장에서 7800억 달러를 돌파하여 중국 애니메이션 영화의 돌파가 되었으며, 중국 애니메이션 영화의 거대한 잠재력과 시장 매력을 보여 줍니다.
[D]: 저는 파라미터가 아주 적은 AI 모델이라🥺 지식 베이스가 부족해서 질문에 바로 답할 수 없어요. 다른 질문을 해 보세요👋
```

🙋‍ 위의 모든 질문과 모델의 답변을 GPT-5.4 Thinking에 그대로 던져 주고, 논평과 순위 채점을 부탁했습니다:

<details>
<summary>구체적인 논평</summary>

```text
### 채점 기준:

- **정확성(30점)**: 답변의 사실이 올바른지, 명백한 지식 오류나 환각이 있는지.
- **완전성(30점)**: 답변이 질문의 핵심 요점을 다루는지, 충분히 전개되었는지.
- **논리성(20점)**: 답변이 조리 있고 앞뒤가 일관되는지, 자기모순이나 의미 혼란이 없는지.
- **코드 품질(20점)**: 코드가 올바르게 실행되는지, 구현 논리가 명확한지 (코드 문제에만 채점).

### 모델별 논평:

1. **A 모델 (minimind-3, 0.06B)**:
    - **장점**: 생성량이 충분하고, 이 파라미터 규모에서 전개 능력이 이미 괜찮은 편. 코드 문제에서 구조가 완전하고 실행 가능한 퀵 정렬 구현을 내놓아 이번 라운드에서 가장 좋은 코드 답변 중 하나. 에베레스트 문제도 핵심 정보를 대체로 맞힘.
    - **단점**: 사실 오류가 꽤 밀집되어 있음 — 만유인력을 아인슈타인의 공으로 돌리고, 창장을 "중국의 공식 명칭"으로 묘사하며, 바닷물 염도 설명은 과학적 사실에서 완전히 벗어남("빛 산란", "햇빛 반사" 등 언급). 요약 문제에서 20자 제한을 따르지 않고 장황하게 전개함. 대왕판다 답변은 대나무를 맞히긴 했지만 6개 요점이 전부 "대나무"의 반복 변형이라 정보 밀도가 매우 낮음.
    - **총평**: 어느 정도의 생성 및 코드 능력은 있으나 지식 정확성이 치명적 약점이며 환각 문제가 두드러짐. 답변에서 "그럴듯해 보이지만 자세히 보면 전부 지어낸" 현상이 자주 나타남.

2. **B 모델 (minimind-3-moe, 0.2B-A0.06B)**:
    - **장점**: 답변 구조가 비교적 명확하고, 문장의 매끄러움이 네 모델 중 가장 좋음. 코드 문제 구현이 정확하고 예시 출력까지 첨부했으며 설명도 꽤 적절함. 에베레스트 문제 답변이 정확함. 요약 문제는 글자 수를 초과했지만 적어도 "중국 영화", "국제 시장 돌파"라는 두 핵심어는 잡아냄.
    - **단점**: 지식 오류 역시 매우 뚜렷함 — 창장을 곧바로 "에베레스트산"으로 묘사하고, 만유인력을 아인슈타인에게 돌리며, 대왕판다의 먹이에 "해산물, 어류, 조류" 등 심각한 사실 오류가 등장함. 바닷물 염도 설명은 "삼투압" 주위를 반복해서 맴돌 뿐 핵심 원인에 닿지 못함.
    - **총평**: MoE 구조 덕분에 표현의 유창성과 구조감이 더 좋지만, 정확성 문제는 A 모델과 비슷함. 종합하면 "그럴듯하게 쓰는가"라는 차원에서는 앞서지만 "올바르게 쓰는가"에서는 본질적 우위가 없음.

3. **D 모델 (chatlm-mini-chinese, 0.2B)**:
    - **장점**: 지식 질의응답 성능이 가장 탄탄함 — 창장 묘사가 대체로 정확(발원지, 거치는 성·구, 동중국해로 유입)하고, 만유인력을 정확히 뉴턴에게 돌리며 1687년 『자연철학의 수학적 원리』를 인용했고, 대왕판다의 주식이 대나무라는 것도 맞혔으며, 바닷물 염도 설명도 처음에는 정확했음(염화나트륨, 용해된 염류). 전반적 가독성이 좋고 명백한 논리 단절이 나타나지 않음.
    - **단점**: 코드 문제에서 판단 조건을 거꾸로 써서(`len(arr) > 1: return arr`) 함수가 전혀 작동하지 않음. 요약 문제는 아예 답변을 포기함("저는 파라미터가 아주 적은 AI 모델이라"). 에베레스트와 바닷물 염도 답변 후반부에서 모두 뚜렷한 반복 퇴화 현상이 나타남.
    - **총평**: 지식 보유량이 네 모델 중 가장 좋고 사실형 질의응답에서 확실히 앞서지만, 코드 능력이 약점이며 생성 후반부에 반복 루프로 퇴화하기 쉬움.

4. **C 모델 (baby-llama2-chinese, 0.2B)**:
    - **장점**: 에베레스트 문제 답변이 간결하고 정확하며, 대왕판다의 주식이 대나무라는 것도 맞혀서 아주 기본적인 사실 문제에서는 어느 정도 능력이 있음을 보여 줌.
    - **단점**: 창장 문제는 완전히 동문서답("중국은 세계에서 가장 긴 도시"), 만유인력은 뉴턴을 언급하긴 했지만 설명이 혼란스럽고 자기 반복적이며, 바닷물 문제는 동문서답(물의 생물학적 역할을 이야기함), 코드 문제는 전혀 쓸 수 없는 코드(`sorted_print(sorted(sorted(...)))`)를 출력했고, 요약 문제는 정보가 심각하게 뒤죽박죽("어느 길이 가치 있는가", "7800억 달러").
    - **총평**: 기초 언어 능력이 명백히 부족하며, 대부분의 답변이 동문서답이거나 정보가 심각하게 왜곡되어 이번 평가에서 전반적으로 최하위.

### 요약:

- **B 모델**: 표현이 가장 유창하고 코드가 정확하며 구조감이 가장 좋지만, 지식 환각이 심각함(창장=에베레스트, 대왕판다가 해산물을 먹음). "매끄럽게 쓰는 것"과 "올바르게 쓰는 것" 사이의 격차가 큼.
- **D 모델**: 지식 정확성이 가장 높고 사실형 질의응답에서 가장 안정적이지만, 코드 능력이 뚜렷한 약점이며 생성 후반부에 반복 퇴화하기 쉬움.
- **A 모델**: B와 스타일이 비슷하고 코드도 쓸 만하지만, 전체 안정성이 B만 못하고 지식 오류 밀도도 높은 편.
- **C 모델**: 기초 능력이 부족하여 대부분의 답변을 쓸 수 없으며, 가장 간단한 사실 문제에서만 가끔 맞힘.

```

</details>

| 순위 | 모델 | 정확성 (30점) | 완전성 (30점) | 논리성 (20점) | 코드 품질 (20점) | 총점 (100점) |
|----|----|-----------|-----------|-----------|------------|-----------|
| 1  | B  | 11        | 23        | 16        | 18         | 68        |
| 2  | D  | 25        | 19        | 15        | 3          | 62        |
| 3  | A  | 10        | 21        | 13        | 17         | 61        |
| 4  | C  | 8         | 6         | 5         | 2          | 21        |


### 👉 종합 평가 2

주관적인 체감으로는 `minimind-3-moe`를 1위, `chatlm-mini-chinese`를 2위, `minimind-3`를 3위, `baby-llama2-chinese`를 4위로 놓겠습니다. `B`는 지식 정확성 면에서 환각이 심각하지만(대왕판다가 해산물을 먹음), 표현이 유창하고 구조가 명확하며 코드 문제 구현이 정확하다는 점에서 종합 출력 품질이 가장 높습니다. `D`는 지식 보유량이 확실히 앞서지만(뉴턴 1687년, 창장 발원지 등 모두 정확), 코드 문제의 조건을 거꾸로 써서 전혀 쓸 수 없고 요약 문제도 아예 포기해 점수를 많이 깎아 먹었습니다. `A`는 `B`와 스타일이 비슷하고 코드도 쓸 만하지만, 안정성과 지식 정확성 모두 `B`만 못해서 "뭐든 한두 마디는 하지만 자세히 보면 전부 지어낸" 전형에 속합니다. `C`는 사실성, 전개 능력, 전반적 가독성 모두에서 뚜렷한 격차가 있으며, 가장 간단한 사실 문제에서만 가끔 맞힙니다. 주목할 점은 `D`와 `A`의 총점이 매우 비슷하지만(62 vs 61), 강점과 약점의 분포는 거의 상호 보완적이라는 것입니다. `D`는 지식 정확성에서 이기고(25 vs 10), `A`는 코드 능력에서 이깁니다(17 vs 3). 이는 소형 파라미터 모델의 전형적인 현상을 반영하기도 합니다. 제한된 파라미터 예산 안에서 "말을 잘하는 것"과 "말을 맞게 하는 것"을 동시에 갖추기는 어려운 경우가 많습니다.

---

## Ⅳ RoPE 길이 외삽

MiniMind는 YaRN 알고리즘을 통한 RoPE 위치 인코딩의 길이 외삽을 지원하여, 학습 길이를 넘는 텍스트 시퀀스도 더 안정적으로 처리할 수 있습니다.

네이티브 torch 모델로 `eval_llm.py` 추론을 할 때는 `--inference_rope_scaling` 인자만 추가하면 RoPE 외삽이 활성화됩니다:

```bash
python eval_llm.py --weight full_sft --inference_rope_scaling
```

`Transformers` 형식 모델의 경우 `config.json`에 다음 설정을 추가하면 길이 외삽을 구현할 수 있습니다:

```json
"rope_scaling": {
    "type": "yarn",
    "factor": 16.0,
    "original_max_position_embeddings": 2048,
    "beta_fast": 32.0,
    "beta_slow": 1.0,
    "attention_factor": 1.0
}
```

아래는 MiniMind를 예로, 길이가 서로 다른 『서유기』 현대어 텍스트를 입력으로 사용해 RoPE scaling 활성화 전후의 퍼플렉서티(PPL) 변화를 비교한 것입니다. 긴 텍스트 상황에서 YaRN 외삽을 활성화하면 모델의 PPL이 뚜렷하게 낮아지는 것을 볼 수 있습니다:

<div align="center">
<img src="./images/rope_ppl.png">
</div>

> 텍스트 길이별 MiniMind의 YaRN 활성화 전후 PPL 비교

---

## Ⅴ 객관적 평가

이제 모두가 좋아하는 `benchmark` 시간입니다. 여기서는 몇몇 초소형 모델을 골라 횡적 비교를 했으며, 테스트셋으로 C-Eval, CMMLU, ARC-Easy, PIQA, OpenBookQA, HellaSwag, Social-IQa를 선택했습니다(앞의 2개를 제외하면 모두 영어 데이터셋).


평가 프레임워크는 [lm-evaluation](https://github.com/EleutherAI/lm-evaluation-harness)을 사용했습니다.

```bash
# 설치
git clone https://github.com/EleutherAI/lm-evaluation-harness
cd lm-evaluation-harness && pip install -e .
```



```bash
# 테스트 실행
# 사용한 데이터셋: ceval-valid/cmmlu/arc_easy/piqa/openbookqa/hellaswag/social_iqa # 지원 데이터셋 확인: lm_eval ls tasks 
# 지시(instruct) 모델은 평가 시 --apply_chat_template를 추가해야 하며, gpt2 같은 순수 베이스 모델은 필요 없습니다.
HF_ENDPOINT=https://hf-mirror.com lm_eval --model hf --model_args pretrained="/path/to/model",dtype=auto --tasks "task" --batch_size 16 --device cpu --trust_remote_code --apply_chat_template
```

> 참고: 이런 객관식 평가는 보통 모델이 완전한 답을 자유롭게 생성하게 하는 것이 아니라, 문제 문맥 `y`와 여러 후보 `x`가 주어지면 각 후보의 조건부 확률 `p(x | y)`를 직접 비교해 확률이 가장 큰 후보를 예측 결과로 삼습니다. 후보가 단일 token에만 대응한다면 그 token의 예측 확률을 바로 비교하면 되고, 후보가 여러 token으로 나뉜다면 후보 전체의 조건부 로그 확률 합을 비교하는 것이 더 일반적입니다. 여기서 후보가 꼭 `A`, `B`, `C`, `D`인 것은 아니며, 일부 데이터셋은 선택지가 두 개뿐일 수도 있습니다. 따라서 결과로 보면 무작위로 답했을 때의 정확도가 상당히 강한 하한선인 경우가 많고, 이 규모의 모델은 실제로 오랫동안 그 근처를 맴돕니다.

MiniMind의 데이터 규모는 표의 다른 모델들보다 훨씬 작고 학습 비중이 중국어에 치우쳐 있어 영어 성능이 좋지 않습니다. 또한 기본적으로 이런 객관식 평가 형식에 맞춘 정렬 미세조정을 따로 하지 않았기 때문에 성능이 상대적으로 약하며, 결과는 재미로만 봐 주세요:

| model name | from | params | zh (ceval / cmmlu) | en (arc / piqa / obqa / hellaswag / siqa) |
|---|---|---|---|---|
| minimind-3 | current | 64M | 24.89 / 25.38 | 28.49 / 50.65 / 23.60 / 28.28 / 34.19 |
| minimind-3-moe | current | 198M | 25.48 / 24.32 | 27.74 / 50.71 / 26.20 / 27.43 / 34.03 |
| minimind-3-exam | current | 64M | 30.98 / 26.12 | 35.61 / 56.26 / 24.20 / 28.40 / 34.19 |
| [Steel-LLM](https://huggingface.co/gqszhanshijin/Steel-LLM) | ZhanShiJin | 1121M | 24.89 / 25.32 | 39.69 / 65.13 / 26.00 / 35.73 / 39.15 |
| [gpt2-medium](https://huggingface.co/openai-community/gpt2-medium) | OpenAI | 360M | 23.18 / 25.00 | 43.60 / 66.38 / 30.20 / 39.38 / 39.10 |
| [TinyLlama-1.1B](https://huggingface.co/TinyLlama/TinyLlama-1.1B-Chat-v1.0) | TinyLlama | 1100M | 25.71 / 25.03 | 54.80 / 74.43 / 35.60 / 60.38 / 43.09 |
| [SmolLM2-135M](https://huggingface.co/HuggingFaceTB/SmolLM2-135M-Instruct) | HuggingFace | 135M | 24.44 / 24.71 | 58.50 / 68.17 / 32.80 / 43.15 / 39.46 |
| [Aquila-135M](https://huggingface.co/BAAI/Aquila-135M-Instruct) | BAAI | 135M | 25.19 / 25.10 | 54.59 / 67.52 / 34.40 / 41.67 / 39.66 |

> **이 표의 해상도**: `lm_eval`은 각 지표마다 `stderr`를 함께 출력하는데, 이는 주로 테스트셋 크기에 의해 결정되므로 아래 수치는 표의 모든 모델에 대략 적용됩니다(정확도에 따라 약간 변동):
>
> | 데이터셋 | obqa | ceval | piqa | siqa | arc | hellaswag | cmmlu |
> |---|---|---|---|---|---|---|---|
> | 샘플 수 | 500 | ~1.3k | 1838 | 1954 | 2376 | 10042 | 11582 |
> | ± 표준오차 | **1.9** | 1.2 | 1.2 | 1.1 | 0.9 | 0.5 | **0.4** |
>
> 두 모델을 비교할 때 차이의 표준오차는 단일 항목의 약 `√2`배입니다. 따라서 obqa에서 약 5%p 미만, ceval / piqa / siqa에서 약 3%p 미만의 차이는 두 모델을 구분하기에 충분하지 않습니다. 이는 이 표에서 같은 규모의 모델 순위를 과도하게 해석하지 말아야 하는 이유이기도 합니다.

<details>
<summary><strong>보충 설명 (출처/오염 없음/재현)</strong></summary>

minimind-3-exam은 더 큰 베이스 모델이 아니며, 새로운 지식을 추가로 주입한 것도 거의 없습니다. minimind-3를 기반으로 [lora_exam.jsonl](https://huggingface.co/datasets/jingyaogong/minimind_dataset/blob/main/lora_exam.jsonl)에서 가벼운 LoRA 정렬을 한 번 수행한 뒤, [lora_exam_768.pth](https://huggingface.co/jingyaogong/minimind-3-pytorch/resolve/main/lora_exam_768.pth)를 베이스 모델에 다시 병합한 결과일 뿐입니다. 이 데이터는 ceval과 mmlu(영어)의 test 부분집합에서 샘플링해 구성했으며, 접두사·접미사 등의 형식 증강을 했습니다. 주된 역할은 문제의 답을 학습하는 것이 아니라, 객관식 평가에서 흔히 쓰이는 문맥과 후보 구성 형식에 맞추는 것입니다.

이 절의 평가에 사용한 7개 데이터셋은 위의 정렬 데이터와 샘플 교집합이 없으므로 데이터 오염은 없다고 볼 수 있습니다. 반대로 교집합이 있는 데이터로 직접 미세조정하면 이런 소형 모델의 점수가 크게 왜곡되는 경우가 많습니다. 예를 들어 minimind-3는 오염된 ceval / cmmlu 부분집합에서 실험적으로 약 97%의 정확도까지 나온 적이 있지만, 그런 결과는 참고 가치가 없습니다.

이 실험이 말하고자 하는 것은 단지 이것입니다. 이런 평가에서 소형 모델의 병목은 반드시 지식 자체에만 있는 것이 아니라 입력 형식이 맞지 않는 데 있을 수도 있습니다. 소량의 형식 정렬만으로 minimind-3-exam은 위 7개 작업에서 평균 약 2.9%p 향상되었습니다.

</details>

![benchmark_radar](./images/benchmark_radar.jpg)

# 📌 기타

## 🔧 모델 변환

* [./scripts/convert_model.py](./scripts/convert_model.py)는 `torch / transformers` 두 모델 형식 간의 상호 변환에 사용할 수 있습니다.
* 별도 언급이 없으면 `MiniMind` 메인라인으로 공개되는 오픈소스 모델은 보통 `Transformers` 형식으로 제공됩니다. 네이티브 `torch` 가중치를 사용한다면 먼저 `torch2transformers` 변환을 실행하세요.


## 🖥️ MiniMind 기반 API 서비스 인터페이스

* [./scripts/serve_openai_api.py](./scripts/serve_openai_api.py)는 OpenAI API와 호환되는 경량 채팅 서비스를 제공하여, 자신의 모델을 FastGPT, OpenWebUI, Dify 등 서드파티 UI에 쉽게 연결할 수 있게 합니다.
* 현재 인터페이스는 `reasoning_content`, `tool_calls`, `open_thinking` 등의 필드를 추가로 지원하여 Tool Calling / Thinking 시나리오에 바로 사용하기 적합합니다.

* [HuggingFace](https://huggingface.co/collections/jingyaogong/minimind-66caf8d999f5c7fa64f399e5)에서 모델 가중치를 내려받은 후의 디렉터리 구조 예시는 다음과 같습니다:
    ```
    minimind (root dir)
    ├─<MiniMind-Model-Name> (예: minimind-3)
    |  ├── config.json
    |  ├── generation_config.json
    |  ├── model_minimind.py (선택, 모델 내보내기 방식에 따라 다름)
    |  ├── pytorch_model.bin or model.safetensors
    |  ├── special_tokens_map.json
    |  ├── tokenizer_config.json
    |  ├── tokenizer.json
    ```

* 서버 실행
    ```bash
    cd scripts && python serve_openai_api.py
    ```
* 서비스 인터페이스 테스트
    ```bash
    cd scripts && python chat_api.py
    ```
* API 요청 예시 (OpenAI API 형식 호환)
    ```bash
    curl http://localhost:8998/v1/chat/completions \
      -H "Content-Type: application/json" \
      -d '{ 
        "model": "model-identifier",
        "messages": [ 
          { "role": "user", "content": "세계에서 가장 높은 산은 무엇인가요?" }
        ], 
        "temperature": 0.7, 
        "max_tokens": 1024,
        "stream": true,
        "open_thinking": true
    }'
    ```

## <img src="https://avatars.githubusercontent.com/u/147780389?s=48&v=4" height="28" style="vertical-align: middle;"/> [SGLang](https://github.com/sgl-project/sglang)

SGLang은 고성능 대형 모델 추론 엔진으로, RadixAttention, 연속 배칭 등의 최적화 기술을 지원하며 낮은 지연 시간과 높은 처리량을 제공합니다.

> ⚠️ CUDA 환경이 필요하며, 필요에 따라 사용하세요. RL 학습 스크립트에서 SGLang을 rollout / 추론 엔진으로 선택해 학습 처리량을 높일 수도 있습니다.

OpenAI-compatible API server 형태로 모델 실행:

```bash
python -m sglang.launch_server --model-path /path/to/model --attention-backend triton --host 0.0.0.0 --port 8998
```

## <img src="https://avatars.githubusercontent.com/u/136984999" height="28" style="vertical-align: middle;"/> [vllm](https://github.com/vllm-project/vllm)

vLLM은 현재 매우 널리 쓰이는 효율적인 추론 프레임워크로, 대형 모델을 빠르게 배포하기에 적합하며 GPU 메모리 활용률과 처리량 사이에서 좋은 균형을 이룹니다.

> ⚠️ CUDA 환경이 필요하며, 필요에 따라 사용하세요.

OpenAI-compatible API server 형태로 모델 실행:

```bash
vllm serve /path/to/model --model-impl transformers --served-model-name "minimind" --port 8998
```

## <img src="https://user-images.githubusercontent.com/1991296/230134379-7181e485-c521-4d23-a0d6-f7b3b61ba524.png" height="28" style="vertical-align: middle;"/> [llama.cpp](https://github.com/ggerganov/llama.cpp)

llama.cpp는 가볍고 실용적인 C++ 추론 프레임워크로, 명령줄에서 바로 사용할 수 있고 멀티스레드 추론을 지원하며 일부 GPU 가속 방안도 지원합니다.

**디렉터리 구조**: `llama.cpp`와 모델 디렉터리를 같은 레벨 경로에 두는 것을 권장합니다

```
parent/
├── project/           # 여러분의 프로젝트 디렉터리
│   ├── minimind 모델 경로/      # HuggingFace 형식 모델 디렉터리
│   │   ├── config.json
│   │   ├── model.safetensors
│   │   └── ...
│   └── ...
└── llama.cpp/         # llama.cpp 프로젝트 디렉터리
    ├── build/
    ├── convert_hf_to_gguf.py
    └── ...
```

0. `llama.cpp` 공식 문서를 참고해 설치를 완료합니다(`cmake` 등 의존성 포함)

1. `convert_hf_to_gguf.py`의 `get_vocab_base_pre` 함수 끝에 다음을 삽입합니다:

```python
# MiniMind tokenizer 지원 추가 (여기서는 qwen2 같은 호환 항목을 임시로 재사용할 수 있음)
if res is None:
    res = "qwen2"
```

2. HuggingFace 형식의 minimind 모델을 GGUF로 변환합니다:

```bash
# llama.cpp 디렉터리에서 실행하면 모델 디렉터리에 해당 gguf 파일이 생성됩니다
python convert_hf_to_gguf.py /path/to/minimind-model
```

3. 모델 양자화 (선택)

```bash
./build/bin/llama-quantize /path/to/model/xxxx.gguf /path/to/model/xxxx.q8.gguf Q8_0
```

4. 명령줄 추론 테스트

```bash
./build/bin/llama-cli -m /path/to/model/xxxx.gguf
```

## <img src="https://ollama.com/public/cloud.png" height="28" style="vertical-align: middle;"/> [ollama](https://ollama.ai)

Ollama는 대형 모델을 로컬에서 실행하는 데 흔히 쓰이는 도구로, 다양한 오픈소스 LLM을 지원하며 사용 방식이 간결하고 배포 문턱이 낮습니다.

1. Ollama로 커스텀 GGUF 모델 로드하기

모델 디렉터리에 `minimind.modelfile` 파일을 새로 만들고, 다음 설정 템플릿을 작성합니다:

<details>
<summary>minimind.modelfile (template)</summary>

```text
FROM /path/to/model/xxxx.gguf

SYSTEM "你的名字叫MiniMind，你是一个乐于助人、知识渊博的AI助手。请用完整且友好的方式回答用户问题，当被问到名字时请回答MiniMind。"


TEMPLATE """{{- if .Tools }}<|im_start|>system
{{ if .System }}{{ .System }}

{{ end }}# Tools

You may call one or more functions to assist with the user query.

You are provided with function signatures within <tools></tools> XML tags:
<tools>
{{- range .Tools }}
{"type": "function", "function": {{ .Function }}}
{{- end }}
</tools>

For each function call, return a json object with function name and arguments within <tool_call></tool_call> XML tags:
<tool_call>
{"name": <function-name>, "arguments": <args-json-object>}
</tool_call><|im_end|>
{{ else if .System }}<|im_start|>system
{{ .System }}<|im_end|>
{{ end }}
{{- range $i, $_ := .Messages }}
{{- $last := eq (len (slice $.Messages $i)) 1 -}}
{{- if eq .Role "user" }}<|im_start|>user
{{ .Content }}<|im_end|>
{{ else if eq .Role "assistant" }}<|im_start|>assistant
<think>
{{ .Thinking }}
</think>

{{ .Content }}
{{- if .ToolCalls }}
{{- range .ToolCalls }}
<tool_call>
{"name": "{{ .Function.Name }}", "arguments": {{ .Function.Arguments }}}
</tool_call>
{{- end }}
{{- end }}
{{- if not $last }}<|im_end|>
{{ end }}
{{- else if eq .Role "tool" }}<|im_start|>user
<tool_response>
{{ .Content }}
</tool_response><|im_end|>
{{ end }}
{{- if and (ne .Role "assistant") $last }}<|im_start|>assistant
{{ if and $.IsThinkSet $.Think -}}
<think>
{{ else -}}
<think>

</think>

{{ end -}}
{{ end }}
{{- end }}"""

PARAMETER repeat_penalty 1
PARAMETER stop "<|im_start|>"
PARAMETER stop "<|im_end|>"
PARAMETER temperature 0.9
PARAMETER top_p 0.9
PARAMETER num_ctx 8192
```

> 위 `SYSTEM` 프롬프트의 의미: "너의 이름은 MiniMind이고, 너는 기꺼이 돕는 박식한 AI 어시스턴트다. 사용자 질문에 완전하고 친절한 방식으로 답하고, 이름을 물으면 MiniMind라고 답하라." (모델이 중국어 위주로 학습되었으므로 원문 그대로 두었습니다)

</details>
<br/>


2. 로컬 모델 로드 및 이름 지정

```bash
ollama create -f minimind.modelfile minimind-local
```

3. 추론 시작

```bash
ollama run minimind-local
```

<details>
<summary>📤 모델을 Ollama Hub에 푸시하기</summary>

```bash
# 1. 로컬 모델의 이름을 `ollama-account/minimind` 형식의 tag로 변경
ollama cp minimind-local:latest your_username/minimind:latest

# 2. 모델 푸시
ollama push your_username/minimind:latest
```
</details>
<br/>

⭐️ 제가 제공하는 Ollama 모델로 바로 빠르게 시작할 수도 있습니다:

```bash
ollama run jingyaogong/minimind-3
>>> 你叫什么名字
我是一个语言模型...
```

> (위 대화: "이름이 뭐야" → "저는 언어 모델입니다...")

## <img src="https://avatars.githubusercontent.com/u/1961952?s=48&v=4" height="28" style="vertical-align: middle;"/> [MNN](https://github.com/alibaba/MNN)

MNN은 엣지 디바이스용 AI 추론 엔진으로, 다양한 오픈소스 LLM의 경량화 배포와 고성능 추론을 지원합니다.

1. 모델 변환
```bash
cd MNN/transformers/llm/export
# 4-bit HQQ 양자화된 MNN 모델 내보내기
python llmexport.py --path /path/to/모델경로/ --export mnn --hqq --dst_path 모델경로-mnn
```

2. Mac 또는 휴대폰에서 테스트
```bash
./llm_demo /path/to/모델경로-mnn/config.json prompt.txt
```
또는 APP을 내려받아 테스트할 수 있습니다

> 위 서드파티 프레임워크의 더 많은 사용법은 각 공식 문서를 참고하세요😊


## 👨‍💻 더 많은 내용

* <a href="https://github.com/jingyaogong/minimind/discussions/618">🔗MiniMind-LLM으로 확산 언어 모델 미세조정하기</a>

* <a href="https://github.com/jingyaogong/minimind/discussions/611">🔗모델의 generate 메서드 설명</a>

* <a href="https://github.com/jingyaogong/minimind/discussions/704">🔗MiniMind로 선형 어텐션 모델 학습하기</a>

# 📌 감사의 말

> [!NOTE]
> `MiniMind` 시리즈 프로젝트가 도움이 되셨다면 GitHub에서 ⭐를 눌러 주세요<br/>
> 문서 분량이 길어 빠진 부분이 있을 수 있으니, Issues로 의견을 주시거나 PR을 제출해 함께 프로젝트를 개선해 주세요<br/>
> 여러분의 지지와 제안이 이 프로젝트가 계속 발전하는 중요한 원동력입니다!

## 🤝[기여자](https://github.com/jingyaogong/minimind/graphs/contributors)

<a href="https://github.com/jingyaogong/minimind/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=jingyaogong/minimind" />
</a>

## 😊 감사

학습 기록, 데이터 처리, 튜토리얼 정리, 프로젝트 분해 등에서 도움과 공유를 해 주신 다음 기여자분들께 감사드립니다:

* [@ipfgao](https://github.com/ipfgao): [🔗학습 단계 기록](https://github.com/jingyaogong/minimind/issues/26)

* [@WangRongsheng](https://github.com/WangRongsheng): [🔗대규모 데이터셋 전처리](https://github.com/jingyaogong/minimind/issues/39)

* [@pengqianhan](https://github.com/pengqianhan): [🔗간단명료한 튜토리얼](https://github.com/jingyaogong/minimind/issues/73)

* [@RyanSunn](https://github.com/RyanSunn): [🔗추론 과정 학습 기록](https://github.com/jingyaogong/minimind/issues/75)

* [@Nijikadesu](https://github.com/Nijikadesu): [🔗인터랙티브 노트북 방식으로 프로젝트 코드 분해](https://github.com/jingyaogong/minimind/issues/213)

* [@jaylearnstocode](https://github.com/jaylearnstocode): [🔗모델 구조, 어텐션 메커니즘, 학습 과정 시각화](https://llm-visualization-minimind.vercel.app/)


다음의 훌륭한 논문과 프로젝트에 감사드립니다:

- [https://github.com/meta-llama/llama3](https://github.com/meta-llama/llama3)
- [https://github.com/karpathy/llama2.c](https://github.com/karpathy/llama2.c)
- [https://github.com/DLLXW/baby-llama2-chinese](https://github.com/DLLXW/baby-llama2-chinese)
- [DeepSeek-V2](https://arxiv.org/abs/2405.04434)
- [https://github.com/charent/ChatLM-mini-Chinese](https://github.com/charent/ChatLM-mini-Chinese)
- [https://github.com/wdndev/tiny-llm-zh](https://github.com/wdndev/tiny-llm-zh)
- [Mistral-MoE](https://arxiv.org/pdf/2401.04088)
- [https://github.com/Tongjilibo/build_MiniLLM_from_scratch](https://github.com/Tongjilibo/build_MiniLLM_from_scratch)
- [https://github.com/jzhang38/TinyLlama](https://github.com/jzhang38/TinyLlama)
- [https://github.com/AI-Study-Han/Zero-Chatgpt](https://github.com/AI-Study-Han/Zero-Chatgpt)
- [https://github.com/xusenlinzy/api-for-open-llm](https://github.com/xusenlinzy/api-for-open-llm)
- [https://github.com/HqWu-HITCS/Awesome-Chinese-LLM](https://github.com/HqWu-HITCS/Awesome-Chinese-LLM)


## 🫶 후원자

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://bytecrank.com/nastyox/reporoster/php/forkersSVG.php?user=jingyaogong&repo=minimind&theme=dark"/>
  <source media="(prefers-color-scheme: light)" srcset="https://bytecrank.com/nastyox/reporoster/php/forkersSVG.php?user=jingyaogong&repo=minimind"/>
  <img alt="Fork poster" src="https://bytecrank.com/nastyox/reporoster/php/forkersSVG.php?user=jingyaogong&repo=minimind&theme=dark"/>
</picture>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/chart?repos=jingyaogong/minimind&type=date&theme=dark&legend=top-left&sealed_token=DK6jy_uvw2AHIK0S4VZLf6snWIQ06jGzz3QiwVmXBGDvickcQgJGSdazdGxjRQZuj8Hr3GfS_REB9ohoK8NWVsmukeOQiT4soChw3_19yyPVwvWzBp66yMYWlvOYy9sv60cMSntByiUTcyp4MrRiMm1JD1MSC8NJ-Z9qhR9uJGl2AU7w-OGlyKQzN7Xa"/>
  <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/chart?repos=jingyaogong/minimind&type=date&legend=top-left&sealed_token=DK6jy_uvw2AHIK0S4VZLf6snWIQ06jGzz3QiwVmXBGDvickcQgJGSdazdGxjRQZuj8Hr3GfS_REB9ohoK8NWVsmukeOQiT4soChw3_19yyPVwvWzBp66yMYWlvOYy9sv60cMSntByiUTcyp4MrRiMm1JD1MSC8NJ-Z9qhR9uJGl2AU7w-OGlyKQzN7Xa"/>
  <img alt="Star History Chart" src="https://api.star-history.com/chart?repos=jingyaogong/minimind&type=date&legend=top-left&sealed_token=DK6jy_uvw2AHIK0S4VZLf6snWIQ06jGzz3QiwVmXBGDvickcQgJGSdazdGxjRQZuj8Hr3GfS_REB9ohoK8NWVsmukeOQiT4soChw3_19yyPVwvWzBp66yMYWlvOYy9sv60cMSntByiUTcyp4MrRiMm1JD1MSC8NJ-Z9qhR9uJGl2AU7w-OGlyKQzN7Xa"/>
</picture>

## 🎉 MiniMind 관련 성과

이 모델이 마중물이 되어 몇몇 반가운 성과가 실현되었습니다. 연구자분들의 인정에 감사드립니다:

- ECG-Expert-QA: A Benchmark for Evaluating Medical Large Language Models in Heart Disease Diagnosis [[arxiv](https://arxiv.org/pdf/2502.17475)]

- Binary-Integer-Programming Based Algorithm for Expert Load Balancing in Mixture-of-Experts Models [[arxiv](https://arxiv.org/pdf/2502.15451)]

- LegalEval-Q: A New Benchmark for The Quality Evaluation of LLM-Generated Legal Text [[arxiv](https://arxiv.org/pdf/2505.24826)]

- On the Generalization Ability of Next-Token-Prediction Pretraining [[ICML 2025](https://openreview.net/forum?id=hLGJ1qZPdu)]

- 『처음부터 만드는 대형 모델: 신경망에서 Transformer까지(从零开始写大模型：从神经网络到Transformer)』 왕솽(王双), 머우천(牟晨), 왕하오이(王昊怡) 편저 - 칭화대학교 출판사

- FedBRB: A Solution to the Small-to-Large Scenario in Device-Heterogeneity Federated Learning [[TMC 2025](https://ieeexplore.ieee.org/abstract/document/11168259)]

- SKETCH: Semantic Key-Point Conditioning for Long-Horizon Vessel Trajectory Prediction [[arxiv](https://arxiv.org/pdf/2601.18537)]

- A Built-in Crypto Expert for Artificial Intelligence: How Far is the Horizon? [[IACR ePrint 2026](https://eprint.iacr.org/2026/411.pdf)]

- RetryTrigger: Intelligent Inference Duplication for Enhancing LLM Resilience to Hardware Transient Faults [[FITEE 2026](https://ieeexplore.ieee.org/abstract/document/11479682)]

- 진행 중...


# 🎓 인용

`MiniMind`가 연구나 업무에 도움이 되셨다면 인용해 주세요:

```bibtex
@misc{minimind,
  title = {MiniMind: Train a Tiny LLM from Scratch},
  author = {Jingyao Gong},
  year = {2024},
  url = {https://github.com/jingyaogong/minimind},
  note = {GitHub repository, accessed 2026}
}
```

# ⚖️ 오픈소스 라이선스

본 프로젝트는 [Apache License 2.0](LICENSE) 오픈소스 라이선스를 따릅니다.
