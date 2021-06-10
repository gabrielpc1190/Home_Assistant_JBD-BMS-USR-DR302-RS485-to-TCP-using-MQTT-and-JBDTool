# Home_Assistant_JBD-BMS-USR-DR302-RS485-to-TCP-using-MQTT-and-JBDTool
This is basic information on how to use the JBD BMS LIFEPO (Overkill Solar) RS485 interface connected to the RS485 to TCP adapter USR-DR302 in Home Assistant, using jbdtool or jbd for Windows to publish MQTT messages to MQTT broker on Home Assistant
This is basic information on how to use the JBD BMS (Overkill Solar) on RS485 connected to the RS485 to TCP adapter USR-DR302 in Home Assistant, using jbdtool or jbd for Windows to push to MQTT broker on Home Assistant: (sorry, I needed to include all key words for better search results ;-))


You need to have an MQTT broker working, I used this guide on Youtube [MEDIA=youtube]dqTn-Gk4Qeo[/MEDIA]

After MQTT is working, Create the sensors on your configuration.yaml file:



[CODE]sensor:

# Example configuration.yaml entry: https://www.home-assistant.io/integrations/sensor.mqtt/

#jbd.exe Solar Director on Windows, uncomment this section if you're using this binary

#https://diysolarforum.com/threads/jbd-bms-wi-fi-module.17252/post-282045

#https://diysolarforum.com/threads/jbd-bms-wi-fi-module.17252/post-282071



#- platform: mqtt

#  name: "LIFEPO4 Battery Voltage"

#  unit_of_measurement: "V"

#  state_topic: "SolarD/Battery/jbd/Data"

#  value_template: "{{ value_json.voltage }}"

#  json_attributes_topic: "SolarD/Battery/jbd/Data"

#  json_attributes_template: "{{ value_json.voltage | tojson }}"

#- platform: mqtt

#  name: "LIFEPO4 Battery Current"

#  unit_of_measurement: "A"

#  state_topic: "SolarD/Battery/jbd/Data"

#  value_template: "{{ value_json.current }}"

#  json_attributes_topic: "SolarD/Battery/jbd/Data"

#  json_attributes_template: "{{ value_json.current | tojson }}"

#- platform: mqtt

#  name: "LIFEPO4 Battery Temps"

#  unit_of_measurement: "C"

#  state_topic: "SolarD/Battery/jbd/Data"

#  value_template: "{{ value_json.temps }}"

#  json_attributes_topic: "SolarD/Battery/jbd/Data"

#  json_attributes_template: "{{ value_json.temps | tojson }}"



# Example configuration.yaml entry: https://www.home-assistant.io/integrations/sensor.mqtt/

#jbdtool.exe on Windows, comment this section if you're not using this binary

#https://diysolarforum.com/threads/jbd-bms-wi-fi-module.17252/post-282019



- platform: mqtt

  name: "LIFEPO4 Battery Voltage"

  unit_of_measurement: "V"

  state_topic: "LIFEPO4"

  value_template: "{{ value_json.Voltage }}"

  json_attributes_topic: "LIFEPO4"

  json_attributes_template: "{{ value_json.Voltage | tojson }}"



- platform: mqtt

  name: "LIFEPO4 Battery Current"

  unit_of_measurement: "A"

  state_topic: "LIFEPO4"

  value_template: "{{ value_json.Current }}"

  json_attributes_topic: "LIFEPO4"

  json_attributes_template: "{{ value_json.Current | tojson }}"



- platform: mqtt

  name: "LIFEPO4 Battery Design Capacity"

  unit_of_measurement: "Ah"

  state_topic: "LIFEPO4"

  value_template: "{{ value_json.DesignCapacity }}"

  json_attributes_topic: "LIFEPO4"

  json_attributes_template: "{{ value_json.DesignCapacity | tojson }}"



- platform: mqtt

  name: "LIFEPO4 Battery Remaining Capacity"

  unit_of_measurement: "Ah"

  state_topic: "LIFEPO4"

  value_template: "{{ value_json.RemainingCapacity }}"

  json_attributes_topic: "LIFEPO4"

  json_attributes_template: "{{ value_json.RemainingCapacity | tojson }}"



- platform: mqtt

  name: "LIFEPO4 Battery Percent Capacity"

  unit_of_measurement: "%"

  state_topic: "LIFEPO4"

  value_template: "{{ value_json.PercentCapacity }}"

  json_attributes_topic: "LIFEPO4"

  json_attributes_template: "{{ value_json.PercentCapacity | tojson }}"



- platform: mqtt

  name: "LIFEPO4 Battery CycleCount"

  state_topic: "LIFEPO4"

  value_template: "{{ value_json.CycleCount }}"

  json_attributes_topic: "LIFEPO4"

  json_attributes_template: "{{ value_json.CycleCount | tojson }}"



- platform: mqtt

  name: "LIFEPO4 Battery Temperatutes"

  unit_of_measurement: "ºC"

  state_topic: "LIFEPO4"

  value_template: "{{ value_json.Temps }}"

  json_attributes_topic: "LIFEPO4"

  json_attributes_template: "{{ value_json.Temps | tojson }}"

[/CODE]



Then run one of the two binaries, in my specific case I'm using jbdtool.exe with this command:

[CODE]jbdtool.exe -d 9 -t ip:172.16.10.99 -m 172.16.9.12:GABO-WORKSTATION:LIFEPO4 -i 5[/CODE]

Replace 172.16.10.99 with your USR-DR302 IP address, remember to have the USR-DR302 on TCP-Server Port 23.

Replace the 172.16.9.12 with your MQTT Broker IP address.

Replace GABO-WORKSTATION with your CLIENTID.

Adjust -i 5 to your needs, in seconds.



I setup a Scheduled Task on Windows for the moment, to run this command at computer startup, then will move on to a docker container when I find how to do it.



Any suggestion is welcome!
