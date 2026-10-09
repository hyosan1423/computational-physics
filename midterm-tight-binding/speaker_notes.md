# SSH chain band gap: midterm presentation, speaker notes

[Slides](slides/SSH_midterm_slides.pptx) (PowerPoint; import into Google Slides if needed)

15 main slides / 600 seconds; 7 backup slides. 대본은 외워서 말하는 완전 대본이며, 슬라이드의 그림은 축, 비교, 변화, 물리적 의미의 순서로 설명한다.

## 1. Band Gap of the SSH Chain

발표 시간: 10초 | 구성: question

안녕하세요, 신효산입니다. SSH 사슬의 밴드갭에 대해 발표하겠습니다. 수업에서 배운 tight-binding 계산을 직접 검증했습니다.

Sources
README.md (Physics question)

## 2. Motivation: from atoms to bands

발표 시간: 30초 | 구성: question

원자를 N개 이으면 준위도 N개로 갈라지고, N이 커지면 촘촘히 모여 밴드가 됩니다. 왼쪽이 그 준위입니다. 밴드 사이의 빈 구간이 갭이고, 갭이 금속과 반도체를 가릅니다. 오른쪽은 폴리아세틸렌처럼 짧은 결합과 긴 결합이 번갈아 나오는 사슬의 모식도로, 이 패턴이 갭을 엽니다. 이것을 가장 단순하게 만든 모형이 SSH 사슬입니다. 오른쪽은 개념도이고 계산 결과가 아닙니다.

Sources
Notebook: tight_binding.ipynb §1 (monatomic chain), 직관 실험 table in the theory notes
W. P. Su, J. R. Schrieffer, A. J. Heeger, Phys. Rev. Lett. 42, 1698 (1979)
Figures: build/fig_levels_N.png, build/fig_dimerization.png (schematic)

## 3. Question and quantities

발표 시간: 20초 | 구성: question

질문은 하나입니다. t2 나누기 t1에 따라 갭은 어떻게 변하고, 유한한 사슬의 수치 계산은 그 값에 얼마나 수렴하는가. 계산할 양은 밴드, 갭, 유한 사슬에서 에너지 절댓값이 가장 작은 상태입니다. 이번 범위는 밴드갭입니다.

Sources
README.md (Physics question)

## 4. SSH model, assumptions, boundary conditions

발표 시간: 30초 | 구성: method

모형입니다. 단위셀마다 A, B 두 원자가 있고, 굵은 선이 셀 안의 hopping t1, 가는 선이 셀 사이의 hopping t2, 점선 상자가 한 셀입니다. 이웃한 원자 사이에만 hopping이 있고 오비탈은 직교하며 원자 자체의 에너지는 없다고 둡니다. 밴드는 주기 경계, 유한 사슬은 열린 경계로 계산하고, A 원자에서 시작해 첫 결합이 t1인 규약을 씁니다. t1, t2는 임의의 단위입니다.

Sources
Notebook: tight_binding.ipynb §2, §4
Figure: build/fig_ssh_chain.png (schematic)

## 5. Bloch Hamiltonian and the predicted gap

발표 시간: 30초 | 구성: method

에너지입니다. 각 k의 2 곱하기 2 행렬은 대각이 0이고 비대각이 t1 더하기 t2 곱하기 e의 i k a승입니다. 고유값은 이 크기의 플러스 마이너스입니다. k가 0이면 t1 더하기 t2로 가장 멀고, k가 파이 나누기 a이면 t1 빼기 t2의 절댓값으로 가장 가깝습니다. 그래서 갭은 2 곱하기 t1 빼기 t2의 절댓값일 것으로 예측되고, 이것을 수치로 확인합니다.

Sources
Notebook: tight_binding.ipynb §2 (ssh_hamiltonian, ssh_bands)
Theory: Bloch Hamiltonian (backup 17, 18)

## 6. Quantities computed

