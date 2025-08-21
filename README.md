# STM32 Input Toggle (Polling & Interrupt)

## Description (English)
This project demonstrates how to control an LED on the STM32 NUCLEO-F103RB board using both polling and external interrupt (EXTI) methods.  
- **Polling version**: Continuously checks the button state in a loop.  
- **Interrupt version**: Uses an external interrupt to detect button presses and toggle the LED without polling.  

## 설명 (한국어)
이 프로젝트는 STM32 NUCLEO-F103RB 보드에서 LED를 버튼으로 제어하는 두 가지 방식을 보여줍니다.  
- **폴링 방식**: 메인 루프에서 버튼 상태를 계속 확인하여 LED를 제어  
- **인터럽트 방식**: 외부 인터럽트를 사용하여 버튼 입력을 감지하고 LED를 토글 (루프에서 감시할 필요 없음)  

---

## Demo Video
[YouTube Link](https://youtu.be/P40fSqM7nto?si=ePqSLccSWjf0dMIa)

---

## Example Code (Interrupt Version)

```c
/* EXTI Interrupt Handler */
void EXTI15_10_IRQHandler(void)
{
  HAL_GPIO_EXTI_IRQHandler(GPIO_PIN_13);
}

void HAL_GPIO_EXTI_Callback(uint16_t GPIO_Pin)
{
  if (GPIO_Pin == GPIO_PIN_13)
  {
    HAL_GPIO_TogglePin(GPIOA, GPIO_PIN_5); // Toggle LD2
  }
}


