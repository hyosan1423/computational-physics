# SSH 사슬의 밴드갭 — Tight-Binding 계산 (전산물리학 중간 프로젝트)

## Physics question

> SSH 사슬에서 $t_2/t_1$에 따라 밴드갭은 어떻게 변하고, 끝이 있는 유한 사슬의 수치 계산은 그 값에 얼마나 잘 수렴하는가?

계산한 양: 밴드 $E_\pm(k)$와 갭 $E_{gap}$, 유한 사슬에서 가장 낮은 벌크 상태의 $\lvert E\rvert$, 그리고 (예비 관찰) 유한 사슬의 갭 안 상태.

**결론 (수치로 확인)**: 갭은 $E_{gap}=2\lvert t_1-t_2\rvert$이고 $t_1=t_2$에서 닫힌다. 수치 대각화는 해석식과 기계 정밀도($10^{-15}\sim10^{-16}$)로 일치하고, 열린 사슬의 갭은 셀 수 $N_c$에 대해 $1/N_c^2$로 이론값에 수렴한다. 예비 관찰로, $t_2>t_1$인 유한 사슬의 갭 안에는 $E\approx0$ 상태가 2개 있다 (원인은 이 프로젝트의 범위 밖).

모델: 단위셀에 A, B 두 원자, 셀 안 hopping $t_1$, 셀 사이 hopping $t_2$. 가정: 최근접 hopping만, 오비탈 직교, 온사이트 에너지 없음. 경계조건: 밴드와 $H(k)$는 주기, 유한 사슬은 열린 경계. 규약: 유한 사슬은 A 원자에서 시작하고 첫 결합이 $t_1$.

수치 방법: 행렬 대각화 (`numpy.linalg.eigh`). 행렬이 작아서(2×2, $2N\times2N$) 정확하고 시간 간격 같은 수렴 변수가 없다.

## Environment and dependencies

- Python 3.12.3, `numpy` 2.4.4, `matplotlib` 3.10.8 (그 외 패키지 없음)
- Jupyter 노트북 실행 환경 (VS Code + Jupyter 확장 또는 JupyterLab)

## How to run

1. `tight_binding.ipynb`를 열고 **Restart → Run All** (약 10초).
2. 결과(그래프, 출력)는 노트북에 이미 저장되어 있어서 실행하지 않아도 볼 수 있다.
3. 실행하면 `output/` 아래의 csv, json, 그림이 새로 쓰인다.

폴더 구성:

```
midterm-tight-binding/
├── README.md
├── tight_binding.ipynb       # 코드
├── input/params.json         # 입력: 계산 조건
└── output/
    ├── summary.json          # 핵심 수치
    ├── *.csv                 # 계산 결과
    └── figs/*.png            # 그림
```

## Inputs and parameters

모든 계산 조건은 `input/params.json`에 있다 (파일이 없으면 노트북이 기본값으로 만든다). 이 파일의 값만 바꾸고 다시 실행하면 결과가 바뀐다.

| 키 | 의미 | 기본값 |
|---|---|---|
| `t_monatomic` | 단원자 사슬 hopping $t$ | 1.0 |
| `ring_N` | 고리 원자 수 | 20 |
| `ssh_pairs` | 비교할 $(t_1,t_2)$ 쌍 | (1, 0.5), (0.5, 1) |
| `gap_scan` | 갭 스캔: $t_1$, $t_2$ 범위, 점 수 | $t_1=1$, $t_2\in[0,2]$, 81점 |
| `chain.n_cells` | 유한 사슬의 셀 수 | 20 |
| `chain.edge_threshold` | "영 근처"의 기준 $\lvert E\rvert$ | 0.1 |
| `resolution.nk_list` | $k$ 격자 점 수 목록 | 3 ~ 64 |
| `resolution.ring_N_list` | 고리 원자 수 목록 | 10 ~ 101 |
| `resolution.chain_gap_ncell_list` | 사슬 길이(셀 수) 목록 | 10 ~ 160 |

## How to reproduce the figures

| 그림 | 내용 | 노트북 절 |
|---|---|---|
| `fig1_monatomic.png` | 단원자 사슬 밴드 | 1 |
| `fig2_ring_check.png` | 고리 대각화 vs 해석식 | 1-2 |
| `fig3_bands_compare.png` | $(1,0.5)$와 $(0.5,1)$의 밴드 | 2 |
| `fig4_gap_vs_t2.png` | 갭 vs $t_2$ | 3 |
| `fig6_edge_states.png` | 유한 사슬의 스펙트럼과 위치별 확률 (예비 관찰) | 4 |
| `fig8_resolution.png` | $N_k$, 고리 원자 수, 사슬 길이에 따른 오차 | 5-2 |

