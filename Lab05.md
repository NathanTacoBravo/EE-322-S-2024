# Lab 5 - Paho-MQTT

Because Paho-MQTT updated to v2.0.0, some of the provided scripts need to be updated as well.

**client.py (line 14):**
- Old --> `client = mqtt.Client()`
- New --> `client = mqtt.Client(mqtt.CallbackAPIVersion.VERSION1)`

**sub.py (line 7):**
- Old --> `client = mqtt.Client()`
- New --> `client = mqtt.Client(mqtt.CallbackAPIVersion.VERSION1)`

**sub-multiple.py (line 7):**
- Old --> `client = mqtt.Client()`
- New --> `client = mqtt.Client(mqtt.CallbackAPIVersion.VERSION1)`

**subcpu.py (line 7):**
- Old --> `client = mqtt.Client()`
- New --> `client = mqtt.Client(mqtt.CallbackAPIVersion.VERSION1)`

**pubcpu.py (line 5):**
- Old --> `mqttc = mqtt.Client()`
- New --> `mqttc = mqtt.Client(mqtt.CallbackAPIVersion.VERSION1)`
---

**Results of sub/pub.py:**
![Screenshot 2024-03-18 145036](https://github.com/NathanTacoBravo/EE-322-S-2024/assets/116911160/bc238cc9-c021-4943-99b4-6ff5f1a5478d)
---

**Results of sub-multiple/pub-multiple.py:**
![Screenshot 2024-03-18 150120](https://github.com/NathanTacoBravo/EE-322-S-2024/assets/116911160/6e5f2eec-df47-4881-887e-af1f98e018db)
---

**Results of subcpu/pubcpu.py:**
![Screenshot 2024-03-18 150859](https://github.com/NathanTacoBravo/EE-322-S-2024/assets/116911160/b086a374-05ff-4ae5-b4bf-6c1baf8a13de)
