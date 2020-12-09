# macos_jenv
마치 node nvm처럼 자바버전 관리하기

## 자바8만 사용하다가 자바 11을 사용해야 하는 경우가 발생

NodeJs에서는 nvm을 통해서 버전별 설치를 하고 필요에 따라서 버전을 변경할 수 있다.

현재 자바8로만 개발하다가 자바 11을 사용해야 하는 경우가 발생해서 그 흔적을 남기고자 한다.

## 개발 OS 환경

MacOs Big Sur 버전 11.0.1

```
$ brew update
$ brew install jenv
```

이렇게 일단 설치를 하자.

```
$ echo $SHELL
```
이 명령을 날려서 Default shell에 jEnv를 추가한다.
이 명령어를 날리면

```
/bin/zsh
```

요렇게 밑에 뜬다. 확인되었으면 다음으로

```
$ echo 'export PATH="$HOME/.jenv/bin:$PATH"' >> ~/.bash_profile
$ echo 'eval "$(jenv init -)"' >> ~/.bash_profile
$ echo 'export PATH="$HOME/.jenv/bin:$PATH"' >> ~/.zshrc
$ echo 'eval "$(jenv init -)"' >> ~/.zshrc
```

요렇게 명령어를 한번 더 날려준다.
이유는 모른다. 다만 zsh가 catalina부터는 기본이라고 한다. 그래서 저렇게 명령어를 날려준다.

```
$ source ~/.bash_profile
$ source ~/.zshrc
```

위 명령어를 날려서 bash_profile, zshrc 파일을 읽어온다.

```
$ jenv versions
* system (set by /Users/basquiat/.jenv/version)
```

위 명령어를 날려보면 '* system (set by /Users/basquiat/.jenv/version)'라는 문구가 뜨는데 이것은 jenv가 자바버전을 관리하도록 해줘야 한다.

```
$ jenv add /Library/Java/JavaVirtualMachines/adoptopenjdk-8.jdk/Contents/Home/
openjdk64-1.8.0.265 added
1.8.0.265 added
1.8 added
```

jenv add를 통해 통상적으로 자바 경로를 추가해주면 밑으로 added로 버전이 추가되는 것을 확인할 수 있다. 이렇게 jenv가 자바버전을 관리하게 해주자.

```
$ jenv versions
* system (set by /Users/basquiat/.jenv/version)
  1.8
  1.8.0.265
  openjdk64-1.8.0.265
```

다시 확인하면 jenv가 어떤 자바 버전을 관리하는지 알 수 있다.


## 자바 11을 깔아보자.

```
$ brew tap AdoptOpenJDK/openjdk 
```

openJDK저장소를 추가한다고 하는데 딱히 뭔가 나오는게 없어서 왜 날리는지는 모르겠음. 일단 날리고~

```
$ brew cask install adoptopenjdk11
```

여렇게 날리면 된다. cask는 deprecated!라고 뜨는걸 보면 사용하지 않는다. 대신 

```
$ brew install adoptopenjdk11
```

이렇게 하라는데? 암튼 날리고 설치하다가 맥북 로그인 비번 물어보는거 비번 치고 기다리면 설치 완료.

이제부터 jenv가 관리하도록 추가를 해주자.

```
jenv add /Library/Java/JavaVirtualMachines/adoptopenjdk-11.jdk/Contents/Home/
openjdk64-11.0.9.1 added
11.0.9.1 added
11.0 added
11 added
```

다시 한번 확인해 보자

```
$ jenv versions
* system (set by /Users/basquiat/.jenv/version)
  1.8
  1.8.0.265
  11
  11.0
  11.0.9.1
  openjdk64-1.8.0.265
  openjdk64-11.0.9.1
```

오~

```
$ java -version
openjdk version "1.8.0_265"
OpenJDK Runtime Environment (AdoptOpenJDK)(build 1.8.0_265-b01)
OpenJDK 64-Bit Server VM (AdoptOpenJDK)(build 25.265-b01, mixed mode)
```

현재 자바 버전을 체크하면 기존에 깔린 정보가 나온다.

```
$ jenv global 11.0.9.1
```

탭을 누르면 사용할 수 있는 버전 정보가 나오는데 위에 처럼 버전을 글로벌로 설정한다.

```
$ java -version
openjdk version "11.0.9.1" 2020-11-04
OpenJDK Runtime Environment AdoptOpenJDK (build 11.0.9.1+1)
OpenJDK 64-Bit Server VM AdoptOpenJDK (build 11.0.9.1+1, mixed mode)
```

끄읏
$ 
