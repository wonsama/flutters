플러터 위젯 소개 - 1

# 211_introduction_to_widgets - 1

[출처] : [Introduction to widgets](https://flutter.io/docs/development/ui/widgets-intro)

> Flutter 위젯은 React에서 영감을 얻어 제작된 프레임워크 입니다. 핵심은 UI를 위젯에서 빌드(제작)하는 것 입니다. 위젯은 현재 설정과 상태에 따라 표현되며, 해당 위젯의 상태가 변경되면 위젯은 자동으로 재빌드 됩니다.

# 배울내용 요약

* flutter 는 state(상태) 변화에 따라 app이 자동으로 재빌드 됨
* Widget build(BuildContext context) 함수의 구현(implement)을 통해 위젯을 구현할 수 있습니다.
* MaterialApp 위젯에서 테마 및 다양한 기본 기능을 제공해주니 일단 쓰세요 :) 


# 헬로 월드 (Hello World)

초간단 flutter 앱 : [runApp](https://docs.flutter.io/flutter/widgets/runApp.html)을 통해 위젯을 기동 !

```
import 'package:flutter/material.dart';

void main() {
  runApp(
    Center(
      child: Text(
        'Hello, world!',
        textDirection: TextDirection.ltr,
      ),
    ),
  );
}
```

* runApp(Widget app) 함수를 통해 기본 위젯트리를 형성합니다. 위젯 트리는 Center - 자식 : Text 로 구성 됩니다.
* 앱기동 - 위젯트리 구성 읽기 - (Center ... Text) : 앱을 중앙으로 위치하며 내부에는 텍스트로 방향을 ltr(왼쪽에서 오른쪽)으로 지정하여 'Hello, World'를 작성
* 앱을 작성할 때 위젯이 상태를 관리하는지 여부에 따라 StatelessWidget 또는 StatefulWidget의 하위 클래스의 위젯을 작성하는 것이 일반적입니다. 
* 위젯의 주요 임무는 빌드 기능을 구현하는 것입니다. `@override Widget build(BuildContext context)`

# 기본적인 위젯 만들기 (Basic widgets)

> Flutter에는 아래와 같이 유용한 기본 위젯을 제공합니다.

[Text](https://docs.flutter.io/flutter/widgets/Text-class.html) : 텍스트 위젯을 사용하면 응용 프로그램 내에서 스타일이 지정된 텍스트를 만들 수 있습니다.

[Row](https://docs.flutter.io/flutter/widgets/Row-class.html), [Collum](https://docs.flutter.io/flutter/widgets/Column-class.html) :이 flex 위젯을 사용하면 가로 (행) 및 세로 (열) 방향 모두에서 유연한 레이아웃을 만들 수 있습니다. 디자인은 웹의 flexbox 레이아웃 모델을 기반으로합니다.

[Stack](https://docs.flutter.io/flutter/widgets/Stack-class.html) : 스택 위젯을 사용하면 직선형 (수평 또는 수직)으로 배치하는 대신 위젯을 페인트 순서대로 서로 쌓을 수 있습니다. 그런 다음 Stack의 하위에있는 [Positioned](https://docs.flutter.io/flutter/widgets/Positioned-class.html) 위젯을 사용하여 스택의 위쪽, 오른쪽, 아래쪽 또는 왼쪽 가장자리를 기준으로 배치 할 수 있습니다. 스택은 웹의 절대 위치 지정 레이아웃 모델을 기반으로합니다.

[Container](https://docs.flutter.io/flutter/widgets/Container-class.html) : 컨테이너 위젯을 사용하여 사각형의 시각적 요소를 만들 수 있습니다. 컨테이너는 배경, 테두리 또는 그림자와 같은 [BoxDecoration](https://docs.flutter.io/flutter/painting/BoxDecoration-class.html) 으로 장식 될 수 있습니다. 컨테이너는 여백, 패딩 및 제약 조건을 크기에 적용 할 수 있습니다. 또한 컨테이너는 행렬을 사용하여 3 차원 공간에서 변형 될 수 있습니다.

```
import 'package:flutter/material.dart';

class MyAppBar extends StatelessWidget {
  MyAppBar({this.title});

  // 위젯의 서브클레스는 항상 final(불변)로 선언 되어야 된다.
  final Widget title;

  @override
  Widget build(BuildContext context) {
    return Container(

      height: 56.0, // 픽셀 단위
      padding: const EdgeInsets.symmetric(horizontal: 8.0),
      decoration: BoxDecoration(color: Colors.blue[500]),
      
      // 행(Row) 은 수평의 선형 레이아웃임
      child: Row(

        // <Widget> 목록 항목의 타입을 나타낸다.
        children: <Widget>[
          IconButton(
            icon: Icon(Icons.menu),
            tooltip: 'Navigation menu',
            onPressed: null, // null 은 버튼을 비활성화 한다
          ),

          // Expanded 는 자식공간에 여유 공간을 확보해 준다.
          Expanded(
            child: title,
          ),
          IconButton(
            icon: Icon(Icons.search),
            tooltip: 'Search',
            onPressed: null,
          ),
        ],
      ),
    );
  }
}

class MyScaffold extends StatelessWidget {
  @override
  Widget build(BuildContext context) {

    // Material 은 UI를 표현하는 컨셉임
    return Material(

      // 열(Column)은 수직 선형 레이아웃임 
      child: Column(
        children: <Widget>[
          MyAppBar(
            title: Text(
              'Example title',
              style: Theme.of(context).primaryTextTheme.title,
            ),
          ),
          Expanded(
            child: Center(
              child: Text('Hello, world!'),
            ),
          ),
        ],
      ),
    );
  }
}

void main() {
  runApp(MaterialApp(
    title: 'My app', // OS 작업 전환기에서 사용됨
    home: MyScaffold(),
  ));
}
```

* `pubspec.yaml` 파일에 `uses-material-design` 항목 값이 true로 설정되어 있는지 여부를 확인해야 된다. 이 설정이 되어 있어야 Material 아이콘을 사용할 수 있음

```
name: my_app
flutter:
  uses-material-design: true
```

* MaterialApp : 테마 기능을 사용하기위해 해당 위젯을 상속받아 구현하는 것을 추천
* MyScaffold 위젯은 하위 항목을 세로 열로 구성합니다. 열의 맨 위에 MyAppBar의 인스턴스를 배치하고 응용 프로그램 막대에 제목으로 사용할 텍스트 위젯을 전달합니다. 위젯을 다른 위젯에 인수로 전달하는 것은 다양한 방법으로 재사용 할 수있는 일반 위젯을 만들 수있는 강력한 기술입니다. 마지막으로 MyScaffold는 Expanded를 사용하여 나머지 공간을 본문으로 채웁니다.

# 다음에 계속

> 내용이 매우 길어요 ... 따라하다 지치면 안되니(제가 지쳐서) 일단 자르고 다음시간에 또 뵙겠습니다.

# 이전 관련 글