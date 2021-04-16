---
title: Hello World
---
Welcome to [Hexo](https://hexo.io/)! This is your very first post. Check [documentation](https://hexo.io/docs/) for more info. If you get any problems when using Hexo, you can find the answer in [troubleshooting](https://hexo.io/docs/troubleshooting.html) or you can ask me on [GitHub](https://github.com/hexojs/hexo/issues).

## Quick Start

### Create a new post

``` bash
$ hexo new "My New Post"
```

More info: [Writing](https://hexo.io/docs/writing.html)

### Run server

``` bash
$ hexo server
```

More info: [Server](https://hexo.io/docs/server.html)

### Generate static files

``` bash
$ hexo generate
```

More info: [Generating](https://hexo.io/docs/generating.html)

### Deploy to remote sites

``` bash
$ hexo deploy
```

More info: [Deployment](https://hexo.io/docs/one-command-deployment.html)

```c
#include "esp32/ulp.h"
#include "driver/rtc_io.h"
#include "esp_deep_sleep.h"
#include "UlpDebug.h"
#include <rom/rtc.h>
#include <ETH.h>
#include "FastLED.h"

// #define ETH_ADDR        1
// #define ETH_POWER_PIN  -1
// #define ETH_MDC_PIN    23
// #define ETH_MDIO_PIN   18
// #define ETH_TYPE       ETH_PHY_LAN8720
// #define ETH_CLK_MODE   ETH_CLOCK_GPIO0_OUT


#define ETH_ADDR 1 //KSZ8863 phy addr
#define ETH_POWER_PIN 5 //KSZ8863复位引脚
#define ETH_MDC_PIN 23 //KSZ8863 MDC引脚
#define ETH_MDIO_PIN 18 //KSZ8863 MDIO引脚
#define ETH_TYPE ETH_PHY_KSZ8863

#define GPIO_EN_BTS50085        12
#define GPIO_EN_V12             32
#define GPIO_ADC_POWER          14
#define GPIO_17                 17
#define GPIO_16                 16
#define GPIO_2                 2

CRGB leds[2];
unsigned short test = 0;
// Slow memory variable assignment
enum {
  SLOW_BLINK_STATE,     // Blink status

  SLOW_PROG_ADDR        // Program start address
};


void ULP_BLINK(uint32_t us) {
  // Set ULP activation interval
  ulp_set_wakeup_period(0, us);

  // Slow memory initialization
  memset(RTC_SLOW_MEM, 0, 8192);

  // Blink status initialization
  RTC_SLOW_MEM[SLOW_BLINK_STATE] = 0;

  // PIN to blink (specify by +14)
  const int pin_blink_bit = RTCIO_GPIO2_CHANNEL + 14;
  const gpio_num_t pin_blink = GPIO_NUM_2;

  // GPIO2 initialization (set to output and initial value is 0)
  // rtc_gpio_init(pin_blink);
  // rtc_gpio_set_direction(pin_blink, RTC_GPIO_MODE_OUTPUT_ONLY);
  // rtc_gpio_set_level(pin_blink, 0);

  // ULP Program
  const ulp_insn_t  ulp_prog[] = {
    M_LABEL(3),    
    I_MOVI(R0, 64),          
    I_MOVI(R1, 0x00), 
    M_LABEL(4), 
    I_ST(R1,R0,0),

    I_ADDI(R1,R1,1),

    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),   
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),
    I_DELAY(60000),         
    M_BX(4), 

    I_MOVI(R3, SLOW_BLINK_STATE),           // R3 = SLOW_BLINK_STATE
    I_LD(R0, R3, 0),                        // R0 = RTC_SLOW_MEM[R3(SLOW_BLINK_STATE)]
    M_BL(1, 1),                             // IF R0 < 1 THAN GOTO M_LABEL(1)

    // R0 => 1 : run
    I_WR_REG(RTC_GPIO_OUT_REG, pin_blink_bit, pin_blink_bit, 1), // pin_blink_bit = 1
    I_MOVI(R0, 0),                          // R0 = 0
    I_ST(R0, R3, 0),                        // RTC_SLOW_MEM[R3(SLOW_BLINK_STATE)] = R0
    M_BX(2),                                // GOTO M_LABEL(2)

    // R0 < 1 : run
    M_LABEL(1),                             // M_LABEL(1)
    I_WR_REG(RTC_GPIO_OUT_REG, pin_blink_bit, pin_blink_bit, 0),// pin_blink_bit = 0
    I_MOVI(R0, 1),                          // R0 = 1
    I_ST(R0, R3, 0),                        // RTC_SLOW_MEM[R3(SLOW_BLINK_STATE)] = R0
    M_LABEL(2),                             // M_LABEL(2)
    // I_DELAY(60000),
    // I_DELAY(60000),
    // I_DELAY(60000),
    // I_DELAY(60000),
    // I_DELAY(60000),
    // I_DELAY(60000),
    // I_DELAY(60000),
    // I_DELAY(60000),
    // I_DELAY(60000),
    // I_DELAY(60000),
    // I_DELAY(60000),
    // I_DELAY(60000),
    // I_DELAY(60000),
    // I_DELAY(60000),
    M_BX(3) 
    //I_HALT()                                // Stop the program
  };

  // Run the program shifted backward by the number of variables
  size_t size = sizeof(ulp_prog) / sizeof(ulp_insn_t);
  ulp_process_macros_and_load(SLOW_PROG_ADDR, ulp_prog, &size);
  ulp_run(SLOW_PROG_ADDR);

  //ETH.begin(ETH_ADDR, ETH_POWER_PIN, ETH_MDC_PIN, ETH_MDIO_PIN, ETH_TYPE, ETH_CLK_MODE); //启用ETH
  ETH.begin(ETH_ADDR, ETH_POWER_PIN, ETH_MDC_PIN, ETH_MDIO_PIN, ETH_TYPE);
  while(!((uint32_t)ETH.localIP())) //等待获取到IP
  {

  }
  Serial.println("Connected");
  Serial.print("IP Address:");
  Serial.println(ETH.localIP());
 
}
#define uS_TO_S_FACTOR 1000000  /* Conversion factor for micro seconds to seconds */
#define TIME_TO_SLEEP  5        /* Time ESP32 will go to sleep (in seconds) */

void setup() {
  // For debug output
  FastLED.addLeds<WS2812, 33>(leds, 2);
  leds[0]=CRGB( 228, 255, 0 );
  FastLED.show();
  delay(1000);
  //FastLED.clear();

  leds[1]=CRGB( 1, 255, 255 );
  FastLED.show();
  delay(1000);
  FastLED.clear();

  int rst = rtc_get_reset_reason(0);
  pinMode (GPIO_2, OUTPUT);
  pinMode (GPIO_EN_BTS50085, OUTPUT);
  pinMode (GPIO_EN_V12, OUTPUT);
  pinMode (GPIO_17, OUTPUT);
  pinMode (GPIO_16, OUTPUT);
  adcAttachPin(GPIO_ADC_POWER);
  analogReadResolution(GPIO_ADC_POWER);

  Serial.begin(115200);
  Serial.printf("rst:%d\r\n",rst);

  digitalWrite(GPIO_EN_BTS50085, LOW); 
  digitalWrite(GPIO_EN_V12, LOW); 

  // Execute ULP program at 300ms intervals
  if(rst == 1)
  {
      Serial.printf("\r\ninit ulp\r\n");
      ULP_BLINK(100000);
  }
   
}

void loop() {
  // For debug output
  //ulpDump();

int  analog_value = 0;
analog_value = analogRead(GPIO_ADC_POWER);
Serial.printf("Current Reading on Pin(%d)=%0.4f\n",GPIO_ADC_POWER,analog_value*3.3/4096);

digitalWrite(GPIO_2, HIGH);
digitalWrite(GPIO_17, HIGH);
digitalWrite(GPIO_17, HIGH);
digitalWrite(GPIO_EN_V12, HIGH);
digitalWrite(GPIO_EN_BTS50085, HIGH);
delay(3000);

analog_value = 0;
analog_value = analogRead(GPIO_ADC_POWER);
Serial.printf("Current Reading on Pin(%d)=%0.4f\n",GPIO_ADC_POWER,analog_value*3.3/4096);

digitalWrite(GPIO_2, LOW);
digitalWrite(GPIO_17, LOW);
digitalWrite(GPIO_EN_V12, LOW);
digitalWrite(GPIO_EN_BTS50085, LOW);
delay(3000);

  *((uint32_t *)(RTC_SLOW_MEM+4*4)) = 0x12345678;

  //for(int i=0;i<10;i++)
  //  Serial.printf("%02X : %08X\r\n",4*i,(uint32_t)*(uint32_t *)(RTC_SLOW_MEM+4*i));
  
  Serial.printf("%d\r\n",(uint16_t)*(uint32_t *)(RTC_SLOW_MEM+64));
  // Wait
  //while(1)
//     delay(1000);

//     esp_deep_sleep_enable_timer_wakeup(TIME_TO_SLEEP * uS_TO_S_FACTOR*2);
//     esp_deep_sleep_start();
// Serial.printf("zzzz");
}

```
