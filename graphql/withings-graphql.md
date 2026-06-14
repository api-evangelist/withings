# Withings GraphQL Schema

## Overview

This conceptual GraphQL schema models the Withings health platform API, which provides access to data from Withings connected health devices including smart scales, blood pressure monitors, sleep trackers, thermometers, and fitness watches. The Withings REST API (available at https://wbsapi.withings.net) uses OAuth2 for authentication and delivers a wide range of health biomarkers for consumer wellness, remote patient monitoring, and clinical research applications.

The schema is derived from the Withings Data API reference at https://developer.withings.com/api-reference/ and reflects the structure of the official REST endpoints covering measures, activity, sleep, heart, and notification domains.

## Schema Source

- API Reference: https://developer.withings.com/api-reference/
- Developer Guide: https://developer.withings.com/developer-guide/v3/data-api/all-available-health-data/
- Authentication: https://developer.withings.com/developer-guide/v3/integration-guide/public-health-data-api/get-access/oauth-web-flow/

## Domain Coverage

### Identity and Authentication
- `User`, `UserDetails`, `UserProfile` — core user identity from the Withings account system
- `Token`, `OAuth2Token`, `APIKey` — OAuth2 token lifecycle management
- `Subscription` — notification subscription management

### Devices
- `Device`, `DeviceDetails`, `DeviceType`, `DeviceModel`, `Battery` — hardware inventory and status for paired Withings devices (scales, watches, blood pressure monitors, sleep trackers, thermometers)

### Body Composition Measures
- `Measure`, `MeasureGroup`, `MeasureDetails`, `MeasureType` — raw measure groups from the `/measure` endpoint
- `Weight`, `BMI`, `BodyFatPercent`, `Lean`, `BoneM`, `Muscle`, `Hydration`, `VisceralFat`, `Height` — individual body composition biomarkers

### Cardiovascular
- `BloodPressure`, `Systolic`, `Diastolic`, `Pulse` — blood pressure monitor readings
- `HeartRate`, `ECG`, `ECGSignal`, `AFib` — electrocardiogram and heart rhythm data from the ScanWatch

### Metabolic and Clinical
- `Glucose`, `GlucoseDetails` — blood glucose measurements for diabetes management
- `Temperature`, `SkinTemperature` — body and skin temperature readings from the Thermo and ScanWatch
- `SPO2`, `SPO2Details` — pulse oximetry / blood oxygen saturation

### Sleep
- `Sleep`, `SleepSummary`, `SleepDetails`, `SleepScore` — sleep session and quality data
- `SleepDuration`, `HRVariability`, `BreathingDisturbances`, `SnoringTime`, `WakeUp` — granular sleep biomarkers from the Sleep Analyzer and ScanWatch

### Activity
- `Activity`, `ActivitySummary`, `Steps`, `Calories`, `Distance`, `Elevation`, `Intensity` — daily activity tracking
- `Workout`, `WorkoutDetails`, `WorkoutType` — structured workout sessions

### Notifications and Goals
- `Notification`, `NotificationDetails` — webhook subscription callbacks for real-time data push
- `Goal`, `GoalDetails` — user health and activity goals

## Type Count

65 named GraphQL types are defined in `withings-schema.graphql`.

## Usage Notes

This is a conceptual schema mapping the Withings REST API to GraphQL idioms. The Withings platform does not expose a native GraphQL endpoint; this schema represents how the API data model would be expressed in GraphQL SDL. Scalar types `DateTime` (ISO 8601 timestamp) and `JSON` (arbitrary JSON object) are used where appropriate. All measure values align with the measure type codes documented in the Withings API reference (e.g., type 1 = Weight in kg, type 5 = Fat Free Mass in kg, type 6 = Fat Ratio in %, type 8 = Fat Mass Weight in kg).
