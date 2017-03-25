# CustomWidget


### 1. 신규 속성을 attrs.xml에 정의
```xml
    <declare-styleable name="Today">
        <attr name="delimeter" format="string" />
    </declare-styleable>
```

### 2. 커스텀할 위젯을 상속받은 후 재 정의
```java
public class Today extends TextView {
    /**
    * attrs : 레이아웃 xml 파일에 정의된 속성의 이름과 값이 배열로 저장
    */
    public Today(Context context, AttributeSet attrs) {
        super(context, attrs);
        // # 커스텀 위젯에 커스텀 속성 사용하기
        // 1. res/values/attrs.xml 에 정의된 어트리뷰트를 가져온다
        TypedArray typed = context.obtainStyledAttributes(attrs, R.styleable.Today);
        // 2. 해당 이름으로 정의된 속성의 개수를 가져오고
        int size = typed.getIndexCount();
        // 3. 반복문을 돌면서 해당 속성에 대한 처리를 해준다
        for(int i=0 ; i<size ; i++){
            // 3.1 현재 속성의 아이디 가져오기
            int current_attr = typed.getIndex(i);

            switch(current_attr){
                // 3.2 아이디가 attrs.xml에 정의된 속성아이디와 같다면
                case R.styleable.Today_delimeter:
                    // 3.3 현재 속성에 입력되어 있는 값을 꺼낸다
                    String delimeter = typed.getString(current_attr);
                    runTask(delimeter);
                    break;
            }
        }
    }
}
```

### 3. 레이아웃에서 사용
```xml
    <!-- xmlns:custom="커스텀 스키마 적용" -->
    <!-- custom:newAttribute="value" -->
    <package.Today
        xmlns:custom="http://schemas.android.com/apk/res-auto"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        custom:delimeter=":::"
        android:text="aaa" />
```
