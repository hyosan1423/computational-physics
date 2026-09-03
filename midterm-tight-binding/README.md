# 중간고사 프로젝트 — SSH 모델 기반 1차원 토폴로지 절연체

Tight-binding 모델(SSH, Su-Schrieffer-Heeger)의 밴드구조와 Zak phase(위상 불변량)를
수치적으로 계산하고, bulk-boundary correspondence(edge state 존재)를 검증하는 프로젝트입니다.

## 환경
- Python 3.13.9
- 필요 패키지: numpy, matplotlib, scipy
- 실행 환경: VS Code + Jupyter 확장 (base 커널)

## 실행 방법
1. `tight_binding.ipynb`를 VS Code 또는 Jupyter에서 엽니다.
2. 상단 메뉴에서 Restart → Run All로 처음부터 순서대로 실행합니다.
3. 순서대로 다음 결과가 출력됩니다:
   - SSH 모델 밴드구조 $E_\pm(k)$
   - $t_1, t_2$ 스캔에 따른 Zak phase (0 또는 π 양자화 확인)
   - 유한 사슬(open boundary)에서의 edge state 시각화
