# SSH chain band gap: midterm presentation, speaker notes

[Slides](slides/SSH_midterm_slides.pptx) (PowerPoint; import into Google Slides if needed)

15 main slides / 575 seconds (25 seconds spare); 7 backup slides. 이 파일은 말하기 단서(키워드)이며 대본이 아니다. 각 그림은 축, 비교, 변화, 물리적 의미의 순서로 설명한다. 슬라이드 8과 13에는 노트북 7절의 시연 셀을 짧게 실행한다(파일을 저장하지 않는다). Q&A는 이 시간 배분 밖이다.

## 1. Band Gap of the SSH Chain

발표 시간: 15초 | 구성: question

- 인사, SSH 사슬의 밴드갭
- tight-binding 모형은 수업 범위 밖 → 직접 공부해서 적용
- 행렬 대각화로 계산하고 검증

Sources
README.md (Physics question)

## 2. Motivation: from atoms to bands

발표 시간: 35초 | 구성: question

- N개 원자 → N개 준위 → 밴드 (왼쪽 그림)
- 빈 구간 = 갭 → 금속과 반도체를 가름
- 짧은 결합과 긴 결합이 번갈아 → 갭 (오른쪽은 모식도, 계산 아님)
- 가장 단순한 모형 = SSH 사슬 (1979, 폴리아세틸렌 설명용)

Sources
Notebook: tight_binding.ipynb §1 (monatomic chain), 직관 실험 table in the theory notes
W. P. Su, J. R. Schrieffer, A. J. Heeger, Phys. Rev. Lett. 42, 1698 (1979)
Figures: build/fig_levels_N.png, build/fig_dimerization.png (schematic)

## 3. Question and quantities

발표 시간: 25초 | 구성: question

- 질문 하나: t2/t1에 따른 갭, 유한 사슬의 수렴
- 계산할 양 3개: 밴드, 갭, 유한 사슬의 최소 |E|
- 범위 = 밴드갭

Sources
README.md (Physics question)

## 4. SSH model, assumptions, boundary conditions

발표 시간: 40초 | 구성: method

- tight-binding: 전자가 이웃 오비탈로 뛰어넘는 hopping만 고려 (수업 밖, 직접 공부)
- A, B 두 원자 / 굵은 선 t1(셀 안), 가는 선 t2(셀 사이), 점선 = 한 셀
- 가정: 최근접 hopping, 직교 오비탈, 온사이트 에너지 없음
- 경계: 주기(밴드), 열린(유한 사슬) / 규약: A에서 시작, 첫 결합 t1

Sources
Notebook: tight_binding.ipynb §2, §4
Figure: build/fig_ssh_chain.png (schematic)

## 5. Bloch Hamiltonian and the predicted gap

발표 시간: 30초 | 구성: method

- h = t1 + t2 e^{ika}, H = [[0, h*], [h, 0]], E± = ±|h|
- k = 0: t1 + t2 (가장 멂), k = π/a: |t1 − t2| (가장 가까움)
- 예측: 갭 = 2|t1 − t2| → 수치로 확인

Sources
Notebook: tight_binding.ipynb §2 (ssh_hamiltonian, ssh_bands)
Theory: Bloch Hamiltonian (backup 17, 18)

## 6. Quantities computed

발표 시간: 30초 | 구성: method

- 계산할 양 3개 / 갭 = 위 밴드 최솟값 − 아래 밴드 최댓값
- 오른쪽 행렬은 예시이지 결과 아님
- 열린 사슬은 Bloch 정리 불가 → 실공간 대각화

Sources
Notebook: tight_binding.ipynb §3 (band_gap, gap_numeric), §4 (finite_ssh)

## 7. Numerical workflow

발표 시간: 30초 | 구성: method

- 흐름: params.json → 대각화(2×2 per k, 2N×2N) → 해석식 비교 → 해상도 → output
- 선택 이유: 작아서 정확, 수렴 변수 없음
- 코드는 의사코드 / 난수 없음 → 같은 결과

Sources
Notebook: tight_binding.ipynb §0 (params.json), §2-§5
Input: input/params.json  Output: output/

## 8. Result: the gap depends on t1 − t2

발표 시간: 95초 | 구성: results

