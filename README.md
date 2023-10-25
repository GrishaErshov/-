package com.example.fxjy;

import androidx.appcompat.app.AppCompatActivity;

import android.content.AsyncQueryHandler;
import android.content.Context;
import android.hardware.Sensor;
import android.hardware.SensorEvent;
import android.hardware.SensorEventListener;
import android.hardware.SensorManager;
import android.os.Bundle;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity {

    //поля
    private Sensor sensorAccelerometer;
    private SensorManager sensorManager;
    private TextView outputAccelerometr;

    //создание
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        outputAccelerometr = findViewById(R.id.output_accelerometer);

        sensorManager=(SensorManager) getSystemService(Context.SENSOR_SERVICE);
        sensorAccelerometer=sensorManager.getDefaultSensor(Sensor.TYPE_ACCELEROMETER);

        //слушатель сенсоров
        private SensorEventListener sensorEventListener = new SensorEventListener() {
            //метод показаний сенсора
            @Override
            public void onSensorChanged(SensorEvent sensorEvent) {
                float accelerometerX = event.values[0];
                float accelerometerY = event.values[1];
                float accelerometerZ = event.values[2];

                outputAccelerometr.setText("Данные акселерометра:\n"
                + accelerometerX + "\n" + accelerometerY + "\n" + accelerometerZ);
            }

            //метод чувствительности сенсора
            @Override
            public void onAccuracyChanged(Sensor sensor, int i) {
            }
        };

        //доступность активности пользователю
        @Override
        public void onResume(){
            super.onResume();
            sensorManager.registerListener(sensorEventListener,sensorAccelerometer,sensorManager.SENSOR_DELAY_UI);
        }

        //активность становится недоступна пользователю
        @Override
        protected void onPause() {
            super.onPause();
            sensorManager.unregisterListener(sensorEventListener);
        }

    }

}




<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/header"
        android:text="Данные акселерометра"
        android:layout_marginTop="14dp"
        android:textSize="25dp"
        android:gravity="center"
        android:textColor="#057288"
        android:layout_width="350dp"
        android:layout_height="70dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <TextView
        android:id="@+id/output_accelerometer"
        android:layout_width="350dp"
        android:layout_height="140dp"
        android:gravity="top"
        android:hint="Данные акселерометра"
        android:textSize="19sp"
        android:textColor="#057288"
        android:textColorHint="#057288"
        android:background="#CCDDE0"
        android:padding="14dp"
        android:layout_marginTop="14dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
