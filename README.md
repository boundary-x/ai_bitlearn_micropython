# bitlearn 라이브러리

![Micro:bit](https://img.shields.io/badge/platform-micro%3Abit-blue?logo=microbit)

> **코드 출처**: [ElecFreaks Ring:bit MicroPython](https://github.com/elecfreaks/EF_Produce_MicroPython/blob/master/Ringbit.py)

`bitlearn`은 Micro:bit 기반 Ring:bit 보드를 제어하기 위한 MicroPython 라이브러리입니다.  
양쪽 바퀴(또는 다리) 제어, 초음파 거리 측정, 라인트레이서 상태 확인 등의 기능을 제공합니다.

---

## 📦 주요 기능

- 좌우 모터(다리) 속도 제어
- 초음파 센서를 통한 거리 측정
- 아날로그 입력을 통한 라인 트레이서 판별

---

## 🔧 클래스: `bitlearn`

### 생성자

```python
bitlearn(left_wheel_pin=pin1, right_wheel_pin=pin2)
```

- `left_wheel_pin`: 왼쪽 모터 제어 핀 (기본값: `pin1`)
- `right_wheel_pin`: 오른쪽 모터 제어 핀 (기본값: `pin2`)

---

### 메서드

#### `set_motors_speed(left_wheel_speed: int, right_wheel_speed: int)`

좌우 모터의 속도를 설정합니다.

- 속도 범위: `-100` ~ `100`
- `0`은 정지, 음수는 반대 방향 회전

```python
rb.set_motors_speed(50, 50)  # 전진
rb.set_motors_speed(-50, -50)  # 후진
```

---

#### `get_distance(unit: int = 0) -> float`

초음파 센서를 사용하여 거리 측정.

- `unit = 0` : 센티미터(cm) 반환 (기본값)
- `unit = 1` : 인치(inch) 반환

```python
distance_cm = rb.get_distance()
distance_inch = rb.get_distance(unit=1)
```

---

#### `get_tracking() -> int`

라인 트레이서 상태를 판별합니다.

| 반환값 | 설명                  |
|--------|-----------------------|
| 0      | 양쪽 모두 흰색 위에 있음 |
| 1      | 왼쪽 흰색, 오른쪽 검정 |
| 10     | 왼쪽 검정, 오른쪽 흰색 |
| 11     | 양쪽 모두 검정 위에 있음 |
| -1     | 알 수 없는 오류         |

---

## 🧪 예제 코드

```python
from microbit import *
from bitlearn import bitlearn

rb = bitlearn(pin1, pin2)

while True:
    rb.set_motors_speed(50, 50)  # 앞으로 이동
    sleep(1000)
    rb.set_motors_speed(0, 0)    # 멈춤
    sleep(1000)
```

---

## 📝 참고사항

- 초음파 센서 및 라인트레이서는 `pin0`, `pin1`, `pin2` 중 남는 핀에 자동으로 할당됩니다.
- 일부 기능은 연결된 센서에 따라 동작하지 않을 수 있습니다.

---

## 📜 라이선스

본 프로젝트는 원본 코드의 라이선스를 따릅니다.  
원본 코드 출처: [Elecfreaks GitHub](https://github.com/elecfreaks/EF_Produce_MicroPython)

---

## 🙌 기여

이 라이브러리는 교육 목적의 마이크로비트 프로젝트에서 사용하기 위해 수정되었습니다.  
기여나 개선 사항이 있다면 언제든지 PR 또는 이슈를 남겨주세요!
