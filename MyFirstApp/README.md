## 목차

- [안드로이드 프로젝트 구성 (1)](#안드로이드-프로젝트-구성-1)
  - [안드로이드 프로젝트 구조](#안드로이드-프로젝트-구조)
- [안드로이드 프로젝트 구성 (2)](#안드로이드-프로젝트-구성-2)
- [안드로이드 프로젝트 구성 (3)](#안드로이드-프로젝트-구성-3)
- [안드로이드 앱의 실행 과정](#안드로이드-앱의-실행-과정)
  - [컴파일 과정](#컴파일-과정)
  - [안드로이드 앱 배포과정](#안드로이드-앱-배포과정)
- [XML 레이아웃의 장점](#xml-레이아웃의-장점)
- [View](#view)
  - [1) 액티비티와 View](#1-액티비티와-view)
  - [2) View의 종류](#2-view의-종류)
    - [ViewGroup](#viewgroup)
    - [위젯](#위젯)
  - [3) View의 속성](#3-view의-속성)
    - [a) id 속성](#a-id-속성)
    - [b) clickable, longClickable 속성](#b-clickable-longclickable-속성)
    - [c) background 속성](#c-background-속성)
    - [d) padding 속성](#d-padding-속성)
    - [e) visibility 속성](#e-visibility-속성)
    - [f) focusable 속성](#f-focusable-속성)
- [용어 정리](#용어-정리)

# 안드로이드 프로젝트 구성 (1)

|파일명|개요|
|:---|:---|
|`java/MainActivity.java`|**JAVA 프로그램 파일**이 저장되는 폴더이며, 실제 **어플리케이션 실행**을 위한 코드|
|`build/R.java`|**프로그램 실행**을 위한 **ID 참조**를 위한 모든 속성이 저장된 파일|
|`res/drawable/*`|화면에 표시될 이미지가 저장되는 폴더|
|`res/layout/activity_main.xml`|레이아웃을 정의한 XML 파일|
|`res/value/strings.xml`|문자열의 속성을 정의한 XML 파일|
|`manifests/AndroidManifest.xml`|프로젝트의 버전이나 이름, 구성, 어플리케이션의 주요 속성을 정의한 XML 파일|

## 안드로이드 프로젝트 구조

![](../images/project-structure.jpg)

# 안드로이드 프로젝트 구성 (2)

1. **`activity_main.xml`**

- 화면의 레이아웃은 JAVA 프로그램에서 직접 기술하지 않고 XML에서 기술된 레이아웃 리소스를 사용함
- RelativeLayout이라는 레이아웃 안에 TextView라는 문자열을 표시하는 View를 배치하고 있음
- TextView의 android:text 속성에는 @strings/hello_world 값이 지정되어 있음
- @strings/hello_world 값은 strings.xml에서 정의된 hell_world라는 이름의 문자열 ID로 대체된다는 것을 의미함

2. **`strings.xml`**

- 화면에 표시되는 문자열은 XML 문서안에서 정의되기도 하지만 strings.xml 파일에서 정의될 수 있음
- 레이아웃 리소스로 정의된 TextView에서 참조되고 있는 문자열(hello_world)
- 홈 스크린의 아이콘 아래에 표시하기 위한 문자열(app_name)을 정의함
- menu_main.xml 에서 사용되는 문자열(action_settings)을 정의함
- 사용되는 문자열을 JAVA 프로그램으로부터 분리하여, 영어나 다른 언어로 쉽게 변환될 수 있음

3. **`R.java`**

- 리소스 ID를 참조하기 위한 클래스
- R 클래스나 내부의 정수 정의는 개발툴(aapt:Android Asset Packagint Tool)에 의해 자동적으로 작성됨(리소스 파일들을 컴파일 한 후에 자동으로 리소스 ID를 등록함)
- JAVA 프로그램이나 XML 파일에서 참조하는 리소스의 ID는 R.java 파일에서 정의됨
- 개발자는 이 파일을 변경해서는 안됨
- R.java 클래스의 필드인 R.layout.activity_main은 JAVA 파일(MainActivity.java)의 setContentView가 인수로서 사용됨

# 안드로이드 프로젝트 구성 (3)

1. **`MainActivity.java`**

- 안드로이드 앱의 화면을 구성하거나 사용자와 상호작용하는 Activity(액티비티) 클래스를 상속받아 새로운 액티비티를 생성함
- 사용자의 요구에 반응하여 새로운 액티비티(화면)를 생성하거나 사용자의 요구사항을 만족시키는 작업을 수행함

2. **`AndroidManifest.xml`**

- 응용 프로그램 구성 정보를 담고 있음
- 매니페스트 파일의 이름은 프로젝트에 상관없이 AndroidManifest.xml로 고정되어 있음
- 안드로이드 앱 컴포넌트의 선언
- 안드로이드 앱의 실행을 위한 소유 권한 정의
- 안드로이드 앱이 필요로 하는 최소한의 API 레벨 정의
- 안드로이드 앱이 필요로 하는 H/W, S/W 기능 정의
- 안드로이드 앱이 필요로 하는 API 라이브러리 정의

# 안드로이드 앱의 실행 과정

## 컴파일 과정

![](../images/compile-flow.jpg)

- 안드로이드 앱은 JAVA 언어를 이용하여 작성함
- 개발자가 작성한 JAVA 코드는 JAVA 컴파일러에 의해 JAVA 바이트 코드로 컴파일 됨
- 원래 JAVA 환경에서는 컴파일 된 JAVA 바이트 코드를 JAVA 가상 머신을 통해 실행하지만 안드로이드는 Dalvik이라고 하는 별도의 가상 머신에서 실행함
- 안드로이드 SDK가 제공하는 DEX 변환기를 이용하여 JAVA 바이트 코드를 Dalvik의 실행 포맷인 .dex 파일로 변환해줌
- 변환된 .dex 파일은 안드로이드 스마트폰에 설치가 가능하며 설치 후 실행하면 Dalvik 가상 머신이 인터프리터 혹은 JIT 컴파일러를 이용하여 DEX 바이너리를 CPU가 인식할 수 있는 기계어 코드로 변환함
- DEX 변환기를 이용하여 JAVA 바이트 코드를 .dex 실행 파일로 변환하는 과정은 개발자가 코드를 개발하는 컴퓨터에서 수행됨

## 안드로이드 앱 배포과정

![](https://developer.android.com/images/tools/studio/build-process_2x.png)

- 안드로이드 프로젝트에 대한 코드 컴파일 작업이 수행되면, JAVA 프로그램의 .class 파일이 생성되고, .class 파일을 이용하여 안드로이드 실행환경(Android runtime)에 적합한 .dex 파일이 생성됨
- 컴파일된 리소스 파일(XML)이 resources.arsc라는 파일로 생성됨
- 안드로이드 앱의 설정 환경을 저장하는 컴파일된 AndroidManifest.xml 파일이 생성됨
- 컴파일 되지 않은 리소스 파일(image 파일, 아이콘 파일 등)이 .dex 파일, resource.arsc 파일, AndroidManifest.xml 파일과 함께 패키징되어 .apk 파일이 생성됨
- debug key를 이용하여 .apk 파일에 서명을 하는 signing 작업을 하여 .apk파일이 타인에 의해서 위변조 되는 것을 방지함
- Goolge Play에 개발된 안드로이드 앱의 배포가 준비되면, 자신의 key 값을 이용하여 sigining 서명을 할 수 있음
- Singing 작업에서 사용한 키값은 안드로이드 앱의 업데이트에서 개발자의 식별에 사용됨

# XML 레이아웃의 장점

- 구조와 속성을 함축적으로 기술할 수 있으며 레이아웃 재활용도 가능함
- XML 파일은 어플리케이션 실행전에 미리 컴파일되므로 성능상의 영향은 없음
- XML 파일 컴파일 결과는 이진 포맷으로 바뀌어 실행 파일에 포함되므로 용량상의 낭비도 없음

# View

## 1) 액티비티와 View

- 액티비티는 안드로이드 앱의 화면을 구성하는 단위임
- 액티비티 자체는 화면에 직접적으로 보이지 않으며 액티비티 안의 View가 사용자에게 보여지는 실체를 구현함
- 여러 개의 View가 모여서 액티비티 하나를 구성하고 액티비티 여러 개가 모여서 하나의 안드로이드 앱을 구성함
- View의 파생 클래스 개수는 방대할 뿐만 아니라 각 클래스가 지원하는 속성이나 기능이 많음

## 2) View의 종류

### ViewGroup

- 직접적으로 보이지 않으며 다른 View를 담는 그릇 역할을 함
- 여러 개의 View를 유기적으로 모아 놓은 것
- ViewGroup 클래스들은 일반적으로 레이아웃이라고 함

### 위젯

- 직접적으로 보이며 사용자 인터페이스를 구성함
- Buttton, TextView, EditView, RadioButton 등이 대표적인 위젯이며 스스로 그릴 수 있는 능력을 가지고 있음

1. **위젯**

![](../images/widget_layout.jpg)

- 사용자들과 직접적인 상호작용을 이끌어내며, 상호작용의 결과를 표현하기 위해서도 사용됨
- 사용자로부터 입력된 값을 JAVA 프로그램에 전달하기도 함

1. **ViewGroup**

![](../images/view_group_layout.jpg)

- 다른 View를 포함하며, 이렇게 포함된 View를 배치하는 기능을 가짐
- 편의상 위젯과 ViewGroup으로 나누지만 어떤 클래스는 ViewGroup이면서도 위젯처럼 사용되기도 함
- 항목의 집합을 표시하는 ListView는 다른 View를 포함하는 ViewGroup이면서 사용자에 직접적으로 보여짐
- 단순 위젯에 비해 여러 개의 View가 모여서 구현되며 많은 기능으로 인해 복잡함

## 3) View의 속성

### a) id 속성

- View의 이름을 정의함
- JAVA 프로그램이나 XML 문서에서 View를 참조할 때 ID를 사용하므로 의미를 잘 성명할 수 있는 직관적인 이름을 붙이는 경우가 많음
- 직관적인 ID의 사용은 JAVA  프로그램의 이해도나 가독성을 높여줄 수 있음
- `@[+]id/ID`
  - `@` : id를 R.java에 정의하거나 R.java로부터 참조한다는 뜻
  - `+` : ID를 새로 정의한다는 뜻인데 처음 정의할 때만 붙이고 참조할 때는 붙이지 않음
  - `id/` : 예약어
  - `ID` : 고유한 명칭(프로그래머가 결정)이므로 명칭 규칙에 맞아야 하며 View끼리 중복되어서는 안됨
  - ex) Button에 name이라는 id를 부여
    - `android:id="@+id/name"`
  - ex) Button에서 textView라는 id의 View를 접근함
    - `android:layout_below="@id/textView"`  

### b) clickable, longClickable 속성

- clickable : 마우스 클릭 이벤트 허용 여부를 결정함
- longClickable : 롱클릭 이벤트 허용 여부를 결정함
- click : 손가락으로 View를 누르는 것
- Long click : View를 누른 채로 잠시 기다린는 것
- 논리형이므로 true 또는 false 둘 중 하나의 값을 지정함

### c) background 속성

- View의 배경을 채우는 방법을 지정함
- 별다른 지정이 없다면 View의 기본 배경이 그려짐
- 여러 가지 객체로 배경을 지정할 수 있는데 가장 흔한 형태는 색상임
- 배경뿐만이 아니라 색상을 지정하는 방법도 background 속성을 이용하며 아래의 네가지 방법이 적용됨
  - #RGB
  - #ARGB
  - #RRGGBB
  - #AARRGGBB
- '#' 다음에 16진수로 각 색상 요소의 강도를 지정
- 웹에서 흔히 사용되는 표준화된 방식임

### d) padding 속성

- View와 내용물간의 간격을 지정함
- View의 안쪽 여백이며, TextView의 경우 TextView 자체와 중앙의 텍스트 사이에 padding 속성값 만큼 여백이 삽입됨
- padding 속성에 값을 지정하면 네 방향(상하좌우)에 대해 동일한 여백이 적용됨
- paddingLeft, paddingTop, paddingRight, paddingBottom 속성에 개별적으로 값을 지정해 각 변에 서로 다른 여백을 줄 수 있음

### e) visibility 속성

- 화면에 View의 표시 유무를 지정함
- 별다른 지정이 없으면 보이는 상태로 배치되지만 이 속성을 사용하면, 실행시에 필요할 때만 보이거나 숨길 수도 있음
- visibility 속성은 런타임에서도 얼마든지 변경 가능함
  |속성값|설명|
  |:---:|:---:|
  |visible|View가 보이는 상태|
  |invisible|View가 숨겨진 상태이지만 자리는 차지|
  |gone|View가 숨겨진 상태이며 자리도 차지하지 않음|
- invisible은 화면에 보이지는 않지만 자리는 여전히 차지하기 떄문에 gone과 다름
- invisible은 일시적인 투명 상태이며 gone은 완전히 사라진 상태임

### f) focusable 속성

- 키보드 포커스 허용 여부를 지정함
- View 클래스 자체는 디폴트로 포커스를 받지 않도록 되어 있으므로 키 입력을 받으려면 이 속성을 true로 변경해야함
- EditText나 Button처럼 사용자의 입력을 받아야 하는 파생 클래스는 focusable 속성의 디폴트가 true로 지정되어 있음

# 용어 정리

- **XML**
  - XML은 마크업 언어의 일종으로, 문서를 사람과 기계 모두가 읽을 수 있는 형식으로 부호화하는 규칙의 집합을 정의함
- **레이아웃**
  - 배치 그 자체를 나타냄. 출력(output)의 양식이나 양식의 설계 등을 모두 레이아웃이라는 말로 사용함
- **안드로이드 액티비티**
  - 안드로이드 어플리케이션의 화면을 구성하는 컴포넌트이며 여러 개의 View로 구성됨
- **View**
  - 안드로이드의 사용자 인터페이스를 구성하는 핵심으로서 화면상의 사각영역에 자신의 모양을 그리고 사용자의 입력을 받아들이는 객체
- **런타임(runtime)**
  - 컴퓨터 프로그램이 실행되고 있는 동안의 동작을 말함
- **안드로이드 앱 컴포넌트(어플리케이션 컴포넌트)**
  - 액티비티 (activity), 서비스 (service), 브로드캐스트 리시버 (broadcast receiver), 콘텐트 프로바이더 (content provider)
- **aapt(Android Asset Packagint Tool)**
  - /res 폴더에 새로운 리소스(이미지, 동영상 등)이 추가되면 자동으로 리소스를 컴파일하고, 이에 대한 정보를 R.java 파일에 반영함
- **Dalvik**
  - JIT(Just In Time) 방식의 컴파일 환경을 기반으로 안드로이드 스마트폰의 가상머신
- **ART(Aondroid RunTime)** 
  - 앱을 설치하기 전에 컴파일을 끝내고 앱을 실행하는 안드로이드 스마트폰의 가상머신(LOLIPOP 이후의 가상머신)
- **ADB(Android Debug Bridge)**
  - 컴퓨터에서 스마트폰을 제어할 수 있는 셀스크립트 기반의 안드로이드 개발 도구