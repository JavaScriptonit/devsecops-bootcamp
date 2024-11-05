## Lesson video:
https://coursehunter.net/course/devsecops-bootcamp?lesson=22

## SAST (Static Application Security Testing)

### NJSSACN
https://hub.docker.com/r/opensecurity/njsscan
Pipeline example:
```
njsscan:
  image: python
  stage: test
  before_script:
    - pip3 install --upgrade njsscan
  script:
    - njsscan --exit-warning .
```

### SEMGREP
https://hub.docker.com/r/semgrep/semgrep - IMAGE
https://semgrep.dev/docs/kb/semgrep-ci/collect-gitlab-logs - DOCS
Pipeline example:
```
semgrep :
  image: semgrep/semgrep
  stage: test
  variables:
    SEMGREP_RULES: p/javascript
  script:
    - semgrep ci --debug &> semgrep.log
  allow_failure: true
```