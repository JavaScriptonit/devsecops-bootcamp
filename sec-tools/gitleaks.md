## Lesson video:
https://coursehunter.net/course/devsecops-bootcamp?lesson=19

## Images:
https://hub.docker.com/search?q=gitleaks

## Docs:
https://hub.docker.com/r/zricethezav/gitleaks

## Install:
### MacOS:
```
brew install gitleaks
```

### Docker (any OS):
```
docker pull zricethezav/gitleaks:latest
docker run -v ${path_to_host_folder_to_scan}:/path zricethezav/gitleaks:latest [COMMAND] --source="/path" [OPTIONS]
```

#### Work example:
```
docker run -v /Users/andreyshabunov/PhpstormProjects/devsecops-bootcamp-group/juice-shop-main:/path zricethezav/gitleaks:latest detect --source="/path" --verbose 
```
#### Command output:
```
    ○
    │╲
    │ ○
    ○ ░
    ░    gitleaks

5:20PM INF 2 commits scanned.
5:20PM INF scan completed in 4.58s
5:20PM WRN leaks found: 40
```

## Customize OWN rules for scanning:
https://github.com/gitleaks/gitleaks/blob/master/config/gitleaks.toml

