# Sharedpreference란?

### 개념
---
- 간단한 값 저장에 DB를 사용하기에는 복잡하기 때문에 SharedPreferences를 사용하면 적합 합니다.

- 보통 초기 설정값이나 자동로그인 여부 등 간단한 값을 저장하기 위해 사용합니다.

- 어플리케이션에 파일 형태로 데이터를 저장합니다.

=> data/data/패키지명/shared_prefs/SharedPreference이름.xml 위치에 저장

- 어플리케이션이 삭제되기 전까지 보존됩니다.


### 목적
---
- 공유된 사용자의 기호를 저장하기 위해 사용됩니다.
- Key-Value 방식입니다.
- 하드하게 데이터베이스 시스템이 구축할 수 없습니다.(할수는 있지만 구축하면 안됩니다.)
