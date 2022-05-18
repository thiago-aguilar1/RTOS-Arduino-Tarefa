# RTOS-Arduino-Tarefa
Trabalho do Prof Fábio sobre RTOS Arduino



```c

#include <Arduino_FreeRTOS.h>
#include <semphr.h>

SemaphoreHandle_t mutex;

void TaskBotaoAzul( void *pvParameters );
void TaskBotaoAmarelo( void *pvParameters );
void TaskParLeds(void *pvParameters );

void setup() {

  Serial.begin(9600);

  mutex = xSemaphoreCreateMutex();
  if (mutex != NULL) {
    Serial.println("Mutex created");
  }

  xTaskCreate(
  TaskBotaoAzul
  ,  "BotaoAzul"  
  ,  128  
  ,  NULL
  ,  1
  ,  NULL );


  xTaskCreate(
  TaskBotaoAmarelo
  ,  "BotaoAmarelo" 
  ,  128 
  ,  NULL
  ,  1
  ,  NULL );

  
  xTaskCreate(
  TaskParLeds
  ,  "ParLeds" 
  ,  128 
  ,  NULL
  ,  1
  ,  NULL );
  
}


void loop() {}



void TaskBotaoAzul( void *pvParameters ) 
{
  (void) pvParameters;
  uint8_t pushButton = 10;
  pinMode(pushButton, INPUT_PULLUP);
  
  for (;;)
  {
    
    int buttonState = digitalRead(pushButton);
    if (buttonState == LOW){
    if ( xSemaphoreTake( mutex, ( TickType_t ) 5 ) == pdTRUE )
    {
    
      Serial.println(" Iniciando o processo do Botão Azul");
      vTaskDelay(pdMS_TO_TICKS(2000));
      Serial.println(" O processo do Botão Azul ainda está em execução...");
      vTaskDelay(pdMS_TO_TICKS(2000));
      Serial.println(" Botão Azul ainda em execução...");
      vTaskDelay(pdMS_TO_TICKS(2000));
      Serial.println(" Azul ainda em execução...");
      vTaskDelay(pdMS_TO_TICKS(2000));
      Serial.println(" executando ainda o Azul...");
      vTaskDelay(pdMS_TO_TICKS(2000));
      Serial.println(" Finalizando o processo do Botão Azul");
      vTaskDelay(pdMS_TO_TICKS(2000));
      
      xSemaphoreGive( mutex ); 
    }
    } 
    vTaskDelay(1); 

  }
}




void TaskBotaoAmarelo( void *pvParameters )  
{
  (void) pvParameters;
  uint8_t pushButton = 8;
  pinMode(pushButton, INPUT_PULLUP);
  
  for (;;)
  {
    
    int buttonState = digitalRead(pushButton);
    if (buttonState == LOW){
    if ( xSemaphoreTake( mutex, ( TickType_t ) 5 ) == pdTRUE )
    {
    
      Serial.println(" Iniciando o processo do Botão Amarelo");
      vTaskDelay(pdMS_TO_TICKS(2000));
      Serial.println(" O processo do Botão Amarelo ainda está em execução...");
      vTaskDelay(pdMS_TO_TICKS(2000));
      Serial.println(" Botão Amarelo ainda em execução...");
      vTaskDelay(pdMS_TO_TICKS(2000));
      Serial.println(" Amarelo ainda em execução...");
      vTaskDelay(pdMS_TO_TICKS(2000));
      Serial.println(" executando ainda o Amarelo...");
      vTaskDelay(pdMS_TO_TICKS(2000));
      Serial.println(" Finalizando o processo do Botão Amarelo");
      vTaskDelay(pdMS_TO_TICKS(2000));
      
      xSemaphoreGive( mutex ); 
    }
    }   
    vTaskDelay(1); 
  
  } 
}



void TaskParLeds(void *pvParameters )  
{    
  (void) pvParameters;
  uint8_t ledRed = 4;
  uint8_t ledGreen = 6; 
  pinMode(ledRed, OUTPUT);
  pinMode(ledGreen, OUTPUT);

  for (;;)
  {
    digitalWrite(ledRed, LOW);
    digitalWrite(ledGreen, HIGH);
    
    vTaskDelay(pdMS_TO_TICKS(1000));

    digitalWrite(ledRed, HIGH);
    digitalWrite(ledGreen, LOW);

    vTaskDelay(pdMS_TO_TICKS(1000));
  }

}

```






