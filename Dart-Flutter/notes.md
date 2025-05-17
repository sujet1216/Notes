```dart

class MyWidget extends StatefulWidget {  
const MyWidget({super.key});  
  
@override  
State<MyWidget> createState() => _MyWidgetState();  
}  
  
class _MyWidgetState extends State<MyWidget> {  
double opacity = 1;  
  
@override  
void initState() {  
startAnimating();  
super.initState();  
}  
  
void startAnimating() {  
Future.delayed(const Duration(seconds: 1, milliseconds: 500), () {  
setState(() {  
opacity = opacity == 1 ? 0.5 : 1;  
});  
  
startAnimating();  
});  
}  
  
@override  
Widget build(BuildContext context) {  
  
return Scaffold(  
body: SafeArea(  
child: Center(  
child: AnimatedOpacity(  
duration: const Duration(milliseconds: 250),  
opacity: opacity,  
child: Container(  
height: 200,  
width: 200,  
decoration: BoxDecoration(  
color: Colors.red,  
borderRadius: BorderRadius.circular(20),  
),  
),  
),  
),  
),  
);  
}  
}

```
funqcia idzaxebs tavs da mudmivad ibildeba;

```dart
TextField(
	onTapOutside: (_) {
		FocusManager.instance.primaryFocus?.unfocus();
	},
```


TweenAnimationBuilder **is better when you need the animated value inside multiple widgets** (like opacity + scale together).