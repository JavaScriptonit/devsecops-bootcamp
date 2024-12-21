https://coursehunter.net/course/devsecops-bootcamp?lesson=58 - lesson ZAP
https://hub.docker.com/r/securecodebox/zap - image


# DAST
**DAST (Dynamic Application Security Testing)** - динамическое тестирование безопасности приложения:
```
zap:
  stage: deploy-test
  image: securecodebox/zap
  needs: ["deploy_test"]
  before_script:
    - mkdir -p /zap/wrk
  script:
    - zap-baseline.py -t $ZAP_TARGET -g gen.conf -I -x baseline.xml
    - cp /zap/wrk/baseline.xml baseline.xml
  artifacts:
    when: always
    paths: 
      - baseline.xml
  tags:
    - $RUNNER_TAG
```

