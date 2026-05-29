# Weather Integration (Recommended Setup)

irriBRANT PRO supports smart weather-aware irrigation using Home Assistant weather providers.

This allows the controller to:

* Block irrigation during rain
* Delay irrigation after rain
* Use rain probability forecasts
* Detect active rain conditions
* Prepare for future smart irrigation features

---

# Recommended Weather Provider

## PirateWeather (Recommended)

PirateWeather is strongly recommended because it provides:

* Hourly rain probability
* Rain intensity
* Snow detection
* High-quality forecasts
* Excellent Home Assistant integration
* Free API access

Official website:

https://pirateweather.net/

---

# Installing PirateWeather

## Step 1 - Create PirateWeather Account

Go to:

https://pirateweather.net/

Create an account and obtain your API key.

---

# Step 2 - Install PirateWeather Integration

Inside Home Assistant:

```text id="0wkl03"
Settings → Devices & Services → Add Integration
```

Search for:

```text id="cn2w73"
Pirate Weather
```

Paste your API key and complete setup.

---

# Step 3 - Find Your Weather Entity

After installation:

1. Open Developer Tools
2. Open States tab
3. Search for:

```text id="2n0ktt"
weather.
```

Example entity:

```text id="n4hbux"
weather.pirateweather_thornton
```

Your entity name may be different.

---

# Template Sensor Configuration

If your `configuration.yaml` contains:

```yaml id="6rybqs"
template: !include templates.yaml
```

Then you must add the following sensors inside:

```text id="7w2pv2"
templates.yaml
```

---

# Add This to templates.yaml

Replace the weather entity with your own entity name if necessary.

Example:

```yaml id="1w2wnk"
# irriBRANT weather sensors

- trigger:
    - platform: time_pattern
      minutes: "/30"

    - platform: homeassistant
      event: start

  action:
    - service: weather.get_forecasts
      target:
        entity_id: weather.pirateweather_thornton
      data:
        type: hourly
      response_variable: hourly

  sensor:
    - name: "irriBRANT Rain Probability 12h"
      unique_id: irribrant_rain_probability_12h
      unit_of_measurement: "%"
      state: >
        {% set fc = hourly.get('weather.pirateweather_thornton', {}).get('forecast', []) %}
        {% if fc | count > 0 %}
          {{ fc[0].precipitation_probability | default(0) }}
        {% else %}
          0
        {% endif %}

- sensor:

    - name: "irriBRANT Current Rain Intensity"
      unique_id: irribrant_current_rain_intensity
      unit_of_measurement: "in/h"
      state: >
        {{ states('sensor.openweathermap_rain') | float(0) }}
```

---

# Important

Replace:

```yaml id="5y3f9m"
weather.pirateweather_thornton
```

with your actual PirateWeather entity.

---

# Restart Home Assistant

After editing `templates.yaml`:

1. Save the file
2. Go to:

```text id="jjk4gx"
Developer Tools → YAML
```

3. Click:

```text id="83rfxm"
Check Configuration
```

4. Restart Home Assistant

---

# Verify Sensors

After restart, verify these entities exist:

```text id="dnhw9d"
sensor.irribrant_rain_probability_12h
sensor.irribrant_current_rain_intensity
```

---

# Recommended Rain Settings

| Setting                    | Recommended |
| -------------------------- | ----------- |
| Rain Probability Threshold | 60%         |
| Rain Intensity Threshold   | 0.1 in/h    |
| Rain Delay Hours           | 12          |

---

# Future Improvements

PirateWeather enables future advanced irrigation features such as:

* Freeze protection
* Snow detection
* Seasonal adjustment
* Smart ET calculations
* Dynamic irrigation scheduling
* Weather-adaptive watering
* Rachio/Hydrawise style optimization
