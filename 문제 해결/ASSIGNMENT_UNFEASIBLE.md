
Alveo 펌웨어 문제일 경우
----

구성 요소와 로직을 재설치
(Docker 밖에서 실행)
```bash
~/Vitis-AI/setup/alveo/u200_u250/packages/install.sh
```

xButler 통신 문제일 경우
---

1. Try reload `xButler`
```bash
sudo service xbutler restart
```
2. xbutil reset
```bash
xbutil reset
```
3. Reinstall xButler
```bash
sudo apt install ./xbutler_4.0-0.deb  --reinstall
```