## Validation and limitations

### 기준과의 비교 (정확한 결과, 극한 경우)

| 비교 | 결과 |
|---|---|
| 원자 20개 고리 $20\times20$ 대각화 vs 해석식 $\epsilon_0-2t\cos ka$ | 최대 차이 $1.1\times10^{-15}$ |
| SSH $2\times2$ 대각화 vs $\pm\lvert t_1+t_2e^{ika}\rvert$ | 최대 차이 $2.2\times10^{-16}$ |
| 수치 갭 vs $2\lvert t_1-t_2\rvert$ ($t_2\in[0,2]$) | 최대 차이 $2.4\times10^{-16}$, $t_2=t_1$에서 0 |
| 극한 $t_1=t_2$: SSH 고리 vs 같은 원자 수의 단원자 고리 | 스펙트럼 차이 0 |
| 극한 $t_2\to0$: 이합체만 남음 | 모든 $\lvert E\rvert=t_1$ |
| 극한 $t_1\to0$ (예비 관찰의 직관) | 끝 원자가 끊어져 $E=0$ 상태 정확히 2개, 끝 원자 확률 1.000 |

### 수치 해상도

| 바꾼 것 | 보는 양 | 결과 |
|---|---|---|
| $k$ 격자 점 수 $N_k$ | 갭 오차 | 짝수 $N_k$는 갭이 가장 작은 $k=\pi$를 지나 오차 0. 홀수는 과대평가 ($(1,0.5)$: $N_k=3$에서 $+0.73$, $17$에서 $+0.033$, $33$에서 $+0.009$) |
| 고리 원자 수 $N$ | 밴드 꼭대기와 $2t$의 차이 | 짝수 $N$은 $\sim10^{-16}$, 홀수 $N$은 $2t(1-\cos(\pi/N))$과 일치 ($N=11$: 0.081, $N=101$: $9.7\times10^{-4}$) |
| 유한 사슬의 셀 수 $N_c$ | 가장 낮은 벌크 $\lvert E\rvert$와 $\lvert t_1-t_2\rvert$의 차이 | $N_c=10,20,40,80,160$에서 $0.033,\ 0.010,\ 0.0028,\ 0.00073,\ 0.00019$ ($(1,0.5)$). 로그 기울기 $-1.92$ ($(1,0.5)$), $-2.03$ ($(0.5,1)$): $\propto1/N_c^2$ |

### 샘플링

이 프로젝트의 계산은 난수를 쓰지 않는 **결정론적 계산**이라 샘플링 불확도는 해당 없다. 수치 불확도는 기계 정밀도뿐이다.

### 예비 관찰 (원인은 다루지 않음)

$t_1>t_2$ 사슬은 $\lvert E\rvert<0.1$ 상태가 0개(가장 가까운 에너지 $\pm0.51$), $t_2>t_1$ 사슬은 2개이고 확률이 양 끝에 몰린다 (`fig6_edge_states.png`).

### 한계

| 확인하지 않은 것 | 확인 방법 |
|---|---|
| 실제 물질(폴리아세틸렌)의 $t_1, t_2$ | 문헌의 hopping 값으로 같은 계산 반복, 측정된 갭과 비교 |
| 사슬 길이 $N_c\le160$ 너머, 갭이 아주 작은 경우($(1,0.9)$는 아직 점근 영역 밖) | 더 긴 사슬로 $1/N_c^2$ 추세 확인 |
| 갭 안 상태가 유지되는 이유 | 별도 프로젝트에서 진폭 해석과 무질서 비교로 다룬다 |
| 2차원(그래핀), 전자 사이의 상호작용 | 이 모델의 범위 밖 |

규약: 유한 사슬은 A 원자에서 시작하고 첫 결합이 $t_1$이다. 이 규약을 바꾸면 갭 안 상태가 생기는 사슬이 뒤바뀐다.

## References and AI assistance

**AI 사용**: 이 프로젝트의 코드, 검증 설계, README, 발표 자료는 AI(Claude, Anthropic)가 전적으로 작성했다.

**참고 문헌** (이론 배경):
- W. P. Su, J. R. Schrieffer, A. J. Heeger, *Phys. Rev. Lett.* **42**, 1698 (1979)
- J. K. Asbóth, L. Oroszlány, A. Pályi, *A Short Course on Topological Insulators*, Springer (2016), arXiv:1509.02295
