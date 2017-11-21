# Docker Katalon Studio Selenium Firefox

Container of this image can execute [Katalon Studio](https://www.katalon.com/) tests in [console mode](https://docs.katalon.com/display/KD/Console+Mode+Execution) with `Firefox` as browser type. 
The image is based on the [Selenium image for Firefox](https://github.com/SeleniumHQ/docker-selenium/tree/master/NodeFirefox) and uses `Katalon_Studio_Linux_64-5.1`. 

## Usage examples

- PROJECT_FILE: katalon project file (.prj)
- TESTSUITE_PATH: path to your test suite ( relative to TEST_DIR and without `.ts` extension)
- TEST_DIR: base directory of your katalon tests

### execute tests from inside the container

1. execute the container :

```bash
docker run --rm -it -v ${TEST_DIR}:/testdir usuresearch/katalon-selenium-firefox bash
```

2. execute tests

```bash
katalon -runMode=console -projectPath="/testdir/$PROJECT_FILE" -retry=0 -testSuitePath="$TESTSUITE_PATH" -browserType="Firefox" --remoteWebDriverType=Selenium
```

### execute tests from outside the container

```bash
docker run --rm -it -e PRJ=$PROJECT_FILE -e "TSP=$TESTSUITE_PATH"  -v $TEST_DIR:/testdir usuresearch/katalon-selenium-firefox bash -c '/start_xvfb.sh && katalon -runMode=console -projectPath="/testdir/$PRJ" -retry=0 -testSuitePath="$TSP" -browserType="Firefox" --remoteWebDriverType=Selenium'
```
