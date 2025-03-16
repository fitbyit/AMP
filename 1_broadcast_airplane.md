# Android App to Change Image Based on Airplane Mode Broadcast Receiver

### Step 1: Create a New Android Project

### Step 2: Add Permissions in `AndroidManifest.xml`
Ensure that the required permissions are declared in `AndroidManifest.xml`.
```xml
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

### Step 3: Set Up Layout (`activity_main.xml`)

Add Images to `res/drawable`
You need two images for this app:
1. `airplane_on.png` – Image for when airplane mode is ON.
2. `airplane_off.png` – Image for when airplane mode is OFF.

Open `res/layout/activity_main.xml` and define an `ImageView` that will show different images based on the airplane mode state.

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="96dp"
        android:text="Airplane Mode"
        android:textAlignment="gravity"
        android:textSize="24sp"
        android:textStyle="bold"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <ImageView
        android:id="@+id/imageView"
        android:layout_width="268dp"
        android:layout_height="328dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.496"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/textView"
        app:layout_constraintVertical_bias="0.214"
        app:srcCompat="@drawable/airplane_off" />

</androidx.constraintlayout.widget.ConstraintLayout>
```
### Step 4: Create the `BroadcastReceiver` in `MainActivity.java`

In `MainActivity.java`, create the `BroadcastReceiver` to listen for airplane mode changes and update the image accordingly.

Declare variable inside in Main Class
```java
private BroadcastReceiver airplaneModeReceiver;
private ImageView imageView;
```

Add Code inside onCreate
```java
imageView = findViewById(R.id.imageView);
        // Initialize the BroadcastReceiver
        airplaneModeReceiver = new BroadcastReceiver() {
            @Override
            public void onReceive(Context context, Intent intent) {
                boolean isAirplaneModeOn = intent.getBooleanExtra("state", false);
                if (isAirplaneModeOn) {
                    // Show Toast when Airplane mode is ON
                    imageView.setImageResource(R.drawable.airplane_on);
                    Toast.makeText(context, "Airplane Mode ON", Toast.LENGTH_SHORT).show();
                } else {
                    // Show Toast when Airplane mode is OFF
                    imageView.setImageResource(R.drawable.airplane_off);
                    Toast.makeText(context, "Airplane Mode OFF", Toast.LENGTH_SHORT).show();
                }
            }
        };

        IntentFilter filter = new IntentFilter(Intent.ACTION_AIRPLANE_MODE_CHANGED);
        registerReceiver(airplaneModeReceiver, filter);
```

Create a onDestroy Override Method 
```java
 @Override
    protected void onDestroy() {
        super.onDestroy();
        // Unregister the receiver when the activity is destroyed
        if (airplaneModeReceiver != null) {
            unregisterReceiver(airplaneModeReceiver);
        }
    }
```

## Done !!! 

Output:

<img src="https://github.com/user-attachments/assets/5e13d063-e79e-4eb3-bb94-c638b5aa3044" height="380px">

<img src="https://github.com/user-attachments/assets/3cf9410e-af3e-4df9-8422-8d7186fe4712" height="380px">





