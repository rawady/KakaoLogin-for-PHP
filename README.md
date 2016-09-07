KLPL  - v0.08 (2016-09-07)
=====================


**카카오 아이디로 로그인 PHP**.
----------

LIVE DEMO : http://www.rawady.co.kr/open/kakao/

네이버 아이디로 로그인 : https://github.com/rawady/NaverLogin-for-PHP




**안내**
카카오 로그인 for PHP는 네이버아이디로 로그인(https://github.com/rawady/NaverLogin-for-PHP) 라이브러리에
카카오톡 연동이 가능하도록 수정된 버전입니다. 자세한 내용은 > https://github.com/rawady/NaverLogin-for-PHP
두 라이브러리 기능 및 사용법은 동일합니다.

> 이제 곧 ...
> - SNS 로그인(네이버/카톡/페이스북) 하나로 합친 라이브러리가 이제 곧... 
> - 버전빌딩이 오락가락 인거 같은데... 이건 나중에 정리할게요

Documents
---------

> **NOTE:**
>
> - 공식 라이브러리가 아닙니다.
> - PHP로 **카카오 아이디로 로그인** 을 연동하기 쉽도록 제공합니다.
> - 공식 API 연동 명세는  **아래 URL** 을 참고하세요.
> - <i class="icon-share"></i> https://developers.kakao.com/docs/





> **Spec :**
>
> - PHP 5 이상의 버전이 필요합니다.
> - curl 활성화 필요.


> **지원 기능 (0.03 버전):**
>
> - 인증 요청 및 엑세스 토큰 취득.
> - 아이디로 로그인 버튼 생성.
> - 사용자 프로필 취득 ( JSON, XML ).
> - 로그아웃



#### <i class="icon-file"></i> 시작하기

카카오에서 발급된 CLIENT_ID 이 필요합니다. https://developers.kakao.com/apps 를 방문하여 키를 발급받고, 등록 과정을 완료한 이후 사용이 가능합니다.
> API 설정에서 '사이트 URL' 과 'callback URL'로 지정된 위치에서는 반드시 본 클래스가 생성되어 있어야 합니다.

> **주의:** 로그인 사용자 연결 유지를 위해, 세션을 사용합니다. 서버의 세션이 작동 가능하도록 해주세요.


----------


How to use
---------------

### Class 초기화


```
$kakao = new KAKAO_LOGIN(array(
		"CLIENT_ID" => "USER_CLIENT_ID",		// (*필수)클라이언트 ID  
		"RETURN_URL" => "USER_RETURN_URL",		// (*필수)콜백 URL
		"AUTO_CLOSE" => false,				// 인증 완료후 팝업 자동으로 닫힘 여부 설정 (추가 정보 기재등 추가행동 필요시 false 설정 후 추가)
		"SHOW_LOGOUT" => false				// 인증 후에 네이버 로그아웃 버튼 표시/ 또는 표시안함
		)
	);
```


### 로그인 버튼 생성

로그인 버튼은 네이버 공식 이미지로 저희 서버에서 재전송됩니다. 로그인 상태에서는 로그아웃 버튼이 표시됩니다.
```
// $kakao->login();

<div class="login_box">
 <?=$kakao->login()?>
</div>
```

```
// 로그인 버튼 크기변경시

$kakao->login(array(
	"width"=>"200"
));

```


### 사용자 정보 취득

사용자 정보는 로그인 및 인증 완료상태에서만, 작동합니다.
네이버에서 제공되는 XML 을  **JSON** 으로 인코딩하여 반환합니다.

```
(optional) $kakao->getUserProfile((string) return type(JSON, XML));

// Default : json 반환
// XML 반환시 : $kakao->getUserProfile('XML');
//

```




### 로그인 상태 확인

현재 사용자의 로그인/인증 상태를 확인 할 수 있습니다.

```
(boolean) $kakao->getConnectState();
```

> **리턴값:**
>
> - <i>(boolean)</i>**true** 로그인 및 인증 완료
> - <i>(boolean)</i>**false** 연결안됨




### Access Token 확인

현재 사용자에게 발급된 엑세스토큰을 반환합니다.

```
(string) $kakao->getAccess_token();
```