발표 시간: 30초 | 구성: method

계산하는 양은 세 가지입니다. 밴드, 갭, 그리고 유한 사슬에서 에너지 절댓값이 가장 작은 상태입니다. 갭은 위 밴드의 최솟값에서 아래 밴드의 최댓값을 뺀 값입니다. 오른쪽은 셀이 둘인 사슬의 행렬 모양으로, 예시이지 계산 결과가 아닙니다. 끝이 있으면 Bloch 정리를 쓸 수 없어서 이 실공간 행렬을 그대로 대각화합니다.

Sources
Notebook: tight_binding.ipynb §3 (band_gap, gap_numeric), §4 (finite_ssh)

## 7. Numerical workflow

발표 시간: 30초 | 구성: method

수치 방법입니다. 입력은 params.json이고, 각 k에서 2 곱하기 2 행렬을, 유한 사슬은 2N 곱하기 2N 행렬을 대각화합니다. 행렬이 작아 정확하고 수렴 변수가 없어서 골랐습니다. 결과를 해석식과 비교하고 해상도를 바꿔 확인한 뒤 output에 저장합니다. 아래 코드는 의사코드입니다. 난수가 없어 다시 돌려도 같은 결과입니다.

Sources
Notebook: tight_binding.ipynb §0 (params.json), §2-§5
Input: input/params.json  Output: output/

## 8. Result: the gap depends on t1 − t2

발표 시간: 90초 | 구성: results

핵심 결과입니다. 축, 비교 조건, 변화, 물리적 의미의 순서로 설명하겠습니다. 왼쪽 큰 그림의 가로축은 t2, 세로축은 갭이고, t1은 1로 고정했습니다. 회색 선이 식 2 곱하기 t1 빼기 t2의 절댓값, 점이 t2마다 대각화해서 잰 값이고 점이 선 위에 놓입니다. 변화는 이렇습니다. t2가 0이면 갭이 2이고, t2가 1에 가까워질수록 줄어서 t2가 t1과 같은 1일 때 정확히 0이 되며, 1을 넘으면 다시 늘어나 t2가 1.5이면 1.0, 2이면 2.0인 브이 모양입니다. 오른쪽 위 그림은 t1이 1, t2가 0.5인 사슬과 t1이 0.5, t2가 1인 사슬의 밴드입니다. 두 사슬의 밴드 모양이 같습니다. k가 0일 때 에너지가 t1 더하기 t2이고 k가 파이일 때 t1 빼기 t2의 절댓값인데, t1과 t2를 바꿔도 이 값들이 변하지 않기 때문입니다. 의미는 두 가지입니다. 갭은 t1과 t2의 차이로만 정해지고, 셀당 전자가 둘이라 아래 밴드가 정확히 가득 차므로 갭이 열려 있으면 절연체이고 닫히면 금속적입니다. 이 계산은 hopping을 임의의 단위로 둔 것이라 실제 폴리아세틸렌의 갭 값을 말하지는 않습니다.

Sources
Notebook: tight_binding.ipynb §2, §3
Figures: output/figs/fig4_gap_vs_t2.png, output/figs/fig3_bands_compare.png
Data: output/gap_vs_t2.csv, output/bands_ssh.csv

## 9. Validation: analytic comparison and limits

발표 시간: 80초 | 구성: results

