/* Arduino Pomodoro Study Timer

This program sets a timer for the "Pomodoro study method,"
which consists of 25-minute study periods followed by 5-minute breaks.
After every 4 study periods, you take a longer 15 minute break.
However, the duration of each period and the number of repetitions
are fully customizable in the code. 

// declare variables for keeping track of time
// and the number of study sessions
int seconds = 0;
int minutes = 0;
int count = 0;

// declare variables for the length of each
// period and the number of sessions before
// a longer break. Change these to customize
// your timer!
const int study_minutes = 25;
const int short_break_minutes = 5;
const int long_break_minutes = 15;
const int repeats = 4;

// a variable used to time the breaks later
int break_duration;

// declare pins used for hardware
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);
const int led1 = 6;
const int led2 = 7;
const int button = 8;

void setup() 
{
  lcd.begin(16, 2); // Set up the number of columns and rows on the LCD.
  // set LED pins as outputs and button pin as input
  pinMode(led1,OUTPUT);
  pinMode(led2,OUTPUT);
  pinMode(button,INPUT);

  // display initial message to user
  lcd.print("Press button");
  lcd.setCursor(0,1);
  lcd.print("to start");

  // wait for button press to start
  while(digitalRead(button)==LOW){
    // do nothing
  }
}

void loop()
{
  count = 0;  // set count to zero

  while(count<repeats){ // alternate timing between study and breaks

    // print message and set LEDs for study time
    lcd.clear();
    lcd.print("Study time!");
    digitalWrite(led1,HIGH);
    digitalWrite(led2,LOW);
    lcd.setCursor(0, 1);

    // reset minutes and seconds to zero
    seconds = 0;
    minutes = 0;

    // count up and display the timer during study period
    while(minutes<study_minutes){ // keep counting until we've reached the time limit for a study session
      seconds = 0;
      // print out the timer value in mm:ss format 
      while(seconds<60){
        lcd.setCursor(0, 1);
        if(minutes<10){  // if minutes is less than 10, we need to print an extra 0 to the display
          lcd.print("0");
        }
        lcd.print(minutes);
        lcd.print(":");
        if(seconds<10){  // if seconds is less than 10, we need to print an extra 0 to the display
          lcd.print("0");
        }
        lcd.print(seconds);
        // wait for one second then increment the second counter
        delay(1000);
        seconds++;
      }
      // increment the minute counter after 60 seconds have elapsed
      minutes++;
  
    }
    
    // now repeat the process for a study break
    lcd.clear();
    lcd.setCursor(0, 0);
    digitalWrite(led1,LOW);
    digitalWrite(led2,HIGH);

    
    if(count==(repeats-1)){ // do a long break on the last repetition
      break_duration = long_break_minutes;
      lcd.print("Long break!");
    }
    else{  // otherwise do a short break
      break_duration = short_break_minutes;
      lcd.print("Short break!");
    }

    lcd.setCursor(0, 1);
    seconds = 0;
    minutes = 0;

    while(minutes<break_duration){
      seconds = 0;
      while(seconds<60){
        lcd.setCursor(0, 1);
        if(minutes<10){
          lcd.print("0");
        }
        lcd.print(minutes);
        lcd.print(":");
        if(seconds<10){
          lcd.print("0");
        }
        lcd.print(seconds);
        delay(1000);
        seconds++;
      }
      minutes++;
    }
    count++;  // increment the counter for the number of study sessions
  }
}
