# SmartWeather-safetyAdvisor

Smart Weather & Personal Safety Advisor: a BME280 sensor on an STM32 NUCLEO-F401RE
sends readings through a Wemos ESP8266 over MQTT to Node-RED, which compares them
with an external weather API (Microclimate Mismatch Detector) and shows safety
recommendations on a dashboard.

## Status
- [ ] Phase 1: BME280 on STM32
- [ ] Phase 2: UART, Wemos and MQTT
- [ ] Phase 3: Node-RED, weather API and mismatch detector
- [ ] Phase 4: Recommendations and dashboard
- [ ] Phase 5: Final testing and documentation