다음은 구현이 맞는지 확인하는 검증입니다. 왼쪽 그림의 가로축은 k, 세로축은 에너지입니다. 회색 곡선이 해석식이고 엑스 표시가 원자 스무 개를 고리로 이은 20 곱하기 20 행렬을 직접 대각화한 값인데, 엑스가 곡선 위에 놓이고 차이는 10의 마이너스 15승, 기계 정밀도입니다. 표의 나머지도 같은 방식입니다. SSH의 2 곱하기 2 대각화는 해석식과 2.2 곱하기 10의 마이너스 16승, 갭은 2 곱하기 t1 빼기 t2의 절댓값과 2.4 곱하기 10의 마이너스 16승 이내로 일치합니다. 답이 알려진 극한도 확인했습니다. t1과 t2가 같으면 같은 원자 수의 단원자 고리와 스펙트럼이 같고, t2가 0이면 이합체만 남아 모든 에너지의 절댓값이 t1이며, t1이 0이면 끝 원자 둘이 이웃과 끊어져 에너지가 정확히 0인 상태가 둘 생기고 끝 사이트의 확률이 1입니다. 이 검증은 코드가 이 모형을 맞게 푼다는 것을 보이고, 모형이 실제 물질을 맞게 나타내는지는 보이지 않습니다.

Sources
Notebook: tight_binding.ipynb §1-2, §5-1
Figure: output/figs/fig2_ring_check.png
Summary: output/summary.json

## 10. Numerical resolution and sampling

발표 시간: 70초 | 구성: results

수치 해상도는 세 가지를 바꿔 봤습니다. 가로축이 각각 k 격자 점 수, 고리의 원자 수, 사슬의 셀 수이고 세로축은 오차입니다. 왼쪽, k 격자 점이 짝수이면 갭이 가장 작은 k인 파이를 격자가 정확히 지나서 오차가 0이고, 홀수이면 그 점을 건너뛰어 갭을 크게 잡습니다. t1이 1, t2가 0.5이고 점이 17개이면 오차가 0.033입니다. 가운데, 고리의 원자 수가 홀수이면 밴드 꼭대기가 이론식만큼 모자랍니다. 오른쪽, 열린 사슬에서 가장 낮은 벌크 상태의 에너지가 이론값에서 벗어나는 정도가 셀 수 10, 20, 40에서 0.033, 0.010, 0.0028이고, 셀 수가 두 배가 되면 오차가 약 4분의 1로 줄어 셀 수의 제곱에 반비례합니다. 샘플링은 해당이 없습니다. 이 계산은 난수를 쓰지 않는 결정론적 계산이라 불확도는 기계 정밀도뿐입니다.

Sources
Notebook: tight_binding.ipynb §5-2, §5-3
Figure: output/figs/fig8_resolution.png
Data: output/resolution_kgrid_gap.csv, resolution_ring.csv, resolution_chain_gap.csv

## 11. Interpretation: why the gap opens

발표 시간: 60초 | 구성: interpretation

해석입니다. t1과 t2가 같은 사슬은 원자 간격이 균일한 단원자 사슬입니다. 왼쪽 그림처럼 이것을 셀 두 개짜리로 다시 세면 브릴루앙 영역이 절반으로 줄고 밴드가 접혀서, k가 파이 나누기 a인 곳에서 두 밴드가 에너지 0으로 만납니다. 가운데 그림입니다. t1과 t2가 다르면 주기가 두 배가 되는 섭동이 이 만나는 점을 밀어 갈라 갭이 열리고, 오른쪽에서 t1이 1.2, t2가 0.8이면 갭이 0.8입니다. 균일한 사슬이 스스로 짝을 짓는 경향을 Peierls 불안정성이라고 하며 폴리아세틸렌이 반도체인 이유로 알려져 있지만, 이것은 이론에서 인용한 설명이고 제가 증명하거나 계산하지는 않았습니다. 전자 수도 중요합니다. 단원자 사슬은 원자당 전자가 하나라 밴드가 반만 차서 금속이고, 이 사슬은 셀당 전자가 둘이라 아래 밴드가 가득 찹니다.

Sources
Theory: zone folding and Peierls instability (cited, not derived here)
Figure: build/fig_folding.png (analytic bands, t1 = t2 = 1 and t1 = 1.2, t2 = 0.8)
R. E. Peierls, Quantum Theory of Solids (1955)

## 12. Limitations and how to check them

발표 시간: 60초 | 구성: interpretation

