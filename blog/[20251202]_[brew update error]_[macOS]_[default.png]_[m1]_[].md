## Run terminal app.

### Unexpected method 'appcast' called on Cask adoptopenjdk11.
### Unexpected method 'appcast' called on Cask adoptopenjdk8.

원인: adoptopenjdk8, 11 지원 종료

## Solution
```bash

# remove openjdk
brew uninstall openjdk@8
brew uninstall openjdk@11

# 위 명령이 적용되지 않으면 강제 제거
brew uninstall --force 

# 강제 제거도 불가한 경우 수동 삭제
cd /opt/homebrew/Caskroom
rm -rf adoptopenjdk8
rm -rf adoptopenjdk11

# remove IntelliJ
brew uninstall intellij-idea

# 위 명령어 실행 시 아래 오류 발생
intellij-idea: It seems the App source '/Applications/IntelliJ IDEA.app' is not there.

# 수동 삭제
cd /opt/homebrew/Caskroom
rm -rf intellij-idea

# remove cache
rm -rf "$(brew --cache)"

# update-reset
brew reset-update

# upgrade
brew upgrade

# cleanup
brew cleanup

```