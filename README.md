\# STM32 Input: Polling Toggle (Nucleo-F103RB)



This is a \*\*polling-based example\*\* on the NUCLEO-F103RB board that toggles \*\*LED (PA5)\*\* using the \*\*user button (PC13)\*\*.  

Each time the button is pressed, the LED switches `ON ↔ OFF` and \*\*remains in that state\*\* (toggle latch behavior).



\## Board / Pins

\- Board: NUCLEO-F103RB (STM32F103RB)

\- LED: `PA5` (LD2)

\- Button: `PC13` (B1, \*\*active-low\*\*: not pressed = High, pressed = Low)



\## How it works

\- The main loop continuously reads the button state using `HAL\_GPIO\_ReadPin()`.

\- A \*\*falling edge (1 → 0)\*\* transition is detected to identify a button press.

\- To prevent false triggers caused by mechanical switch bouncing, a \*\*50 ms debounce\*\* is applied using `HAL\_GetTick()`.



Core logic:

```c

uint8\_t prev = 1;

uint32\_t last\_ms = 0;



while (1) {

&nbsp; uint8\_t now = HAL\_GPIO\_ReadPin(GPIOC, GPIO\_PIN\_13);



&nbsp; if (prev == 1 \&\& now == 0 \&\& (HAL\_GetTick() - last\_ms) > 50) {

&nbsp;   HAL\_GPIO\_TogglePin(GPIOA, GPIO\_PIN\_5);

&nbsp;   last\_ms = HAL\_GetTick();

&nbsp; }

&nbsp; prev = now;

&nbsp; HAL\_Delay(1);

}



Build \& Flash



Open STM32CubeIDE → File > Import > Existing Projects into Workspace.



Select projects/polling\_button\_toggle/.



Build the project and flash it to the NUCLEO board.



Press button B1 (PC13) → LED (PA5) toggles.



Demo



YouTube: https://youtu.be/SYNOw21XwiU?si=h7SaOyw55f0dR8a0





\# STM32 Input: Polling Toggle (Nucleo-F103RB)



NUCLEO-F103RB에서 \*\*버튼(PC13)\*\*으로 \*\*LED(PA5)\*\*를 토글하는 폴링(Polling) 예제입니다.  

버튼을 누를 때마다 LED가 `ON ↔ OFF`로 바뀌어 \*\*그 상태를 유지\*\*합니다. (토글 유지형)



\## Board / Pins

\- Board: NUCLEO-F103RB (STM32F103RB)

\- LED: `PA5` (LD2)

\- Button: `PC13` (B1, \*\*active-low\*\*: 안 누름=High, 누름=Low)



\## How it works

\- 메인 루프에서 `HAL\_GPIO\_ReadPin()`으로 버튼을 읽어 \*\*하강 에지(1→0)\*\*를 감지합니다.

\- 기계식 스위치 노이즈를 막기 위해 \*\*디바운스 50ms\*\*를 적용합니다. (`HAL\_GetTick()` 사용)



핵심 로직:

```c

uint8\_t prev = 1;

uint32\_t last\_ms = 0;



while (1) {

&nbsp; uint8\_t now = HAL\_GPIO\_ReadPin(GPIOC, GPIO\_PIN\_13);



&nbsp; if (prev == 1 \&\& now == 0 \&\& (HAL\_GetTick() - last\_ms) > 50) {

&nbsp;   HAL\_GPIO\_TogglePin(GPIOA, GPIO\_PIN\_5);

&nbsp;   last\_ms = HAL\_GetTick();

&nbsp; }

&nbsp; prev = now;

&nbsp; HAL\_Delay(1);

}