한계입니다. 확인하지 않은 것과 그것을 확인하는 방법을 표로 말씀드립니다. 첫째, 실제 폴리아세틸렌의 hopping 값으로는 계산하지 않았습니다. 문헌 값으로 같은 계산을 반복해 측정된 갭과 비교하면 됩니다. 둘째, 사슬 길이는 160셀까지 확인했습니다. t1이 1, t2가 0.9처럼 갭이 작은 사슬은 셀 수를 두 배로 해도 오차가 4분의 1이 아니라 2.4분의 1에서 3분의 1 수준이라 아직 점근 영역에 들어오지 못했으므로, 더 긴 사슬로 확인해야 합니다. 셋째, 갭 안 상태가 유지되는 이유는 설명하지 못했고 기말에서 다룹니다. 넷째, 2차원과 전자 사이의 상호작용은 이 모형의 범위 밖입니다. 그리고 유한 사슬이 어느 원자에서 시작하느냐에 따라 상태가 생기는 사슬이 바뀌는 규약 의존이 있습니다.

Sources
Notebook: tight_binding.ipynb §5-2, §6
Data: output/resolution_chain_gap.csv

## 13. Preliminary observation: states inside the gap

발표 시간: 20초 | 구성: conclusion

예비 관찰입니다. 위는 유한 사슬의 에너지, 아래는 0에 가장 가까운 두 상태의 위치별 확률입니다. t1이 큰 왼쪽 사슬은 0 근처 상태가 없고, t2가 큰 오른쪽 사슬은 갭 안에 상태가 둘 있고 확률이 양 끝에 몰려 있습니다. 이유는 기말에서 다룹니다.

Sources
Notebook: tight_binding.ipynb §4
Figure: output/figs/fig6_edge_states.png
Data: output/edge_states.csv, output/edge_density.csv

## 14. Outlook: what the final project will test

발표 시간: 20초 | 구성: conclusion

기말에서는 이 상태가 무엇이고 언제 유지되는지 검증합니다. 진폭이 안쪽으로 줄어드는 모양과 사슬 길이 의존성, 무질서에 따른 변화를 평균과 표준오차로, 그리고 이를 설명하는 대칭을 계산합니다. 이것은 계획이고 새 결과가 아닙니다.

Sources
Plan only; no new result is shown on this slide

## 15. Summary

발표 시간: 20초 | 구성: conclusion

정리하겠습니다. 갭은 2 곱하기 t1 빼기 t2의 절댓값이고 t1과 t2가 같을 때 닫힙니다. 수치는 해석식과 기계 정밀도로 일치하고 유한 사슬의 갭은 셀 수 제곱에 반비례해 수렴합니다. 예비 관찰로 갭 안 상태가 나타났고, 후속 연구에서 이유를 검증하겠습니다. 감사합니다.

Sources
output/summary.json

## 16. Backup: Bloch theorem and the Brillouin zone

백업 | 질문이 나오면 사용

질문: 왜 k를 한 구간만 보는가? 결정이 간격 a로 반복되면 고유상태는 평면파와 같은 주기의 함수의 곱이고, 한 칸 옮기면 위상 e의 i k a승만 곱해진다. k와 k 더하기 2 파이 나누기 a는 같은 상태라서 k를 마이너스 파이 나누기 a에서 파이 나누기 a 사이에서만 구별한다. 이 덕분에 각 k마다 단위셀 크기의 작은 행렬만 대각화하면 된다. 증명은 평이동 연산자가 해밀토니안과 교환한다는 데서 나온다. 끝이 있는 사슬에는 쓸 수 없다.

Sources
Theory notes ch. 2 (Bloch theorem)
Asbóth, Oroszlány, Pályi, A Short Course on Topological Insulators (2016), arXiv:1509.02295

## 17. Backup: derivation of H(k)

백업 | 질문이 나오면 사용

