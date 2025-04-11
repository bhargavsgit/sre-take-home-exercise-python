API Monitoring Tool

This Python script continuously monitors a set of HTTP endpoints defined in a YAML file. It checks whether each endpoint is considered available (based on status code and response time) and logs domain-level availability percentages every 15 seconds.

🧰 Requirements

Python 3.7+

requests and pyyaml libraries

📦 Installation

Clone this repo:

git clone https://github.com/bhargavsgit/sre-take-home-exercise-python.git
cd sre-take-home-exercise-python

Install dependencies:

pip install pyyaml requests

🚀 Usage

There is sample.yaml file in the repo which needs to be passed along the script to read the configs

Run the script:

python3 main.py sample.yaml

The script will run in an infinite loop, printing domain availability stats every 15 seconds.

✅ What This Script Does

Reads endpoint configurations from a YAML file

Makes requests every 15 seconds

Evaluates if endpoints are UP (status 200–299 and response time ≤ 500ms)

Tracks cumulative availability per domain (ignoring ports)

Logs results clearly to the terminal

🛠️ Issues Identified and Fixes Applied

1. Response Time Not Checked

❌ The original code didn’t measure latency.

✅ Fix: Wrapped HTTP request in a timer and ensured response time is ≤ 500ms.

2. Port Numbers Not Ignored in Domain Grouping

❌ Original logic grouped stats by full URL.

✅ Fix: Used urllib.parse.urlparse().hostname to extract domain name only.

3. Missing Defaults for Optional Fields

❌ Missing method, headers, or body caused errors.

✅ Fix: Added .get() with defaults (GET, {}, None).

4. Improper Request Timeout

❌ Requests were not timing out, leading to hanging cycles.

✅ Fix: Set timeout=0.5 to enforce latency cutoff.

5. No Cumulative Tracking Per Domain

❌ No memory of previous checks.

✅ Fix: Used defaultdict to persist cumulative stats.