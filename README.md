# prometheus-operator-lab
* setup per [user guide](https://prometheus-operator.dev/docs/user-guides/alerting/#configuring-alertmanager-in-prometheus)
* This lab is to demo using prom-operator to:
    * multiple prometheus
    * distributed rules configs per team

# How to run 
* start up
```bash
tilt up
```
* press <kbd>space</kbd> for web console
* under `uncategorized`, you should see links to prometheus and alertmanager

# Explanation
* `example` is the default prometheus instance
* `team1` has a dedicate prometheus instance
* `team2` uses default prometheus instance
* all of them share the same HA Alertmanager