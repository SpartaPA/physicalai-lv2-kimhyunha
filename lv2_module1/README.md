# 모듈 1 — 임베디드 제어기초

## 장비·환경

- 라즈베리파이: Ubuntu 22.04.5 LTS(Jammy), 아키텍처 aarch64
- 호스트명 pak / 사용포트 /dev/ttyACM0 — [results/환경확인.txt](results/환경확인.txt) 참고
- 제어기: OpenCR 1.0 (USB로 라즈베리파이에 직접연결, PC는 SSH접속 전용)
- 모터: 다이나믹셀 XM430-W350 (모델 1020), ID 12, 1 Mbps, Protocol 2.0, 1개
- 펌웨어: 제공된 사전 빌드 바이너리 `opencr_position_p.ino.bin`
  ([firmware/README.md](../reference/모듈1_임베디드제어기초/firmware/README.md), SHA-256 `c68eddf221d60cfc61767d1937120db2f3d74445dcc5d30b851d5be850df4f7f`)
- 예제소스: [opencr_position_p.ino](../reference/모듈1_임베디드제어기초/examples/opencr_position_p/opencr_position_p.ino) — 수정없이 그대로 사용함

## 실행방법

1. PC에서 라즈베리파이로 SSH접속. OpenCR은 라즈베리파이에 USB로 연결.
2. 라즈베리파이에서 [OpenCR 빌드·업로드 가이드](../reference/모듈1_임베디드제어기초/OpenCR_빌드_업로드_가이드.md) 8~9단계대로 포트확인 후 제공펌웨어 업로드, `CRC OK` / `[OK] Download` 나오는지 확인.
3. 시리얼모니터로 `READY` 준비상태 확인.
4. `s <Kp> <speed_deg_s> <angle_deg>` 형식으로 목표입력(실행A: `s 1 30 20`). 시작하고 2초뒤에 목표로 이동함, `x`누르면 정지.
5. 시리얼 출력을 라즈베리파이에서 로그파일로 저장하고, `x` 입력 후 `STOP: user` 응답까지 확인. (문제3용으로 Kp만 2로 바꿔서 한번 더 실행 → 실행B, `s 2 30 20`, 마찬가지로 `x`·`STOP:` 확인)

## 결과파일 위치

| 파일 | 내용 |
|---|---|
| [results/환경확인.txt](results/환경확인.txt) | 호스트명, Ubuntu 버전, 아키텍처, 사용 포트 |
| [results/upload.log](results/upload.log) | 펌웨어 업로드 및 성공 확인 로그 |
| [results/실행A.log](results/실행A.log) | 문제1·2용, 목표 변경 이후 측정값과 `x`→`STOP: user` 정지 확인 로그 (Kp 1) |
| [results/실행B.log](results/실행B.log) | 문제3용, Kp만 바꿔서 재실행한 로그, 정지 확인 포함 (Kp 2) |

