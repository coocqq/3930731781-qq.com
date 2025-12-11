<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <ImageView
        android:id="@+id/card_image"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1"
        android:scaleType="centerCrop"
        android:background="#444444" />

    <TextView
        android:id="@+id/card_text"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:padding="4dp"
        android:textColor="#FFFFFF"
        android:background="#88000000"
        android:singleLine="true"
        android:ellipsize="end" />

</LinearLayout>
