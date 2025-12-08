# CtbAI
**Last updated - [`v1.0.6`](https://github.com/ctb-os/CtbAI/releases/tag/v1.0.6)**

> AI 관련 서비스

</br>

## Index
 - [Feature](#feature)
   - [Base Service](#base-service)
   - [Translation](#translation)
     - [Edge Case](#edge-case)
     - [API](#api)
 - [How to binding](#how-to-binding)


</br>
</br>

## Feature

### Base-Service
  > 서비스 작업 Base class(abstract class)

  **Default process**
  - 기본 요청 처리는 [Message](https://developer.android.com/reference/android/os/Message) 객체로 상호작용
  - 각 요청은 병렬(coroutine)로 처리
  - 바인드 방식 사용
  - abstract value - `TAG` `TIME_OUT`
  - 반환 데이터 - `what` = Request what(요청 값) or Error(음수)

  **Default Error Desc**  
  what
  - `what = -1` - 기타 에러(catch Exception)
  - `what = -2` - 작업 시간이 `TIME_OUT`을 넘길 경우

  data
  - "error" - Exception.message(String)
  - "what" - requestWhat(Int)

</br>
</br>

### Translation
> 번역기
> TAG = `CTB_AI_TranslationService`  
> TIME_OUT = 10,000ms  
> Action = `com.ctb.ai.translation`  
> Class = `com.ctb.ai.translation.Main`

</br>

#### Edge Case
- **언어 세팅(`100` `201` `211`)**  
  1. 입출력 언어가 같은 경우
  2. 지원하지 않는 언어일 경우
  
  언어 변경이 이뤄지지 않습니다.

- **번역(`200` `201` `210` `211`)**
  1. 언어 설정이 이뤄지지 않은 경우
  2. 입력 문자의 언어 감지 결과가 출력언어와 같을 경우
  3. (201, 211)에서 언어 변경이 이뤄지지않은 경우

  입력 값과 같은 값을 반환합니다.

</br>

#### API
<table>
  <tr>
    <th>Title</th>
    <th>what</th>
    <th colspan="4">요청 data</th>
    <th colspan="4">반환 data</th>
  </tr>
  <tr>
    <th> </th>
    <th> </th>
    <th>key</th>
    <th>type</th>
    <th>optional</th>
    <th>description</th>
    <th>key</th>
    <th>type</th>
    <th>optional</th>
    <th>description</th>
  </tr>
  <tr style="height:1px">
    <td><pre>                  </pre></td><!-- 줄바꿈안되게 공간차지 -->
    <td></td><td></td><td></td><td></td>
    <td><pre>                  </pre></td><!-- 줄바꿈안되게 공간차지 -->
    <td></td><td></td><td></td>
    <td><pre>                  </pre></td><!-- 줄바꿈안되게 공간차지 -->
  </tr>
  <tr>
    <td>연결 종료</td>
    <td>-1</td>
    <td colspan="4"></td>
    <td colspan="4"></td>
  </tr>
  <tr>
    <td rowspan="4">번역 가능한 언어 목록</td>
    <td rowspan="4">0</td>
    <td rowspan="4" colspan="4"></td>
    <td>sourceList</td>
    <td>StringArray</td>
    <td>X</td>
    <td>설정 가능한 입력 언어 코드 리스트</td>
  </tr>
  <tr>
    <td>sourceStrList</td>
    <td>StringArray</td>
    <td>X</td>
    <td>UI용 언어 리스트</td>
  </tr>
  <tr>
    <td>targetList</td>
    <td>StringArray</td>
    <td>X</td>
    <td>설정 가능한 출력 언어 코드 리스트</td>
  </tr>
  <tr>
    <td>targetStrList</td>
    <td>StringArray</td>
    <td>X</td>
    <td>UI용 언어 리스트</td>
  </tr>
  <tr>
    <td rowspan="2">입력 값에 대한 언어 감지 결과</td>
    <td rowspan="2">1</td>
    <td rowspan="2">input</td>
    <td rowspan="2">String</td>
    <td rowspan="2">X</td>
    <td rowspan="2">감지할 내용</td>
    <td>sourceList</td>
    <td>StringArray</td>
    <td>X</td>
    <td>식별한 설정 가능한 입력 언어 코드 리스트, 가능성 높은 순</td>
  </tr>
  <tr> <td>sourceStrList</td> <td>StringArray</td> <td>X</td> <td>UI용 언어 리스트</td> </tr>
  <tr>
    <td rowspan="2">언어 세팅 및 초기화</td>
    <td rowspan="2">100</td>
    <td>source</td>
    <td>String</td>
    <td>X</td>
    <td>입력 언어 코드</td>
    <td>source</td>
    <td>String</td>
    <td>X</td>
    <td>설정된 입력 언어 코드</td>
  </tr>
  <tr> <td>target</td> <td>String</td> <td>X</td> <td>출력 언어 코드</td> <td>target</td> <td>String</td> <td>X</td> <td>설정된 출력 언어 코드</td> </tr>
  <tr>
    <td rowspan="6">번역</td>
    <td rowspan="6">200</td>
    <td rowspan="6">input</td>
    <td rowspan="6">String</td>
    <td rowspan="6">X</td>
    <td rowspan="6">입력 값</td>
    <td>input</td>
    <td>String</td>
    <td>X</td>
    <td>입력 값</td>
  </tr>
  <tr> <td>output</td><td>String</td><td>X</td><td>번역 값</td> </tr>
  <tr> <td>source</td><td>String</td><td>X</td><td>설정된 입력 언어 코드</td> </tr>
  <tr> <td>sourceStr</td><td>String</td><td>X</td><td>UI용 언어</td> </tr>
  <tr> <td>target</td><td>String</td><td>X</td><td>설정된 출력 언어 코드</td> </tr>
  <tr> <td>targetStr</td><td>String</td><td>X</td><td>UI용 언어</td> </tr>
  <tr>
    <td rowspan="6">언어 세팅 및 번역</td>
    <td rowspan="6">201</td>
    <td>input</td><td>String</td><td>X</td><td>입력 값</td>
    <td>input</td><td>String</td><td>X</td><td>입력 값</td>
  </tr>
  <tr>
    <td>source</td><td>String</td><td>O</td><td>입력 언어 코드, default: 입력 감지</td>
    <td>output</td><td>String</td><td>X</td><td>번역 값</td>
  </tr>
  <tr>
    <td>target</td><td>String</td><td>O</td><td>출력 언어 코드, default: 시스템 언어</td>
    <td>source</td><td>String</td><td>X</td><td>설정 "시도"된 입력 언어 코드 (설정되지 않을 수 있음)</td>
  </tr>
  <tr>
    <td rowspan="3" colspan="4"> </td>
    <td>sourceStr</td><td>String</td><td>X</td><td>UI용 언어</td>
  </tr>
  <tr> <td>target</td><td>String</td><td>X</td><td>설정 "시도"된  출력 언어 코드 (설정되지 않을 수 있음)</td></tr>
  <tr> <td>targetStr</td><td>String</td><td>X</td><td>UI용 언어</td></tr>
  
  <tr>
    <td rowspan="6">다중 번역</td>
    <td rowspan="6">210</td>
    <td>inputs</td><td>StringArray</td><td>X</td><td>입력 값 리스트</td>
    <td>inputs</td><td>StringArray</td><td>X</td><td>입력 값 리스트</td>
  </tr>
  <tr>
    <td rowspan="5" colspan="4"> </td>
    <td>outputs</td><td>StringArray</td><td>X</td><td>번역 값 리스트</td>
  </tr>
  <tr> <td>source</td><td>String</td><td>X</td><td>설정된 입력 언어 코드</td> </tr>
  <tr> <td>sourceStr</td><td>String</td><td>X</td><td>UI용 언어</td> </tr>
  <tr> <td>target</td><td>String</td><td>X</td><td>설정된 출력 언어 코드</td> </tr>
  <tr> <td>targetStr</td><td>String</td><td>X</td><td>UI용 언어</td> </tr>
  <tr>
    <td rowspan="6">언어 세팅 및 다중 번역</td>
    <td rowspan="6">211</td>
    <td>inputs</td><td>StringArray</td><td>X</td><td>입력 값 리스트</td>
    <td>inputs</td><td>StringArray</td><td>X</td><td>입력 값 리스트</td>
  </tr>
  <tr>
    <td>source</td><td>String</td><td>O</td><td>입력 언어 코드, default: 입력 감지(첫번째 문자열)</td>
    <td>outputs</td><td>StringArray</td><td>X</td><td>번역 값 리스트</td>
  </tr>
  <tr>
    <td>target</td><td>String</td><td>O</td><td>출력 언어 코드, default: 시스템 언어</td>
    <td>source</td><td>String</td><td>X</td><td>설정 "시도"된 입력 언어 코드 (설정되지 않을 수 있음)</td>
  </tr>
  <tr>
    <td rowspan="3" colspan="4"> </td>
    <td>sourceStr</td><td>String</td><td>X</td><td>UI용 언어</td>
  </tr>
  <tr> <td>target</td><td>String</td><td>X</td><td>설정 "시도"된 출력 언어 코드 (설정되지 않을 수 있음)</td> </tr>
  <tr> <td>targetStr</td><td>String</td><td>X</td><td>UI용 언어</td> </tr>
</table>

</br>
</br>

## How to binding
> // package name은 고정  
> const value PACKAGE_NAME = "com.ctb.ai"  
> 
> // Translation 기준 예시  
> const value ACTION = "com.ctb.ai.translation"  
> const value CLASS = "com.ctb.ai.translation.Main"


1. **Manifest 설정**
```
<!-- Manifest (android 13 이후 필수) -->
    <!-- 패키지로 추가 -->
    <queries>
        <package android:name=PACKAGE_NAME />
    </queries>

    <!-- 액션으로 추가 -->
    <queries>
        <intent>
            <action android:name=ACTION />
        </intent>
    </queries>
```

2. **bind service**
```
// connection 설정
private var serviceMessenger: Messenger? = null
private val serviceConnection: ServiceConnection = object : ServiceConnection {
    override fun onServiceConnected(className: ComponentName, service: IBinder) {
        serviceMessenger = Messenger(service)
    }
    override fun onServiceDisconnected(className: ComponentName) {
        serviceMessenger = null
    }
}

// 1. 액션으로 연결
val intent = Intent(ACTION)
intent.setPackage(PACKAGE_NAME)

context.bindService(intent, serviceConnection, Context.BIND_AUTO_CREATE)

// 2. 클래스명으로 연결
val intent = Intent()
intent.setClassName(PACKAGE_NAME, CLASS)
intent.component = ComponentName(PACKAGE_NAME, CLASS)

context.bindService(intent, serviceConnection, Context.BIND_AUTO_CREATE)
```

3. 서비스 호출 **요청** 값 작성
```
fun exampleTranslate(
    what: Int, // 요청 분류
    input: String = "번역할 문장",
    source: String = "ko",
    target: String = "en"
) {
    val bundle = bundleOf()
    if(what == 0) {
        // 요청 값 X
    } else if(what == 1) {
        bundle.putString("input", input)
    } else if(what == 100) {
        bundle.putString("source", source)
        bundle.putString("target", target)
    } else if(what == 200) {
        bundle.putString("input", input)
    } else if(what == 201) {
        bundle.putString("input", input)
        bundle.putString("source", source)
        bundle.putString("target", target)
    }
    
    val msg: Message = Message.obtain(null, what)
    msg.data = bundle
    msg.replyTo = clientMessenger // 4 에서 작성할 응답 처리
    serviceMessenger.send(msg)
}
```
4. 서비스 호출 **응답** 값 작성
```
val clientMessenger: Messenger = Messenger(object : Handler(Looper.getMainLooper()) {
    override fun handleMessage(msg: Message) {
        if(msg.what == 0) {
            val sourceList: Array<String>    = msg.data.getStringArray("sourceList")!!
            val sourceStrList: Array<String> = msg.data.getStringArray("sourceStrList")!!
            val targetList: Array<String>    = msg.data.getStringArray("targetList")!!
            val targetStrList: Array<String> = msg.data.getStringArray("targetStrList")!!
        } else if(msg.what == 1) {
            val sourceList: Array<String>    = msg.data.getStringArray("sourceList")!!
            val sourceStrList: Array<String> = msg.data.getStringArray("sourceStrList")!!
        } else if(msg.what == 100) {
        } else if(msg.what == 200 || msg.what ==201) {
            val output: String    = msg.data.getString("output")!!
            val source: String    = msg.data.getString("source")!!
            val sourceStr: String = msg.data.getString("sourceStr")!!
            val target: String    = msg.data.getString("target")!!
            val targetStr: String = msg.data.getString("targetStr")!!
        }

        // todo
    }
})
```


 
