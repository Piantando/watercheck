![Header](/README/header.gif)

# About

**Jack doesn't waste** is a university project built in [p5.js](https://p5js.org/) during the course *Creative Coding* at the Politecnico di Milano. The goal was to develop an interactive app about an ***out of scale*** topic. 

# Project idea

The theme we choose is the **waste of water for domestic consumption**. The user has the chance to take an experience otherwise impossible through a guided path that allows him to find out how much water he uses. <br>
Jack drives the user in three different rooms of the house (bathroom, kitchen and laundry room). There the user has to answer questions about his weekly use of water. The experience ends showing him how much water was used and wasted in a week. The water waste is graphically represented using as unit a tub full of water.  

# Development

To code the app we mostly used Javascript (with [p5.js](https://p5js.org/)) and in support to it we also used HTML and CSS.

## Resources

### [p5.play.js](http://p5play.molleindustria.org/)

Created by Paolo Pedercini, this library provides a *Sprite* class to manage visual objects in 2D space, to create animations and to help mouse and keyboard interactions. p5.play.js is perfect for the creation of games and playthings.

We used this library to add animations to Jack and to the other objects, as well as to simulate a playful experience giving the chance to interact with the characters.

The following examples were written using this library:

* **Create animation**
```
Jack.addAnimation("moving", "images/Jack_walk1.png", "images/Jack_walk2.png");
```
![Jack_moving](/README/Jack_moving.gif)

* **Set velocity to animation**
```
if(mouseX > Jack.position.x + 10) {
    Jack.changeAnimation("moving");
    Jack.mirrorX(1);
    Jack.velocity.x = 5
}
 ```
![Jack_walking](/README/Jack_walking.gif)

* **Change animation**
```
Dish.addAnimation("Dish_none", "images/dish.png");

if (pressHands==true){
    Dish.changeAnimation("Sink");
} else if (pressDishwasher==true){
    Dish.changeAnimation("Dishwasher");
}
```
![GitHub Logo](/README/changeanimation.gif)

* **SetInterval and onMouseOver** 
The *glow effect* of the objects is visible after 3 seconds from the end of a previous action 
```
timeSinkGlow = setInterval(sinkGlow,timeGlow);
```
   or going above the object with the mouse.
```
Sink.onMouseOver = function() {this.changeAnimation("SinkGlow");}
```
![glow_time](/README/glow_time.gif)![glow_mouse](/README/glow_mouse.gif)


### [p5.sound.js](https://p5js.org/reference/#/libraries/p5.sound)
We used this library to load and analyze the sound. <br><br>
Thanks to this function 
```
analyzer.setInput(mySound);
```
we can analyze the sound and the user can play or pause it.<br><br>
The **music** is a *Royalty Free Music* from [Bensound](http://www.bensound.com/royalty-free-music/track/cute).

### [wavePercent](http://codepen.io/ElaineXu/pen/jAzGAw)
This is not a library, but an open source code from [CodePen](http://codepen.io/) created by [Elaine](http://codepen.io/ElaineXu/). <br> We used and modified this animation to fill the screen of water before the results.

![wavepercent](/README/wavepercent.gif)![waves](/README/waves.gif)

## Data
To calculate the amount of water used by the user, we add to the code some arrays with the units of water of different situation (take a shower, brushing teeth, run the dishwasher ...).
```
var bathroomData = [5, 150, 80];
var kitchenData = [5,10,11,15];
var gardenData = [12,1];
var laundryData = [5,33,51,45,48,78,84];
```
Each of these unit is multiplied with the corrisponding value of the answers provided by the user.

![handQ](/README/pressHand.png)
![dishwasherQ](/README/pressDishwasher.png)

We also defined a *default result* for each group of questions to avoid a null value in case the user doesn't answer.
<br><br>
At the end, the results are summed to define the amount of water used, on average, in a week
```
Result = resultMop + resultWMachine + resultGarden + resultDishwasher + resultHand + resultTeeth + resultBath + resultShower;
```
and at this result are subtracted 700 liters of water (the necessary amount for person setted by the World Health Organization) to show the amount wasted. Every 100 liters of water wasted is represented by a tub.
```
var WaterWaste =Math.round(Result - 700, 1);
```

## Challenges
To maintain visually activated the selected answer, we used Javascript to change the CSS class of the clicked buttons and to add them a different style from the others.
```
/* CSS */
.button {
    background: none;
    border: 2.5px solid;
    color: #677f8c;
}
.selected {	
    background-color: #677f8c;
    border: #677f8c 2.5px solid;
    color: white;
}

//JAVASCRIPT
buttonTub.addClass("button");
buttonShower.addClass("button");

if(pressShower===true){
    document.getElementById("buttonShower").className = "selected"; 
    document.getElementById("buttonTub").className = "button";
} else if(pressTub===true){
    document.getElementById("buttonShower").className = "button";
    document.getElementById("buttonTub").className = "selected";
}
```
![className](/README/classname.gif)<br><br><br>
We add to the code also some clickable icons, like the *info button* and the *play/pause sound*. To create them, we used the CSS and we put the icon images in the background of the buttons. <br>
We also make them responsive using the `@media` query.
```
@media screen and (max-width: 1024px)
.info {
    background-image: url(images/info_20.png);
}
.sound {
    background-image: url(images/audio_play_20.png);
}

@media screen and (min-width: 1024px)
.info {
    background-image: url(images/info_25.png);
}
.sound {
    background-image: url(images/audio_play_25.png);
}
```
![className](/README/responsive.gif)

# Team
**Jack doesn't waste** is developed by:
* Mara Cominardi [@phoenis](https://github.com/phoenis) 
* Chiara Riente [@chiarariente](https://github.com/chiarariente) 
* Sara Pizzatti [@sarapizzatti93](https://github.com/sarapizzatti93) <br><br><br>

### And you, do you know how much water do you use? 
Share your result with the hashtags **#JackDoesntWaste #beLikeJack**