- 축: 가로 t2, 세로 갭 (t1 = 1) / 비교: 점(대각화) vs 회색선 2|t1 − t2|
- 변화: t2 = 0 → 2, t2 = 1 → 0, 1.5 → 1.0, 2 → 2.0 (브이)
- ▶ 시연 1 (노트북 §7 첫 셀): T2 = 0.5 → 0.9 → 1.0 → 1.5, 갭 1.000 → 0.200 → 0.000 → 1.000
- 오른쪽 위: (1, 0.5)와 (0.5, 1)의 밴드가 같음 → 갭은 t1과 t2의 차이로만 결정
- 의미: 셀당 전자 2개 → 아래 밴드 가득 → 절연체 또는 금속적
- 한계: hopping은 임의 단위, 실제 폴리아세틸렌 값 아님

Sources
Notebook: tight_binding.ipynb §2, §3
Figures: output/figs/fig4_gap_vs_t2.png, output/figs/fig3_bands_compare.png
Data: output/gap_vs_t2.csv, output/bands_ssh.csv

## 9. Validation: analytic comparison and limits

발표 시간: 50초 | 구성: results

- 왼쪽: 가로 k, 세로 E / 회색 = 해석식, × = 20원자 고리 대각화, 차이 1e-15
- 표: SSH 2.2e-16, 갭 2.4e-16
- 극한: t1 = t2 (단원자 고리와 같음), t2 → 0 (|E| = t1), t1 → 0 (E = 0 상태 2개, 끝 사이트 확률 1)
- 의미: 코드가 모형을 맞게 풂 ≠ 모형이 물질을 맞게 나타냄

Sources
Notebook: tight_binding.ipynb §1-2, §5-1
Figure: output/figs/fig2_ring_check.png
Summary: output/summary.json

## 10. Numerical resolution and sampling

발표 시간: 45초 | 구성: results

- 축: 가로 N_k / 원자 수 / 셀 수, 세로 오차
- k 격자: 짝수 → k = π 포함 → 0, 홀수 → 건너뜀 (t2 = 0.5, 17점: +0.033)
- 고리: 홀수 N → 꼭대기 부족
- 사슬 길이: 10, 20, 40 → 0.033, 0.010, 0.0028, 2배 → 1/4 → 1/N_c²
- 샘플링 해당 없음: 결정론적, 불확도 = 기계 정밀도

Sources
Notebook: tight_binding.ipynb §5-2, §5-3
Figure: output/figs/fig8_resolution.png
Data: output/resolution_kgrid_gap.csv, resolution_ring.csv, resolution_chain_gap.csv

## 11. Interpretation: why the gap opens

발표 시간: 50초 | 구성: interpretation

- 균일 사슬을 셀 2개로 세면 BZ 절반, 밴드 접힘 → k = π/a에서 만남
- t1 ≠ t2 → 주기 2배 섭동 → 갭 (1.2, 0.8이면 0.8)
- Peierls: 이론 인용, 증명하지 않음
- 전자 수: 단원자 사슬은 반만 참(금속), SSH는 아래 밴드 가득

Sources
Theory: zone folding and Peierls instability (cited, not derived here)
Figure: build/fig_folding.png (analytic bands, t1 = t2 = 1 and t1 = 1.2, t2 = 0.8)
R. E. Peierls, Quantum Theory of Solids (1955)

## 12. Limitations and how to check them

발표 시간: 45초 | 구성: interpretation

- 실제 폴리아세틸렌 hopping 안 씀 → 문헌 값으로 반복
- 160셀까지, 갭이 작으면(t2 = 0.9) 점근 아님 → 더 긴 사슬
- 갭 안 상태의 이유 못 설명 → 기말
- 2차원, 상호작용은 범위 밖 / 시작 원자 규약 의존

Sources
Notebook: tight_binding.ipynb §5-2, §6
Data: output/resolution_chain_gap.csv

## 13. Preliminary observation: states inside the gap

발표 시간: 45초 | 구성: conclusion

