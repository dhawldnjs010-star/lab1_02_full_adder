# 실험 후 레포트: LAB1-02 전가산기 (반가산기 두 개의 연결)

작성자: 엄상혁 (학번 ______) / 조: g조 / 실험일: 2026-09-14 / 소스 커밋: `c2c88f3` (https://github.com/dhawldnjs010-star/lab1_02_full_adder/commit/c2c88f380d5622390cde18cf3393613125fd0816) / 구현 도구·버전: Vivado 2026.1 (Build 6511674) / part: xc7s75fgga484-1 / top: `full_adder` (시뮬레이션 top `tb_full_adder`) / XDC: `constraints/pins.xdc`

경로: Vivado 경로로 수행했다.

## Vivado 시뮬레이션 — Vivado 경로

프로젝트 생성·등록: RTL(`src/half_adder.v, src/full_adder.v`)은 Design Sources, TB(`sim/tb_full_adder.sv`)는 Simulation Sources, XDC(`constraints/pins.xdc`)는 Constraints에 추가했다(Copy sources 끔). 설계 top은 `full_adder`, 시뮬레이션 top은 `tb_full_adder`이다.

| 실행 | PASS 문구 | 검사 수 | 종료 시각 | 로그 |
|---|---|---|---|---|
| VS Code (Icarus) | `LAB1_PASS full_adder cases=8` | 8개 | 80 ns | `evidence/simulation.txt` |
| Vivado xsim | `LAB1_PASS full_adder cases=8` | 8개 | 80 ns | `evidence/vivado/xsim_simulate.log` |

- Icarus와 Vivado xsim의 PASS 문구, 검사 수, 종료 시각이 같다.

- 파형: `evidence/wave.vcd`(Icarus VCD).

## 오픈소스 실행 환경 — CLI 경로

이 랩은 Vivado 경로로 수행했다. CLI 경로는 사용하지 않았다.

## 합성·구현·비트스트림

| 항목 | 결과 |
|---|---|
| Run Synthesis | 완료. `Synthesis finished with 0 errors, 0 critical warnings and 0 warnings.` |
| Run Implementation | 배치·배선 완료 |
| Generate Bitstream | `write_bitstream completed successfully` |
| DRC | Checks found: 1 — CFGBVS-1(Warning) |
| Methodology | Checks found: 0 |
| 타이밍 | WNS/WHS = inf, 실패 endpoint 0. 사용자 타이밍 제약이 없는 조합회로라 통과 수치가 아니다(`Timing 38-313`). |
| 경고 | `Place 46-29`, `Power 33-232`, `Timing 38-313` |

- bit 경로: `vivado/full_adder.runs/impl_1/full_adder.bit` (Git 제외) / 크기: 3,687,013 bytes / SHA-256: `2182ae5a3d7f0fa2584830f99799c0196f1b74c5c01f51a5d025e68fd7d18766`

- 보고서 원본: `evidence/vivado/`의 `synth_runme.log`, `impl_runme.log`, `drc_routed.rpt`, `methodology_drc_routed.rpt`, `timing_summary_routed.rpt`.

- DRC의 `CFGBVS-1`은 CONFIG_VOLTAGE·CFGBVS 속성이 지정되지 않았다는 경고이다. 실제 보드의 구성 뱅크 전압과 대조해 해석하며 오류는 아니다.

## 실제 보드 기록·실측

연결된 장치: Spartan-7 XC7S75 교육용 보드(part `xc7s75fgga484-1`), 기록 도구: Vivado Hardware Manager (Open target → Program Device). 콘솔 로그: `evidence/board/console_lab1_02_sanghyeok.txt`.

- Hardware Manager 콘솔에서 `program_hw_devices`가 2회 실행되었다.

- 배선·입력·출력이 보이는 영상: `evidence/board/videos/20260914_150235.mp4` (2026-09-14 15:02:35 촬영).


| 조건 | 예상 출력 | 실측 출력 | 사진/영상 시각 | 일치 여부·원인 |
|---|---|---|---|---|
| a=0 b=0 cin=0 | s=0 cout=0 | 예상 출력과 같음 | `20260914_150235.mp4` (2026-09-14 15:02:35) | 일치 |
| a=0 b=0 cin=1 | s=1 cout=0 | 예상 출력과 같음 | `20260914_150235.mp4` (2026-09-14 15:02:35) | 일치 |
| a=0 b=1 cin=0 | s=1 cout=0 | 예상 출력과 같음 | `20260914_150235.mp4` (2026-09-14 15:02:35) | 일치 |
| a=0 b=1 cin=1 | s=0 cout=1 | 예상 출력과 같음 | `20260914_150235.mp4` (2026-09-14 15:02:35) | 일치 |
| a=1 b=0 cin=0 | s=1 cout=0 | 예상 출력과 같음 | `20260914_150235.mp4` (2026-09-14 15:02:35) | 일치 |
| a=1 b=0 cin=1 | s=0 cout=1 | 예상 출력과 같음 | `20260914_150235.mp4` (2026-09-14 15:02:35) | 일치 |
| a=1 b=1 cin=0 | s=0 cout=1 | 예상 출력과 같음 | `20260914_150235.mp4` (2026-09-14 15:02:35) | 일치 |
| a=1 b=1 cin=1 | s=1 cout=1 | 예상 출력과 같음 | `20260914_150235.mp4` (2026-09-14 15:02:35) | 일치 |


실측은 작성자가 보드에서 직접 확인한 결과이다.

## 비교·결론

- 예상값(진리표) → VS Code(Icarus) `LAB1_PASS full_adder cases=8` → Vivado xsim `LAB1_PASS full_adder cases=8`: 검사 8개 모두 일치하고 종료 시각 80 ns로 같다.

- 실측: 위 표의 모든 조건에서 예상 출력과 같았다. 불일치는 없었다.

- 구현 성공(bit 생성)만으로 동작을 확인한 것으로 보지 않고, 위 실측 표를 별도로 확인했다.

## 제출 링크

소스 커밋: https://github.com/dhawldnjs010-star/lab1_02_full_adder/commit/c2c88f380d5622390cde18cf3393613125fd0816 / 실험 전 레포트: `reports/pre/lab1_02_pre_report.md` / 로그·VCD: `evidence/simulation.txt`, `evidence/wave.vcd`, `evidence/vivado/` / bit·해시: 위 3절 (SHA-256 `2182ae5a3d7f0fa2584830f99799c0196f1b74c5c01f51a5d025e68fd7d18766`) / 영상: `evidence/board/videos/20260914_150235.mp4` / GitHub에서 링크 확인한 날짜: ______
