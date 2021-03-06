---
layout: page
title: "Customizing devices and services"
description: "Simple customization for devices and services in the frontend."
date: 2016-04-20 06:00
sidebar: true
comments: false
sharing: true
footer: true
---

By default, all of your devices will be visible and have a default icon determined by their domain. You can customize the look and feel of your front page by altering some of these parameters. This can be done by overriding attributes of specific entities.

This format works for version 0.37+. For pre-0.37 use [Older format](https://home-assistant.io/getting-started/customizing-devices/#older-format)

`customize` consists of a list of attribute customization blocks

```yaml
# Example configuration.yaml entry
homeassistant:
  name: Home
  unit_system: metric
  # etc

  customize:
    # Only the 'entity_id' is required.  All other options are optional.
    - entity_id: sensor.living_room_motion
      hidden: true
    - entity_id: thermostat.family_roomfamily_room
      entity_picture: https://example.com/images/nest.jpg
      friendly_name: Nest
    - entity_id: switch.wemo_switch_1
      friendly_name: Toaster
      entity_picture: /local/toaster.jpg
    - entity_id: switch.wemo_switch_2
      friendly_name: Kitchen kettle
      icon: mdi:kettle
    - entity_id: switch.rfxtrx_switch
      assumed_state: false
```

### {% linkable_title Possible values %}

| Attribute | Description |
| --------- | ----------- |
| `friendly_name` | Name of the entity
| `hidden`    | Set to `true` to hide the entity.
| `entity_picture` | Url to use as picture for entity
| `icon` | Any icon from [MaterialDesignIcons.com](http://MaterialDesignIcons.com). Prefix name with `mdi:`, ie `mdi:home`.
| `assumed_state` | For switches with an assumed state two buttons are shown (turn off, turn on) instead of a switch. By setting `assumed_state` to `false` you will get the default switch icon.
| `device_class` | Sets the [class of the device](/components/binary_sensor/), changing the device state and icon that is displayed on the UI (see below).

### {% linkable_title Advanced example %}

You can also specify attributes for all devices in a domain, use wildcards, use several entity IDs as a list or comma separated list. 

```yaml
homeassistant:
  customize:
    - entity_id: sensor
      icon: mdi:kettle # Give all sensor the kettle icon
    - entity_id: light.family*
      hidden: true # Hide all lights that have an ID starting with 'family'
    - entity_id: switch.wemo_switch_1,switch.wemo_switch_2,switch.wemo_switch_3
      entity_picture: /local/toaster.jpg # Set picture on multiple devices
```

Either `entity_id` must be present in each customization block.

### {% linkable_title Older format %}

In the previous version of customize format the keys were the IDs:
```yaml
homeassistant:
  name: Home
  unit_system: metric
  # etc

  customize:
    # Only the 'entity_id' is required.  All other options are optional.
    sensor.living_room_motion:
      hidden: true
    thermostat.family_roomfamily_room:
      entity_picture: https://example.com/images/nest.jpg
      friendly_name: Nest
    switch.wemo_switch_1:
      friendly_name: Toaster
      entity_picture: /local/toaster.jpg
    switch.wemo_switch_2:
      friendly_name: Kitchen kettle
      icon: mdi:kettle
    - entity_id: switch.rfxtrx_switch:
      assumed_state: false
```
This format doesn't support comma-separated IDs, wildcards or domain matching.

The formats can't be mixed
```yaml
  # NOT A VALID CONFIGURATION
  customize:
    sensor.living_room_motion:
      hidden: true
    - entity_id: thermostat.family_roomfamily_room
      friendly_name: Nest
```

### {% linkable_title Reloading customize %}
 
Home Assistant offers a service to reload the core configuration while Home Assistant is running called `homeassistant/reload_core_config`. This allows you to change your customize section and see it being applied without having to restart Home Assistant. To call this service, go to the <img src='/images/screenshots/developer-tool-services-icon.png' alt='service developer tool icon' class="no-shadow" height="38" /> service developer tools, select the service `homeassistant/reload_core_config` and click "Call Service".

<p class='note warning'>
New customize information will be applied the next time the state of the entity gets updated.
</p>

### [Next step: Setting up presence detection &raquo;](/getting-started/presence-detection/)