질문: 2 곱하기 2 행렬은 어디서 나오는가? 단위셀에 원자가 둘이라 상태가 둘이다. A 원자에 이어진 B는 같은 셀의 B, 세기 t1이고, 왼쪽 셀의 B, 세기 t2이고 위상이 e의 마이너스 i k a승이다. 그래서 한 성분이 t1 더하기 t2 곱하기 e의 마이너스 i k a승이고, 에르미티안 조건으로 반대쪽 성분은 그 복소공액이 된다. 같은 종류의 원자 사이에는 hopping이 없고 온사이트 에너지를 두지 않으므로 대각은 0이다. 노트북은 비대각의 위치를 반대로 쓰는데 복소공액이라 고유값은 같다.

Sources
Notebook: tight_binding.ipynb §2 (ssh_hamiltonian)

## 18. Backup: eigenvalues and the gap

백업 | 질문이 나오면 사용

질문: 에너지를 유도해 보라. 행렬식 det(H − E)가 E 제곱 빼기 비대각 성분의 크기 제곱이므로 E는 플러스 마이너스 그 크기이다. 크기의 제곱은 t1 제곱 더하기 t2 제곱 더하기 2 t1 t2 코사인 k a이고, 코사인이 1일 때 최대인 t1 더하기 t2의 제곱, 마이너스 1일 때 최소인 t1 빼기 t2의 제곱이다. 최소는 k가 파이 나누기 a에서 나오고 갭은 그 두 배다. t1과 t2를 바꿔도 이 식이 변하지 않으므로 갭과 밴드가 같다.

Sources
Notebook: tight_binding.ipynb §2, §3

## 19. Backup: monatomic chain (reference)

백업 | 질문이 나오면 사용

질문: 균일한 단원자 사슬은 어떻게 되는가? 에너지는 ε0 빼기 2t 코사인 k a이고 밴드 폭은 4t이다. 브릴루앙 영역에 k가 N개, 스핀 포함 자리가 2N개인데 전자는 N개라서 밴드가 반만 차고 금속이다. 셀을 두 개로 세면 밴드가 접히는 출발점이 되고, SSH에서 t1과 t2가 같은 극한이 이 사슬과 같다는 것을 5-1에서 스펙트럼 차이 0으로 확인했다.

Sources
Notebook: tight_binding.ipynb §1, §5-1

## 20. Backup: k-grid parity table

백업 | 질문이 나오면 사용

질문: k 점이 충분한가? k 격자를 2 파이 j 나누기 N_k로 만들면 N_k가 짝수일 때 j가 N_k의 절반에서 k가 정확히 파이라서 갭 오차가 0이다. 홀수이면 파이를 건너뛰고 파이에서 파이 나누기 N_k 떨어진 점의 값을 읽어 갭을 크게 잡는다. 표에서 갭이 0.1로 작은 t2 0.95는 같은 점 수에서 갭이 1인 0.5보다 오차가 훨씬 크므로, 갭이 작을수록 k 점을 더 촘촘히 잡아야 한다.

Sources
Notebook: tight_binding.ipynb §5-2 (gamma_grid, gap_on_grid)
Data: output/resolution_kgrid_gap.csv

## 21. Backup: finite-chain gap convergence

백업 | 질문이 나오면 사용

질문: 왜 오차가 셀 수의 제곱에 반비례하는가? k가 파이에서 q만큼 떨어진 곳에서 크기는 대략 t1 빼기 t2의 절댓값 더하기 t1 t2 나누기 2 곱하기 t1 빼기 t2의 절댓값 곱하기 q 제곱이다. 열린 사슬에서 가장 낮은 q는 파이 나누기 셀 수 정도이므로 오차는 N_c 제곱에 반비례하고, t1이 1, t2가 0.5이면 계수가 4.93이다. 표에서 이 계수가 맞는 극한으로 배율이 4에 다가가는 것을 볼 수 있다. 갭이 작은 t2 0.9는 배율이 아직 2.4에서 3.5라 점근 영역 밖이다.

