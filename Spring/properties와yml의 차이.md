# ```application.properties```와 ```application.yml```

- 다른 환경에서도 애플리케이션이 동작할 수 있도록 **설정 관련 정보**가 들어있는 하나의 파일이다.
- 포트 설정, 어떤 데이터베이스와 연결해줄 것인지와 관련한 정보 등을 저장할 수 있다. 
  - 스프링 부트의 서버번호는 8080이 default 이지만, 다른 포트를 사용하고 싶다면 설정 파일에 선언해줄 수 있다.
```
server.port = 9090
```
---
- 두 파일 모두 **설정 파일**이라는 공통점을 가지고 있지만, **서술하는 방식은 다르다.**
- ```Elastric Search```나 ```MongoDB database```는 ```YAML(.yml)```을 default configuration format으로 사용한다.
- ```Java```에서는 주로 ```.properties```를 많이 이용한다. 

``` shell
***.yml

# 구분자: spacebar, (XX tab)

somemap:
    key:value 
    number:9

    map2: {bool=true, date=2022.07.19}

```

``` shell
***.properties

key = value
number = 9
bool = true

```

|YAML (```.yml```) |```.properties```|
|:---:|:---:|
|key/value <br/> map, List, Scalar 유형 지원|key/value를 지원하지만, 문자열 이외에는 지원하지 않는다|
|Python, Ruby, Java등에 많이 퍼져있다. | 주로 자바에서 이용|
|계층형구조|비계층형구조|
|SpringFramework는 ```@PropertySources```를 지원하지 않는다. | SpringFramework에서 ```@PropertySources```를 지원한다.|

> ```@PropertySources``` ? 
> > SpringFramework에서 환경설정 경로 등을 주입할 때 사용하는 어노테이션 <br/> 
> Spring 4.0에서 추가된 옵션 

``` java
@Configuration
@PropertySource(value = {"dbProperty.properties"})
public class DBConfig {
  @Value("${dbconfig.driver}")
  private String driver;
  @Value("${dbconfig.url}")
  private String url;
  @Value("${dbconfig.username}")
  private String username;
  @Value("${dbconfig.password}")
  private String password;
  ...
}
```


<br/>

### ```.yml```은 ```.properties```에 비해 어떤 이점이 있을까?
- 의존관계나, 파일 설정정보 등을 계층형으로 관리하기 때문에 규칙이나 유형변환에 있어서 ```.properties```보다 효과적일 수 있다.
- 지원하는 언어의 폭이 넓기 때문에 다양한 응용프로그램을 사용하는 경우 ```.yml``` 이 유리하다. 

