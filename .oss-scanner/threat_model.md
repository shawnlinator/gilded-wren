# Threat model

## What this project does and where untrusted input enters
A Node.js server for continuous glucose monitoring data (Nightscout). Untrusted input: the REST
API (CGM values, devices, treatments, bolus/wizard data), the uplugin/device push endpoints, and
JSON bodies. It computes insulin recommendations from untrusted glucose/treatment input.

## Components that matter most / least
- most: the API/JSON deserialization and the bolus/wizard/COB calculation logic (medical
  decisions from untrusted numbers).
- less: the static UI, docs.

## How to exercise it
Push crafted CGM/treatment/device records; exercise every REST endpoint with malformed JSON and
extreme values.

## How you rate severity
- RCE or auth bypass: critical. Logic bugs producing dangerous insulin recommendations:
  high (treat as safety-critical).
- Data corruption: medium.

## Anything to leave alone
- Do not report the static frontend assets; focus on the server.