- 위: 에너지, 아래: 0에 가장 가까운 두 상태의 위치별 확률
- 왼쪽 t1 > t2: 0개 (가장 가까운 값 0.51) / 오른쪽 t2 > t1: 2개, 양 끝에 집중
- ▶ 시연 2 (노트북 §7 둘째 셀): (T1, T2, NC) = (1, 0.5, 20) → (0.5, 1, 20) → (0.5, 1, 5), 가장 작은 |E| 0.510 → 7.15e-07 → 2.35e-02
- 관찰만, 이유는 기말

Sources
Notebook: tight_binding.ipynb §4
Figure: output/figs/fig6_edge_states.png
Data: output/edge_states.csv, output/edge_density.csv

## 14. Outlook: what the final project will test

발표 시간: 15초 | 구성: conclusion

- 기말 계획 3개: 진폭과 길이 의존, 무질서(평균 ± 표준오차), 대칭
- 계획이지 새 결과 아님

Sources
Plan only; no new result is shown on this slide

## 15. Summary

발표 시간: 25초 | 구성: conclusion

- 갭 = 2|t1 − t2|, t1 = t2에서 닫힘
- 해석식과 1e-15 일치, 유한 사슬 1/N_c²
- 예비 관찰 → 후속 연구, 감사

Sources
output/summary.json

## 16. Backup: Bloch theorem and the Brillouin zone

백업 | 질문이 나오면 사용

- 질문: 왜 k를 한 구간만?
- 한 칸 이동 = 위상 e^{ika}, k ≡ k + 2π/a
- 각 k마다 작은 행렬 / 열린 사슬엔 불가

Sources
Theory notes ch. 2 (Bloch theorem)
Asbóth, Oroszlány, Pályi, A Short Course on Topological Insulators (2016), arXiv:1509.02295

## 17. Backup: derivation of H(k)

백업 | 질문이 나오면 사용

- 질문: 2×2는 어디서?
- A에 이어진 B: 같은 셀 t1, 왼쪽 셀 t2 e^{−ika}
- 에르미티안 → 반대 성분은 복소공액, 대각 0

Sources
Notebook: tight_binding.ipynb §2 (ssh_hamiltonian)

## 18. Backup: eigenvalues and the gap

백업 | 질문이 나오면 사용

- 질문: 에너지 유도
- det(H − E) = E² − |h|², |h|² = t1² + t2² + 2t1t2 cos ka
- 최소 (t1 − t2)² at k = π/a → 갭 = 2|t1 − t2|

Sources
Notebook: tight_binding.ipynb §2, §3

## 19. Backup: monatomic chain (reference)

백업 | 질문이 나오면 사용

- 질문: 단원자 사슬
- E = ε0 − 2t cos ka, 폭 4t, 반만 참 → 금속
- t1 = t2 극한과 같음 (차이 0)

Sources
Notebook: tight_binding.ipynb §1, §5-1

## 20. Backup: k-grid parity table

백업 | 질문이 나오면 사용

- 질문: k 점이 충분한가
- 짝수 N_k → k = π 포함 → 오차 0, 홀수 → 과대평가
- 갭이 작을수록 k 점 더 필요 (0.95: 17점 +0.273)

Sources
Notebook: tight_binding.ipynb §5-2 (gamma_grid, gap_on_grid)
Data: output/resolution_kgrid_gap.csv

## 21. Backup: finite-chain gap convergence

백업 | 질문이 나오면 사용

- 질문: 왜 1/N_c²?
- |h| ≈ |t1 − t2| + t1t2 q²/(2|t1 − t2|), q ~ π/N_c
- 계수 4.93, 배율 3.30 → 3.90 / t2 = 0.9는 아직 2.4~3.5

Sources
Notebook: tight_binding.ipynb §5-2 (bulk_edge_energy)
Data: output/resolution_chain_gap.csv

## 22. Backup: reproducibility and sources

백업 | 질문이 나오면 사용

- README: 질문, 환경, 실행, 입력, 그림, 검증, 출처
- Run All 약 10초, python project.py, manifest.json / 노트북 §7 = 발표용 시연 셀(파일 저장 안 함)
- AI(Claude) 사용 공개, 설명 책임은 발표자

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
- tight-binding은 수업에서 배웠나? 아니요, 수업 범위 밖이라 직접 공부해서 썼습니다. 수치 방법인 행렬 대각화는 수업에서 다룬 종류의 방법입니다 (슬라이드 1, 4).
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
