# Código java

```java
public class OnboardingWithCenterAnimationActivity extends AppCompatActivity {
public static final int STARTUP_DELAY = 300;
public static final int ANIM_ITEM_DURATION = 1000;
public static final int ITEM_DELAY = 300;

private boolean animationStarted = false;

@Override
protected void onCreate(@Nullable Bundle savedInstanceState) {
    setTheme(R.style.AppTheme);
    getWindow().getDecorView().setSystemUiVisibility(
            View.SYSTEM_UI_FLAG_LAYOUT_FULLSCREEN | View.SYSTEM_UI_FLAG_LAYOUT_HIDE_NAVIGATION);
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_onboarding_center);
}

@Override
public void onWindowFocusChanged(boolean hasFocus) {

    if (!hasFocus || animationStarted) {
        return;
    }

    animate();

    super.onWindowFocusChanged(hasFocus);
}

private void animate() {
    ImageView logoImageView = (ImageView) findViewById(R.id.img_logo);
    ViewGroup container = (ViewGroup) findViewById(R.id.container);

    ViewCompat.animate(logoImageView)
        .translationY(-250)
        .setStartDelay(STARTUP_DELAY)
        .setDuration(ANIM_ITEM_DURATION).setInterpolator(
            new DecelerateInterpolator(1.2f)).start();

    for (int i = 0; i < container.getChildCount(); i++) {
        View v = container.getChildAt(i);
        ViewPropertyAnimatorCompat viewAnimator;

        if (!(v instanceof Button)) {
            viewAnimator = ViewCompat.animate(v)
                    .translationY(50).alpha(1)
                    .setStartDelay((ITEM_DELAY * i) + 500)
                    .setDuration(1000);
        } else {
            viewAnimator = ViewCompat.animate(v)
                    .scaleY(1).scaleX(1)
                    .setStartDelay((ITEM_DELAY * i) + 500)
                    .setDuration(500);
        }

        viewAnimator.setInterpolator(new DecelerateInterpolator()).start();
    }
}
}
```

# Layout xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<FrameLayout
xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:tools="http://schemas.android.com/tools"
android:layout_width="match_parent"
android:layout_height="match_parent"
android:background="?colorPrimary"
android:orientation="vertical"
>

<LinearLayout
    android:id="@+id/container"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_gravity="center"
    android:gravity="center"
    android:orientation="vertical"
    android:paddingTop="144dp"
    tools:ignore="HardcodedText"
    >

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center_horizontal"
        android:layout_marginTop="16dp"
        android:alpha="0"
        android:text="Hello world"         android:textAppearance="@style/TextAppearance.AppCompat.Widget.ActionBar.Title.Inverse"
        android:textColor="@android:color/white"
        android:textSize="22sp"
        tools:alpha="1"
        />

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center_horizontal"
        android:layout_marginTop="8dp"
        android:alpha="0"
        android:gravity="center"
        android:text="This a nice text"
      android:textAppearance="@style/TextAppearance.AppCompat.Widget.ActionBar.Subtitle.Inverse"
        android:textSize="20sp"
        tools:alpha="1"
        />

    <Button
        android:id="@+id/btn_choice1"
        android:layout_width="200dp"
        android:layout_height="wrap_content"
        android:layout_marginTop="48dp"
        android:scaleX="0"
        android:scaleY="0"
        android:text="A nice choice"
        android:theme="@style/Button"
        />

    <Button
        android:id="@+id/btn_choice2"
        android:layout_width="200dp"
        android:layout_height="wrap_content"
        android:layout_marginTop="4dp"
        android:scaleX="0"
        android:scaleY="0"
        android:text="Far better!"
        android:theme="@style/Button"
        />

</LinearLayout>

<ImageView
    android:id="@+id/img_logo"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_gravity="center"
    android:src="@drawable/img_face"
    tools:visibility="gone"
    />
</FrameLayout>
```

# img face
```xml
<?xml version="1.0" encoding="utf-8"?>
<layer-list xmlns:android="http://schemas.android.com/apk/res/android"
        android:opacity="opaque">

<item android:drawable="?colorPrimary"/>
<item>
    <bitmap
        android:gravity="center"
        android:src="@drawable/img_face"/>
</item>
```

# Add this theme to your splashscreen in the manifest
```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
<style name="AppTheme" parent="Theme.AppCompat.Light.NoActionBar">
    <!-- Customize your theme here. -->
    <item name="colorPrimary">@color/colorPrimary</item>
    <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
    <item name="colorAccent">@color/colorAccent</item>
    <item name="android:windowBackground">@null</item>
</style>

<style name="AppTheme.CenterAnimation">
    <item name="android:windowBackground">@drawable/ll_face_logo</item>
</style>
```
