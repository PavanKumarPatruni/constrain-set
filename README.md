# constrain-set
About ConstrainSets in Constraint Layout

There are 2 ways add a view to constraint layout
  1. Using XML
  2. Dynamically from logic
  
<img style="width: 200px;" src="https://github.com/PavanKumarPatruni/constrain-set/blob/master/image.png?raw=true"/>
  
<h3>1. Using XML</h3>

    <android.support.constraint.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
      xmlns:app="http://schemas.android.com/apk/res-auto"
      xmlns:tools="http://schemas.android.com/tools"
      android:layout_width="match_parent"
      android:layout_height="match_parent"
      tools:context=".MainActivity">

        <EditText
            android:id="@+id/editText"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_marginStart="8dp"
            android:layout_marginLeft="8dp"
            android:layout_marginTop="8dp"
            android:layout_marginEnd="8dp"
            android:layout_marginRight="8dp"
            android:background="@drawable/edit_text_rounded_rectangle"
            android:drawableEnd="@drawable/ic_search_black_24dp"
            android:drawableRight="@drawable/ic_search_black_24dp"
            android:hint="@string/search"
            android:padding="15dp"
            android:textColorHint="@color/colorGrey"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toTopOf="parent" />

    </android.support.constraint.ConstraintLayout>
    
<h3>Dynamically From Login</h3>

Whenever there a layout with EditText that need to part of the main xml file. We need to add that view to the XML dynamically. In that case we need to use ConstraintSet for adding the constraints dynamically to the view while adding to main XML.

<b>activity_main.xml</b>

    <?xml version="1.0" encoding="utf-8"?>
    <android.support.constraint.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:tools="http://schemas.android.com/tools"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        tools:context=".MainActivity">

    </android.support.constraint.ConstraintLayout>
    
<b>layout_edittext.xml</b>
    
    <?xml version="1.0" encoding="utf-8"?>
    <EditText xmlns:android="http://schemas.android.com/apk/res/android"
        android:id="@+id/editText"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginStart="8dp"
        android:layout_marginLeft="8dp"
        android:layout_marginTop="8dp"
        android:layout_marginEnd="8dp"
        android:layout_marginRight="8dp"
        android:background="@drawable/edit_text_rounded_rectangle"
        android:drawableEnd="@drawable/ic_search_black_24dp"
        android:drawableRight="@drawable/ic_search_black_24dp"
        android:hint="@string/search"
        android:padding="15dp"
        android:textColorHint="@color/colorGrey" />
        
<b>Add below code to MainActivity.kt</b>
        
      val editText = LayoutInflater.from(this).inflate(R.layout.layout_edittext, constraintLayout, false)
        constraintLayout.addView(editText)

        val constraintSet = ConstraintSet()
        constraintSet.clone(constraintLayout)

        constraintSet.connect(editText.id, ConstraintSet.START, ConstraintSet.PARENT_ID, ConstraintSet.START)
        constraintSet.connect(editText.id, ConstraintSet.END, ConstraintSet.PARENT_ID, ConstraintSet.END)
        constraintSet.connect(editText.id, ConstraintSet.TOP, ConstraintSet.PARENT_ID, ConstraintSet.TOP)

        constraintSet.applyTo(constraintLayout)
