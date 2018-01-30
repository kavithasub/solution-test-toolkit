# Scenario Tests - Repo Structure - Updated on Jan 27, 2018
```
<product>-test-integration
    scenario-config.yaml
    pre-run-scenarios.sh
    run-scenarios.sh
    post-run-scenarios.sh
    config.yaml
    scenario01
        run-scenario.sh
        01-pre-scenario.sh
        01-post-scenario.sh
        jmeter
            01-<test_plan_name>.jmx
            02-<test_plan_name>.jmx
    config-sets
        config01
            apply-config.sh
            revert-config.sh
        config02
            apply-config.sh
            revert-config.sh
    apps
        <custom_app_source>
```
# Configuration YAML structure (Scenariofile)

### Scenariofile v1:
Until config-value-sets come into the picture, we can maintain a configuration like following to let TestGrid know what scenarios are ready:
```
scenarios:
--apps
--scenario02
--scenario12
--scenario18
--scenario21
--scenario28
```
### Scenariofile v2:
```
config-value-sets:
--config01:
    -description: “abc”
    -applies-to:
            -scenario01
            -scenario02
--config02
    -description: “abc”
    -excludes-from:
            -scenario03
            -scenario01
```
**Note:** Applies-to and Excludes-from are mutually exclusive.

## Pre test run script (pre-scenario-run.sh)

Here, we run any task that needs to be executed as the very first step.

Define a working directory for scenario-runs.. Say: /opt/scenario-runs/

Logic:
- Download jmeter
- Build and copy jmeter related libs to jmeter
- Build web apps/ needed for IS

### run-scenarios.sh
Call run-scenario.sh in each scenario folder.

