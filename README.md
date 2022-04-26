# STM32F401-control-of-a-three-phase-electric-motor
Modeling the control of a three-phase electric motor using automatic approach with a microcontroller.
ФЕДЕРАЛЬНО ГОСУДАРСТВЕННОЕ АВТОНОМНОЕ ОБРАЗОВАТЕЛЬНОЕ 
УЧРЕЖДЕНИЕ ВЫСШЕГО ОБРАЗОВАНИЯ
«САНКТ-ПЕТЕРБУРГСКИЙ НАЦИОНАЛЬНЫЙ ИССЛЕДОВАТЕЛЬСКИЙ 
УНИВЕСИТЕТ ИТМО»
Факультет безопасности информационных технологий
Лабораторная Работа №3
по дисциплине «Дезайн вещей будущего»
Выполнил:
 Студент группы R3235
Динь Нгок Туан
 
Проверил преподаватель:
Власов С. М.
 
Санкт Петербург
2022
Цель работы: 
Моделирование управления трехфазного электродвигателя с использованием 
автоматного подхода при помощи микроконтроллера. 
Программное обеспечение: 
Proteus, STM32CubeIDE.
1. Схема на Proteus
• Схема до моделирования
• Моделирование (Запуск вперед )
• Моделирование ( Реверс двигателя )
• Моделирование ( Останов двигателя после вращения в прямом направлении)
2. Код программы управления двигателем
Код на STM32F401RE:
/* Private typedef -----------------
------------------------------------
------*/
// define for input
#define STOP_Pin GPIO_PIN_2
#define FORWARD_Pin GPIO_PIN_3
#define REVERCE_Pin GPIO_PIN_4
#define Button_GPIO_Port GPIOB
// define for output
#define MOTOR_port GPIOA
#define KM1_FORW_Pin GPIO_PIN_0
#define KM2_REV_Pin GPIO_PIN_5
/* USER CODE BEGIN PTD */
int main(void)
{
 /* USER CODE BEGIN 1 */
 /* USER CODE END 1 */
 /* MCU Configuration--------------
------------------------------------
------*/
 /* Reset of all peripherals, 
Initializes the Flash interface and 
the Systick. */
 HAL_Init();
 /* USER CODE BEGIN Init */
 /* USER CODE END Init */
 /* Configure the system clock */
 SystemClock_Config();
 /* USER CODE BEGIN SysInit */
 /* USER CODE END SysInit */
 /* Initialize all configured peripherals */
 MX_GPIO_Init();
 /* USER CODE BEGIN 2 */
 HAL_GPIO_WritePin(MOTOR_port, KM1_FORW_Pin, GPIO_PIN_RESET);
 HAL_GPIO_WritePin(MOTOR_port, KM2_REV_Pin, GPIO_PIN_RESET);
 uint8_t state = 0;
 /* USER CODE END 2 */
 /* Infinite loop */
 /* USER CODE BEGIN WHILE */
 while (1)
 {
 if(!state && (HAL_GPIO_ReadPin(Button_GPIO_Port, FORWARD_Pin) != 0) &&
 (HAL_GPIO_ReadPin(Button_GPIO_Port, REVERCE_Pin) == 0))
 {
 state = 1;
 HAL_GPIO_WritePin(MOTOR_port, KM1_FORW_Pin, GPIO_PIN_SET);
 HAL_GPIO_WritePin(MOTOR_port, KM2_REV_Pin, GPIO_PIN_RESET);
 }
 else
 {
 if(state != 0 && (HAL_GPIO_ReadPin(Button_GPIO_Port,STOP_Pin) != 0))
 {
 state = 0;
 HAL_GPIO_WritePin(MOTOR_port, KM1_FORW_Pin, GPIO_PIN_RESET);
 HAL_GPIO_WritePin(MOTOR_port, KM2_REV_Pin, GPIO_PIN_RESET);
 }
 else
 {
 if(!state &&(HAL_GPIO_ReadPin(Button_GPIO_Port, REVERCE_Pin) != 0) &&
 (HAL_GPIO_ReadPin(Button_GPIO_Port, FORWARD_Pin) == 0))
 {
 state = 1;
 HAL_GPIO_WritePin(MOTOR_port, KM1_FORW_Pin, GPIO_PIN_RESET);
 HAL_GPIO_WritePin(MOTOR_port, KM2_REV_Pin, GPIO_PIN_SET);
 }
 }
 }
 /* USER CODE END WHILE */
 /* USER CODE BEGIN 3 */
 }
 /* USER CODE END 3 */
}
3. Вывод
После выполнения этой лабораторной работы я научился 
программировать управление трехфазным двигателем с реверсивным 
управлением с помощью микроконтроллера STM32F401RE. Узнайте, как 
использовать два программного обеспечения, Proteus и STM32CUBE IDE.
