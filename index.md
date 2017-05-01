package com.entotem.myfirstapp;

import android.annotation.SuppressLint;
import android.content.Context;
import android.content.Intent;
import android.net.Uri;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;                           // Importing all the things for the app, from XML file
import android.util.AttributeSet;
import android.util.Log;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.Button;
import android.widget.EditText;
import android.widget.SeekBar;
import android.widget.Toast;

import com.entotem.myfirstapp.DisplayMessageActivity;
import com.entotem.myfirstapp.R;

public class MainActivity extends AppCompatActivity {
  public static final String TAG = "MainActivity";
  public int bckCol1, bckCol2, bckCol3;                 // Setting stuff
  int redProgressChangedValue = 0;
  int blueProgressChangedValue = 0;
  SeekBar redSeekBar;
  SeekBar blueSeekBar;
  MainActivity MyActivity;


  @Override
  protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    MyActivity = this;
    redSeekBar=(SeekBar)findViewById(R.id.seekBar);

    redSeekBar.setOnSeekBarChangeListener(new SeekBar.OnSeekBarChangeListener() {

      public void onProgressChanged(SeekBar seekBar, int progress, boolean fromUser) {        // Coding a bit of the seekbars
        redProgressChangedValue = progress;                                                 
      }

      public void onStartTrackingTouch(SeekBar seekBar) {

      }

      public void onStopTrackingTouch(SeekBar bar) {
         Toast.makeText(MainActivity.this, "Red:" + redProgressChangedValue,
             Toast.LENGTH_SHORT).show();
      }
    });

    MyActivity = this;
    blueSeekBar=(SeekBar)findViewById(R.id.seekBar2);
    blueSeekBar.setOnSeekBarChangeListener(new SeekBar.OnSeekBarChangeListener() {    // Telling seekbar what to do

      public void onProgressChanged(SeekBar seekBar, int progress, boolean fromUser) {
        blueProgressChangedValue = progress;

      }

      public void onStartTrackingTouch(SeekBar seekBar) {
        // TODO Auto-generated method stub
      }

      public void onStopTrackingTouch(SeekBar bar) {
        switch (bar.getId()) {
          case R.id.seekBar:
            Toast.makeText(MainActivity.this, "Red:" + redProgressChangedValue,
                Toast.LENGTH_SHORT).show();                                          // Telling the seekbars what to do
            break;

          case R.id.seekBar2:
            Toast.makeText(MainActivity.this, "Blue:" + blueProgressChangedValue,
                Toast.LENGTH_SHORT).show();
            break;
        }
      }
    });
    addListenerOnButton();
  }



  public void addListenerOnButton() {

    Button myButton = (Button) findViewById(R.id.button);
    Button myButton2 = (Button) findViewById(R.id.button2);
    Button myButton3 = (Button) findViewById(R.id.button3);   // Giving the buttons names/ids's
    Button myButton4 = (Button) findViewById(R.id.button4);

    bckCol1 = 0xffff0000;
    bckCol2 = 0xff0000ff;    // Seting variables for my colors
    bckCol3 = 0xff000000;

    final OnClickListener onClickListener = new OnClickListener() {
      @Override                                                              // Telling the buttons what to do
      public void onClick(View button) {
        switch (button.getId()) {
          case R.id.button:
            Log.v(TAG, "Button 1 press: " + redProgressChangedValue);
            View Parent = (View) button.getParent();
            bckCol1 &= 0xff000000;
            int redBackground = redProgressChangedValue << 16;
            bckCol1 |= redBackground;
            Parent.setBackgroundColor(bckCol1);
            break;
          case R.id.button2:
            Log.v(TAG, "Button 2 press: " + blueProgressChangedValue);
            Parent = (View) button.getParent();
            bckCol2 &= 0xff000000;
            int blueBackground = blueProgressChangedValue & 0xff;
            bckCol2 |= blueBackground;
            Parent.setBackgroundColor(bckCol2);
            break;
          case R.id.button3:
            Log.v(TAG, "Button 3 press: ");
            Parent = (View) button.getParent();
            Parent.setBackgroundColor(bckCol3);
            break;
          case R.id.button4:
            Log.v(TAG, "Button 4 press");
            Intent intent = new Intent(MainActivity.this, DisplayMessageActivity.class);
            startActivity(intent);



        }

      }



    };

    myButton.setOnClickListener(onClickListener);   // Seting the "listeners for when the buttons are pressed
    myButton2.setOnClickListener(onClickListener);
    myButton3.setOnClickListener(onClickListener);
    myButton4.setOnClickListener(onClickListener);
  }
}
