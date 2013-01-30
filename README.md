     // roboetry
     ========

     UrbiScript code to control a typing robot on a linux system using Robotic/Dynamixel servos. Callibrated to a ThinkPad X60 12" laptop.


     //ROBOETRY: Steph Horak & Philip Dickinson
     //Written by P Dickinson, commented by S Horak

load("/home/student/dev/urbi/urbi-for-bioloid/dynamixel.u");
load("/home/student/dev/urbi/scripts/armPosition.u");
var Global.d = Dynamixel.new;

     //load the above files. armPosition.u will allow us to setup the dictionary. The positions of the dictionary are set in relation to a ThinkPad X Series.
     //this is the contructor 
     //initiate each servo and name it. In this instance L[name] referring to joints in left arm, R[name] referring to joints in right arm.

class Thing
   {
function init() {
  var this.lshoulder = Dynamixel.Device.new(d,5,Dynamixel.DeviceDesc.AX12); //instantiate each servo
  var this.lelbow = Dynamixel.Device.new(d,12,Dynamixel.DeviceDesc.AX12);
  var this.lwrist = Dynamixel.Device.new(d,9,Dynamixel.DeviceDesc.AX12); 
	var this.lfinger = Dynamixel.Device.new(d,4,Dynamixel.DeviceDesc.AX12);

  var this.rshoulder = Dynamixel.Device.new(d,2,Dynamixel.DeviceDesc.AX12); //instantiate each servo
  var this.relbow = Dynamixel.Device.new(d,1,Dynamixel.DeviceDesc.AX12);
  var this.rwrist = Dynamixel.Device.new(d,3,Dynamixel.DeviceDesc.AX12); 
	var this.rfinger = Dynamixel.Device.new(d,14,Dynamixel.DeviceDesc.AX12);
             
  //var this.sensor = Dynamixel.Device.new(d,100,Dynamixel.DeviceDesc.AXS1); //instantiate the sensor  

     //set the speed of movement
	var this.moveSpeed = 1.0;
  setComplianceMargins();
	 //set speeds
	setMovingSpeeds();

    //DICTIONNAIRE -instantiate the dictionary for servo co-ordinates mapped to keyboard alphabet positions 
	
  var this.dictionnaire = Dictionary.new;
	this.setupDictionary();
};

  function setComplianceMargins() {
	//set margin of error
	lshoulder.cwMargin = 0;
	sleep(0.1);
	lshoulder.ccwMargin = 0;
	sleep(0.1);
	lelbow.cwMargin = 0;
	sleep(0.1);
	lelbow.ccwMargin = 0;
	sleep(0.1);
	lwrist.cwMargin = 0;
	sleep(0.1);
	lwrist.ccwMargin = 0;
	sleep(0.1);
	rshoulder.cwMargin = 0;
	sleep(0.1);
	rshoulder.ccwMargin = 0;
	sleep(0.1);
	relbow.cwMargin = 0;
	sleep(0.1);
	relbow.ccwMargin = 0;
	sleep(0.1);
	rwrist.cwMargin = 0;
	sleep(0.1);
	rwrist.ccwMargin = 0;
	sleep(0.1);
  };

 function setMovingSpeeds() {
	lshoulder.targetSpeed = moveSpeed;
	sleep(0.1);
	lshoulder.targetSpeed = moveSpeed;
	sleep(0.1);
	lelbow.targetSpeed = moveSpeed;
	sleep(0.1);
	lelbow.targetSpeed = moveSpeed;
	sleep(0.1);
	lwrist.targetSpeed = moveSpeed;
	sleep(0.1);
	lwrist.targetSpeed = moveSpeed;
	sleep(0.1);
	rshoulder.targetSpeed = moveSpeed;
	sleep(0.1);
	rshoulder.targetSpeed = moveSpeed;
	sleep(0.1);
	relbow.targetSpeed = moveSpeed;
	sleep(0.1);
	relbow.targetSpeed = moveSpeed;
	sleep(0.1);
	rwrist.targetSpeed = moveSpeed;
	sleep(0.1);
	rwrist.targetSpeed = moveSpeed;
	sleep(0.1);
  };

     //setup the dictionary. Mapping the position coordinates of shoulder, elbow and wrist of each arm according to letter position on keyboard; defining arm (L or R), angle of finger joint movement//

  function setupDictionary() {
  
	dictionnaire.set("a", armPosition.new(0.406902, -0.217526, 1.57387, "L", 1.2, 1.05));
	dictionnaire.set("b", armPosition.new(-0.345483, -0.212408, 1.0000, "L", 1.30, 1.05));
	dictionnaire.set("c", armPosition.new(0.0639783, -0.212408, 1.4152, "L", 1.2, 1.05));
	dictionnaire.set("d", armPosition.new(0.0895697, -0.212408, 1.32307, "L", 1.2, 1.05));
	dictionnaire.set("e", armPosition.new(0.0793331, -0.166344, 1.15929, "L", 1.2, 1.05));
	dictionnaire.set("f", armPosition.new(-0.0690966, -0.166344, 1.15929, "L", 1.2, 1.05));
	dictionnaire.set("g", armPosition.new(-0.253354, -0.156107, 0.928966, "L", 1.2, 1.05));
	dictionnaire.set("h", armPosition.new(0.488795, -0.166344, -0.637224, "R", 1.2, 1.05));
	dictionnaire.set("i", armPosition.new(0.227763, -0.145871, -0.821482, "R", 1.2, 1.0));
	dictionnaire.set("j", armPosition.new(0.258473, -0.130516, -0.923847, "R", 1.2, 1.0));
	dictionnaire.set("k", armPosition.new(0.0742149, -0.130516, -1.11834, "R", 1.2, 1.0));
	dictionnaire.set("l", armPosition.new(-0.0998062, -0.094688, -1.29236, "R", 1.2, 1.0));
	dictionnaire.set("m", armPosition.new(0.094688, -0.0690966, -1.21047, "R", 1.2, 1.0));
	dictionnaire.set("n", armPosition.new(0.258473, -0.0690966, -1.04157, "R", 1.2, 1.1));
	dictionnaire.set("o", armPosition.new(0.0230322, -0.0690966, -1.09275, "R", 1.2, 0.92));
	dictionnaire.set("p", armPosition.new(-0.115161, -0.0742149, -1.20535, "R", 1.2, 1.05));
	dictionnaire.set("q", armPosition.new(0.386429, -0.140752, 1.42544, "L", 1.2, 1.05));
	dictionnaire.set("r", armPosition.new(-0.0895697, -0.0998062, 1.00062, "L", 1.2, 1.05));
	dictionnaire.set("s", armPosition.new(0.278946, -0.094688, 1.46127, "L", 1.2, 1.05));
	dictionnaire.set("t", armPosition.new(-0.273827, -0.0844514, 0.801009, "L", 1.2, 1.05));
	dictionnaire.set("u", armPosition.new(0.350601, -0.0588601, -0.688407, "R", 1.2, 0.9));
	dictionnaire.set("v", armPosition.new(-0.0639783, -0.0793331, 1.26677, "L", 1.2, 1.05));
	dictionnaire.set("w", armPosition.new(0.258473, -0.0844514, 1.32819, "L", 1.2, 1.05));
	dictionnaire.set("x", armPosition.new(0.237999, -0.197053, 1.56363, "L", 1.2, 1.05));
	dictionnaire.set("y", armPosition.new(0.662816, -0.0588601, -0.289182, "R", 1.2, 0.9));
	dictionnaire.set("z", armPosition.new(0.396666, -0.191935, 1.70182, "L", 1.2, 1.05));


//------NUMERIC KEYBOARD SETUP-----//

	dictionnaire.set("1", armPosition.new(0.32501, -0.125398, 1.28213, "L", 1.2, 1.05));
	dictionnaire.set("2", armPosition.new(0.181698, -0.125398, 1.15929, "L", 1.2, 1.05));
	dictionnaire.set("3", armPosition.new(0.0281505, 0.0998062, 0.980148, "L", 1.2, 1.05));
	dictionnaire.set("4", armPosition.new(-0.20729, -0.186817, 0.749826, "L", 1.1, 1.05));        
	dictionnaire.set("5", armPosition.new(-0.458085, -0.217526, 0.437612, "L", 1.3, 1.05));
	dictionnaire.set("6", armPosition.new(-0.667934, -0.0998062, 0.166344, "L", 1.3, 1.05));
	dictionnaire.set("7", armPosition.new(0.673052, -0.161225, -0.0844514, "R", 1.2, 1.2));	
	dictionnaire.set("8", armPosition.new(0.59116, -0.161225, -0.130516, "R", 1.2, 1.2));
	dictionnaire.set("9", armPosition.new(0.284064, -0.20729, -0.616751, "R", 1.2, 1.2));
	dictionnaire.set("0", armPosition.new(0.094688, -0.212408, -0.831718, "R", 1.2, 1.2));


//-----SYMBOLS, FUNCTIONS & EXCEPTIONS SETUP-----//

	dictionnaire.set("-", armPosition.new(-0.0844514, -0.212408, -1.02109, "R", 1.2, 1.4));
	dictionnaire.set("=", armPosition.new(-0.243118, -0.212408, -1.17976, "R", 1.2, 1.4));	
	dictionnaire.set("¬¨", armPosition.new(-0.401784, -0.212408, -1.27701, "R", 1.2, 1.0));//backspace key
	dictionnaire.set("#", armPosition.new(-0.514386, -0.217526, -1.65064, "R", 1.2, 1.0));	
  dictionnaire.set("@", armPosition.new(-0.550214, -0.212408, -1.61993, "R", 1.2, 1.0));//Return/ENTER
	dictionnaire.set("?", armPosition.new(-0.345483, 0.00729, -1.666, "R", 1.2, 1.0));	
	dictionnaire.set(" ", armPosition.new(0.289182, -0.20729, -1.15417, "R", 1.2, 1.5));//Right SPACEBAR
	dictionnaire.set("[", armPosition.new(-0.934084, -0.391547, 0.232881, "L", 1.2, 1.0));//Left SPACEBAR
	dictionnaire.set(".", armPosition.new(-0.191935, -0.227763, -1.54316, "R", 1.2, 1.2));
	dictionnaire.set(",", armPosition.new(-0.0230322, -0.232881, -1.38961, "R", 1.2, 1.2));	
	dictionnaire.set("'", armPosition.new(-0.309655, -0.237999, -1.52268, "R", 1.2, 1.2));
	dictionnaire.set(";", armPosition.new(-0.202172, -0.145871, -1.41008, "R", 1.2, 1.0));	
	dictionnaire.set("/", armPosition.new(-0.391547, -0.079331, -1.68135, "R", 1.2, 1.0));
	dictionnaire.set("`", armPosition.new(0.181698, -0.222645, 0.888019, "L", 1.2, 1.0));//ESCAPE
	//dictionnaire.set("¬", armPosition.new(-0.237999, -0.237999, -1.7223, "R", 1.2, 1.0));//CONTROL
	//dictionnaire.set("~", armPosition.new(0.44273, 0.0895697, 1.77348, "L", 1.2, 1.0));//Windows Home	
	dictionnaire.set("{", armPosition.new(0.64817, 0.263591, 1.77348, "L", 1.1, 1.05));//Left SHIFT
  dictionnaire.set("}", armPosition.new(-0.56045, -0.0793331, -1.79395, "R", 1.2, 1.4));//Right SHIFT
  dictionnaire.set("*", armPosition.new(-0.0281505, 0.00255913, 1.6097, "L", 1.3, 1.4));//LEFT MOUSE button
    
};

     //Creating SHIFT function with both hands in use at same time. Need to know which hand is pressing the letter to tell the other hand to press shift; which letters need a shift key function (e.g. capital letters, punctuation marks ()?! etc)  
  
  function moveFinger(var hand, var lfd, var rfd, var mode) {
	if(hand == "L") {
		var upPosition = 0;
	if (mode==0 || mode==1) {
			lfinger.targetPos = upPosition + lfd;
			sleep(0.4);
};
	
  if (mode==0 || mode==2) {
			lfinger.targetPos = upPosition;
			sleep(0.4);
};

 } else {
		var upPosition = 1.5;
		if (mode==0 || mode==1) {
			rfinger.targetPos = upPosition - rfd;
			sleep(0.4);
};
		if (mode==0 || mode==2) {
			rfinger.targetPos = upPosition;
			sleep(0.4);
		};
	};
};

     //identify the range of capital letters using ASCII values
  function isUpperCase(var letter) {
	if(letter.toAscii() > 64 && letter.toAscii() < 91) {
		return true;
	};
	return false;
};

     //create exceptions where shift is pressed with one arm and key is pressed with another. ASCII keycodes are used here as duplicate letters are used (for example '!' is the same as key '1':
  
  function typeWord(var word) {
   	for(var i=0; i<word.length; i++) {
  
  if(word[i].toAscii == 33){
			//!
			moveToKey("}", 1);
			moveToKey("1", 0);
			moveToKey("}", 2);
	
  } else if(word[i].toAscii == 34){
			//"
			moveToKey("}", 1);
			moveToKey("2", 0);
			moveToKey("}", 2);
	
  } else if(word[i].toAscii == 63){
			//?
			moveToKey("{", 1);
			moveToKey("?", 0);
			moveToKey("{", 2);
	
  } else if(word[i].toAscii == 126){
			//~
			moveToKey("{", 1);
			moveToKey("#", 0);
			moveToKey("{", 2);
	
  } else if(word[i].toAscii == 95){
			//_
			moveToKey("{", 1);
			moveToKey("-", 0);
			moveToKey("{", 2);
	
  }  else if(word[i] == "%"){
			sleep(1);
	
  }  else if(isUpperCase(word[i])){
			//upper case
			var shiftHand = "A";
			if(dictionnaire.get(word[i].toLower()).hand == "L"){
				//press right shift
				shiftHand = "R";
				moveToKey("}", 1);
	} else {
				//press left shift
				shiftHand = "L";
				moveToKey("{", 1);
};

  moveToKey(word[i].toLower(), 0);
			//release shift
			if(shiftHand == "L"){
				moveToKey("{", 2);
			} else {
				moveToKey("}", 2);
};
	} else {
			moveToKey(word[i], 0);
		};
	};
};
    
  function moveToKey(var k, var mode) {
  
	  if(dictionnaire.get(k).hand == "L"){
		    sleepMoveL(dictionnaire.get(k).spos, dictionnaire.get(k).epos, dictionnaire.get(k).wpos);
		    moveFinger("L", dictionnaire.get(k).lFingerDistance, dictionnaire.get(k).rFingerDistance, mode);
  	} else {
		    sleepMoveR(dictionnaire.get(k).spos, dictionnaire.get(k).epos, dictionnaire.get(k).wpos);
		    moveFinger("R", dictionnaire.get(k).lFingerDistance, dictionnaire.get(k).rFingerDistance, mode);
	}
};

  function sleepMoveL(var first, var second, var third) {
	this.lshoulder.targetPos = first;
	sleep(0.5);
	this.lelbow.targetPos = second;
	sleep(0.5);
	this.lwrist.targetPos = third;
	sleep(1.0);
};

  function sleepMoveR(var first, var second, var third) {
	this.rshoulder.targetPos = first;
	sleep(0.5);
	this.relbow.targetPos = second;
	sleep(0.5);
	this.rwrist.targetPos = third;
	sleep(1.0);
};

  function getPositionsL() {
	echo("lshoulder: " + lshoulder.position + "\n");
	echo("lelbow: " + lelbow.position + "\n");
	echo("lwrist: " + lwrist.position + "\n");
};

    //create a function to manually move the position of the servos to desired letter, and to get the position data to type into the dictionary.

 function getPositionsR() {
	echo("rshoulder: " + rshoulder.position + "\n");
	echo("relbow: " + relbow.position + "\n");
	echo("rwrist: " + rwrist.position + "\n");
};

    //To create a function to unlock each servo for testing purposes.
	
  function unlock() {
	  lshoulder.load=0;
	  sleep(0.1);
	  lelbow.load=0;
	  sleep(0.1);
	  lwrist.load=0;
	  sleep(0.1);
	  rshoulder.load=0;
	  sleep(0.1);
	  relbow.load=0;
	  sleep(0.1);
	  rwrist.load=0;
	  sleep(0.1);
	  lfinger.load=0;
	  sleep(0.1);
	  rfinger.load=0;
	  sleep(0.1);
};

    //do not use, can't write parallel

  function moveAll(var amount) {
	move(1, amount) & move(2, amount) & move(3, amount);
};

  function getPosition() {
	echo(this.lshoulder.position);
  }
};
    //text file input for robot to type
var t = Thing.new;
var someText = File.new("testing.txt").asList;
for(var i=0; i<someText.size; i++){
	t.typeWord(someText[i]);
	t.typeWord("@");
}
