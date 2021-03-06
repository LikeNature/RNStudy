# Android IDE

## 1. 주요 단축키 모음
Ctrl + Shift + A : 액션찾기
Ctrl + Space : 자동완성
Alt + Insert : 코드생성
Ctrl + / : 주석처리
Alt + Enter : 경고확인 및 퀵픽스
Ctrl + Alt + I : 자동 들여쓰기
Ctrl + B : 선언보기
Ctrl + Alt + Shift + F7 : 사용하는 곳 찾기
Ctrl + F9 : 프로젝트 빌드
Shift + F10 : 프로젝트 실행
Ctrl + G : 라인점프
Ctrl + U : 부모클래스 확인
Ctrl + H : 타입계층 확인
Ctrl + Shift + H : 메소드계층 확인
Ctrl + Alt + H : 콜계층 확인
Shift + F6 : 이름 바꾸기
Ctrl + Alt + M : 함수 추출하기
Ctrl + J : 라이브 템플릿 넣기

모든 단축키 확인하기 :  [Help→ Default Keymap Reference] 

## 2. AVD 변경(애뮬레이터 <-> 디바이스)

```bash
# 디바이스 이름 확인
adb devices

# 실행 디바이스 변경 명령-
adb -s [실행하고자하는 디바이스이름] reverse tcp:8081 tcp:8081

# 디바이스 개발자 메뉴 open
adb shell input key
```

## 3. WebVeiw 

### 1. Linking

https://reactnative.dev/docs/linking

```tsx
import { Linking } from 'react-native';
```

```tsx
// 사용예

<TouchableOpacity
    accessibilityRole="button"
    onPress={() => Linking.openURL(link)}  // Linking 사용
    style={styles.linkContainer}>
    <Text style={styles.link}>{title}</Text>
    <Text
        style={[
            styles.description,
            {
                color: isDarkMode ? Colors.lighter : Colors.dark,
            },
        ]}>
        {description}
    </Text>
</TouchableOpacity>
```

