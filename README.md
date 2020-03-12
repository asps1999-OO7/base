// # base
import'package:flutter/material.dart';
import './question.dart';
import'./answer.dart';


void main(){
  runApp(MyApp());
}
class MyApp extends StatefulWidget {

  @override
  State<StatefulWidget> createState() {
    // TODO: implement createState
    return _MyAppState();
  }
}

class _MyAppState extends State<MyApp>{  //_ before the MyAppState class makes is private
  var _questionindex=0;  // _ makes it private
  void _answerquestion(){
    setState(() {          // setState works as a function which changes the question from color to animal in our case
    _questionindex = _questionindex+1;//print('answer chosen ') coomand can also be choosen to print anserchoosen when a button is pressed  
    
    });
    
    print(_questionindex); 
    //print('answer choosen');
  }
  @override
 Widget build(BuildContext context){
   const  question =[                      // final can be used when we are not intended to change some value and const is been used because it shows the compile time constaant not run time constant
     {'questiontext':'what\'s your favourite color','answer':['black','white','red','pink']},
     {'questiontext':'what\'s your favourite animal','answer':['tiger','elephant','cow','horse']},
     {'questiontext':'who is your favourite entreprenuer','answer':['jeff','mark','elon','steve']},// now question is a map
     
   ];
    return MaterialApp(home: Scaffold(
      appBar: AppBar(title: Text('My First App'),),
      
      body:Column(children: [
        Question(question[_questionindex]['questiontext'],),// as question is a map now to access the element of a map we use a another square bracket 
        /*Answer(_answerquestion), // name instead of result of  the  function
        Answer(_answerquestion),
        Answer(_answerquestion), // we can do as above or we can call a anonymous function this is used if only1 pressed button for instance*/
        ...(question[_questionindex]['answer'] as List<String>).map((answer){return Answer(_answerquestion,answer);}).toList()
        
        
      ],//... operator add the elements of one list to th eelement of the another list not add to seperate list
    ),
    ),
    );
  }
}
import'package:flutter/material.dart';


class Question extends StatelessWidget {
  final String questiontext; // final helps to prvent any change in the questiontext again as it is once changed 
  Question(this.questiontext);  // contructor
  @override
  Widget build(BuildContext context) {
    return Container (width : double.infinity,margin: EdgeInsets.all(10) ,child : Text(questiontext, style: TextStyle(fontSize: 28), textAlign: TextAlign.center , ),);// without the container and child text and most important the width syntax will not be in the centre of the screen
  }                                                                                                                                         // width: double.infinity ensures that container takes as much space as is wants              
}
import 'package:flutter/material.dart';


class Answer extends StatelessWidget {
  final Function selecthandler;
  final String answerText;
  
  Answer(this.selecthandler, this.answerText);// whatever we chhose will be stored in the select handler
  @override
  Widget build(BuildContext context) {
    return Container(width: double.infinity,child:RaisedButton(child: Text(answerText),color:Colors.blue[100],textColor: Colors.black,onPressed: selecthandler,) ,
      
    );
  }
}
