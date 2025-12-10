# CtbTrranslation
**Last updated - [`v1.0.1`](https://github.com/ctb-os/CtbTranslation/releases/tag/1.0.1)**

> 번역기 앱

</br>

## Index
 - [Intent Action](#intent-action)
   - [Text](#text)
     - [시스템 호출](#시스템-호출)
     - [암시적](#암시적)
     - [명시적](#명시적)
   - [Image](#image)
     - [암시적](#암시적-1)
     - [명시적](#명시적-1)

</br>
</br>

## Intent Action
> Package = `com.ctb.translation`
> Class = `com.ctb.translation.IntentActivity`

### Text
> 텍스트 번역 인스턴스 액티비티  
> <img width="360" height="640" alt="screenshot" src="https://github.com/user-attachments/assets/0a2edab9-1b25-4385-8922-d95b8a3b3cd3" />

#### 시스템 호출
> Selectable Text View - 텍스트 선택 시스템 호출

- action.PROCESS_TEXT 지원
<img width="719" height="241" alt="image" src="https://github.com/user-attachments/assets/ba0da193-83cc-4bbf-a142-31c836501e7e" />

- action.TRANSLATE 지원(영문 텍스트)  
<img width="718" height="331" alt="image" src="https://github.com/user-attachments/assets/9feba452-3b4c-40cd-ad6d-70dfb6183a58" />  


#### 암시적
```
val intent = Intent()
intent.setAction(Intent.ACTION_PROCESS_TEXT)
intent.setType("text/plain")

// Set Data  1 or 2
putExtra(Intent.EXTRA_PROCESS_TEXT, "text message") // 1
putExtra(Intent.EXTRA_TEXT, "text message")         // 2

startActivity(intent)
```

#### 명시적
```
val intent = Intent()

// Set target  1 or 2
intent.setClassName("com.ctb.translation", "com.ctb.translation.IntentActivity")                // 1
intent.setComponent(ComponentName("com.ctb.translation", "com.ctb.translation.IntentActivity")) // 2

// Set Data  1 or 2
putExtra(Intent.EXTRA_PROCESS_TEXT, "text message") // 1
putExtra(Intent.EXTRA_TEXT, "text message")         // 2

startActivity(intent)
```

</br>
</br>


### Image
> 사진 번역 인스턴스 액티비티  
> <img width="360" height="640" alt="screenshot" src="https://github.com/user-attachments/assets/839815c6-b621-4523-89bd-29d789ea1da5" /> <img width="360" height="640" alt="screenshot" src="https://github.com/user-attachments/assets/fe3be5ed-ec93-4d43-a896-a6f84ba476f8" />



#### 암시적
```
val intent = Intent()
intent.setAction("com.ctb.translation")

// Set Data and permission
intent.setDataAndType(URI, "image/*")
intent.addFlags(Intent.FLAG_GRANT_READ_URI_PERMISSION)

startActivity(intent)
```

#### 명시적
```
val intent = Intent()

// Set Data and permission
intent.setDataAndType(URI, "image/*")
intent.addFlags(Intent.FLAG_GRANT_READ_URI_PERMISSION)

// Set target  1 or 2
setClassName("com.ctb.translation", "com.ctb.translation.IntentActivity")                // 1
setComponent(ComponentName("com.ctb.translation", "com.ctb.translation.IntentActivity")) // 2

startActivity(intent)
```