Sources
Notebook: tight_binding.ipynb §5-2 (bulk_edge_energy)
Data: output/resolution_chain_gap.csv

## 22. Backup: reproducibility and sources

백업 | 질문이 나오면 사용

가이드의 재현성과 AI 공개 항목에 대응한다. README에 질문, 환경, 실행법, 입력, 그림 재현, 검증과 한계, 출처와 AI 도움을 적었다. 노트북은 Restart Kernel and Run All로 약 10초에 전체가 다시 실행되고, python project.py로 같은 결과를 스크립트로 만든다. 입력은 input/params.json, 결과는 output 폴더이고 파일 해시는 manifest.json에 있다. 코드, 검증 설계, README, 발표 자료는 AI인 Claude가 작성했고, 저는 모형과 코드와 결과와 한계를 설명할 책임이 있다. 출처는 Su, Schrieffer, Heeger 1979와 Asbóth 등 2016이다.

Sources
README.md
manifest.json, provenance.json, requirements.txt

## Q&A 대비 (답을 먼저, 그다음 근거)

- H(k)는 어디서 나오나? 단위셀에 원자가 둘이라 2×2이고, 성분은 hopping에 위상을 곱해 더한 것입니다 (백업 17).
- 왜 k를 한 구간만 보나? k와 k+2π/a가 같은 상태이기 때문입니다 (백업 16).
- 갭은 어디서 나오나? k=π/a에서 두 밴드가 가장 가깝고 그 간격이 2|t₁−t₂|입니다 (백업 18).
- 코드가 맞는다는 증거는? 해석식과 극한(t₁=t₂, t₂→0, t₁→0)에서 일치합니다 (슬라이드 9).
- k 점이 충분한가? 짝수 격자는 k=π를 지나 정확하고, 홀수 격자는 갭이 작을수록 더 필요합니다 (백업 20).
- 샘플링 오차는? 난수를 쓰지 않는 결정론적 계산이라 해당 없습니다 (슬라이드 10).
- 갭 안 상태가 왜 생기나? 아직 설명하지 못했습니다. 관찰까지이고 기말에서 다룹니다 (슬라이드 13, 14).
- 정확히 0이 아닌 이유는? 사슬이 유한해서 두 끝이 약하게 섞이기 때문이고, 길수록 0에 가까워집니다 (셀 5, 10, 20에서 2.4e-02, 7.3e-04, 7.2e-07).
- 실제 물질에 적용되나? 이 계산만으로는 아닙니다. 문헌의 hopping 값으로 반복해야 합니다 (슬라이드 12).

## 부록: 질문이 나오면 쓰는 확인 셀

노트북을 Restart → Run All 한 뒤 맨 아래에 붙여 넣어 쓴다. 파일을 저장하지 않는다.

```python
# t2 를 바꾸면 갭이 어떻게 변하나 (예상: 1.000, 0.200, 0.000, 1.000)
for t2 in (0.5, 0.9, 1.0, 1.5):
    print(f"t1=1.0, t2={t2}: 갭 = {gap_numeric(1.0, t2):.3f}")

# 홀수 k 격자의 갭 오차 (예상: t2=0.5 → +0.033, t2=0.95 → +0.273)
for t2 in (0.5, 0.95):
    print(t2, [f"{gap_on_grid(1.0, t2, gamma_grid(nk)) - band_gap(1.0, t2):+.3f}" for nk in (16, 17, 33)])

# 영 근처 에너지와 사슬 길이 (예상: 2.35e-02, 7.32e-04, 7.15e-07)
for nc in (5, 10, 20):
    E = np.sort(np.abs(np.linalg.eigvalsh(finite_ssh(nc, 0.5, 1.0))))
    print(nc, f"{E[0]:.2e}")
```
