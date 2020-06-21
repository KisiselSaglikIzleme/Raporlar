

actionbar_app.xml
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

<?xml version="1.0" encoding="utf-8"?>
<androidx.appcompat.widget.Toolbar xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:background="@color/colorAccent"
    android:theme="@style/ThemeOverlay.AppCompat.Dark.ActionBar"
    android:id="@+id/pnlActionBar"

    />

//PROGRAMIZDAKÝ ACTÝONBAR XML DOSYASIDIR.
//ÇALIÞTIRMA ESNASINDA YAN PANELDE BULUNAN SAYFAMIZDIR.
********************************************************************************************************************************************************************************************************************************


activity_ana.xml
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
<?xml version="1.0" encoding="utf-8"?>
<androidx.drawerlayout.widget.DrawerLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/drawerLayout"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".Ana"
    tools:openDrawer="start"
    >
<androidx.constraintlayout.widget.ConstraintLayout
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    <LinearLayout
        android:id="@+id/layoutToolBar"
        android:layout_width="match_parent"
        android:layout_height="?actionBarSize"
        android:orientation="horizontal"

        android:background="@color/colorAccent"
        android:gravity="center_vertical"
        android:paddingStart="15dp"
        android:paddingEnd="15dp"
        app:layout_constraintTop_toTopOf="parent"
        >
        <ImageView
            android:id="@+id/imageMenu"
            android:layout_width="30dp"
            android:layout_height="30dp"
            android:contentDescription="@string/app_name"
            android:src="@drawable/ic_menu"
            android:tint="@android:color/holo_purple"

            ></ImageView>
        <TextView
            android:id="@+id/textTitle"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="@string/app_name"
            android:layout_marginStart="15dp"
            android:textColor="@android:color/holo_purple"
            android:textSize="18sp"
            android:textStyle="bold"


            ></TextView>



    </LinearLayout>
    <fragment
        android:layout_width="match_parent"
        android:layout_height="0dp"
        app:layout_constraintTop_toTopOf="@+id/layoutToolBar"
        app:layout_constraintBottom_toBottomOf="parent"
        android:id="@+id/navHostFragment"
        android:name="androidx.navigation.fragment.NavHostFragment"
        app:defaultNavHost="true"
        app:navGraph="@navigation/main"

        tools:ignore="MissingConstraints"></fragment>



</androidx.constraintlayout.widget.ConstraintLayout>

    <com.google.android.material.navigation.NavigationView
        android:layout_width="wrap_content"
        android:layout_height="match_parent"
        android:id="@+id/navigationView"
        app:menu="@menu/nav_menu"
        android:layout_gravity="start"
        app:headerLayout="@layout/layout_navigation_heder"

        ></com.google.android.material.navigation.NavigationView>



</androidx.drawerlayout.widget.DrawerLayout>

//GÝRÝÞ YAPTIKTAN SONRA KARÞIMIZA ÇIKACAK OLAN SAYFALARI GÖSTERMEKTEDÝR

**********************************************************************************************************************************************************************************************************************************************

activity_login.xml
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".LoginActivity">
<include layout="@layout/actionbar_app"
    android:id="@+id/actionbarlogin"></include>
    <TextView
        android:id="@+id/txtinfo3"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/login_with_your_account"
        android:layout_below="@id/actionbarlogin"
        android:layout_marginTop="20dp"
        android:textSize="20sp"
        android:textColor="@android:color/black"
        android:layout_marginStart="20dp"


        ></TextView>
    <TextView
        android:id="@+id/txtinfo4"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/e_mail"
        android:layout_below="@id/txtinfo3"
        android:layout_marginStart="20dp"
        android:layout_marginTop="20dp"

        ></TextView>

    <EditText
        android:id="@+id/txtEmailLogin"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_below="@id/txtinfo4"
        android:hint="@string/e_mail"
        android:layout_marginStart="10dp"
        android:layout_marginEnd="10dp"
        android:inputType="textEmailAddress"
        android:importantForAutofill="no"></EditText>

    <EditText
        android:id="@+id/txtPasswordLogin"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_below="@id/txtEmailLogin"
        android:hint="@string/password"
        android:layout_marginStart="10dp"
        android:layout_marginTop="10dp"
        android:layout_marginEnd="10dp"
        android:inputType="textPassword"
        android:importantForAutofill="no"></EditText>



    <Button
        android:id="@+id/btnLogin"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="@string/login_with_your_account"
        android:layout_alignParentBottom="true"
        android:layout_marginStart="10dp"
        android:layout_marginEnd="10dp"
        android:layout_marginBottom="35dp"
        android:background="@color/colorAccent"
        android:textColor="@android:color/black"

        ></Button>


</RelativeLayout>

//KULLANICI GÝRÝÞ EKRANIDIR.
//KULLANICILARIN E-MAÝL VE ÞÝFRE BÝLGÝLERÝNÝ GÝRÝLMESÝ EKRANIDIR.
//KULLANICILARIN GÝRÝÞ XML. DOSYASIDIR.
********************************************************************************************************************************************************************************************************************************************


activity_main.xml
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity"
    android:background="@color/colorAccent"
    android:padding="20dp"
    >
    <ImageView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:src="@drawable/icon8_healt"
        android:layout_centerHorizontal="true"
        android:layout_below="@id/txtWelcomeAppName"
        android:layout_marginTop="20dp"


        android:contentDescription="@string/todo"></ImageView>

    <TextView
        android:id="@+id/txtWelcomeAppName"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/healtyfriendly"
        android:textSize="35sp"
        android:textColor="@android:color/black"
        android:layout_centerHorizontal="true"
        android:layout_marginTop="35dp"

        ></TextView>

    <Button
        android:id="@+id/btnWelcomeRegister"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:background="@android:color/white"
        android:text="@string/new_create_account"
       android:layout_alignParentBottom="true"
        android:layout_marginBottom="50dp"
        />
    <Button
        android:id="@+id/btnWelcomeLogin"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="@string/i_have_account"
        android:background="@android:color/holo_red_dark"
        android:layout_above="@id/btnWelcomeRegister"
        android:layout_marginBottom="20dp"

        ></Button>


</RelativeLayout>

// UYGULAMAYI ÝLK ÝNDÝRMEDEN SONRA KULLANICILARI KARÞILAYAN SAYFAMIZDIR.
//BU SAYFADA ÝKÝ SEÇENEK SUNULMAKTADIR.
//KAYITLI KULLANICI VE ÝLK GÝRÝÞ YAPAN KULLANICI OLMAK ÜZERE.
// SEÇENEK SEÇÝLDÝÐÝ ZAMAN GÝRÝÞ YAPILABÝLMEKTEDÝR

*******************************************************************************************************************************************************************************************************************************************


activity_register.xml
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------
satýr xml gi
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".RegisterActivity">

    <include layout="@layout/actionbar_app"
        android:id="@+id/actionbarregister"
        ></include>

    <TextView
        android:id="@+id/txtinfo1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/new_create_account"
        android:layout_below="@id/actionbarregister"
        android:layout_marginTop="20dp"
        android:textSize="20sp"
        android:textColor="@android:color/black"
        android:layout_marginStart="20dp"


        ></TextView>
    <TextView
        android:id="@+id/txtinfo2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/username"
        android:layout_below="@id/txtinfo1"
        android:layout_marginStart="20dp"
        android:layout_marginTop="20dp"

        ></TextView>

    <EditText
        android:id="@+id/txtUsername"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_below="@id/txtinfo2"
        android:hint="@string/username"
        android:layout_marginStart="10dp"
        android:layout_marginEnd="10dp"

        android:inputType="text"
        android:importantForAutofill="no"></EditText>

    <EditText
        android:id="@+id/txtEmail"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_below="@id/txtUsername"
        android:hint="@string/e_mail"
        android:layout_marginStart="10dp"
        android:layout_marginTop="10dp"
        android:layout_marginEnd="10dp"
        android:inputType="textEmailAddress"
        android:importantForAutofill="no"></EditText>

    <EditText
        android:id="@+id/txtPassword"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_below="@id/txtEmail"
        android:hint="@string/password"
        android:layout_marginStart="10dp"
        android:layout_marginTop="10dp"
        android:layout_marginEnd="10dp"
        android:inputType="textPassword"
        android:importantForAutofill="no"></EditText>

    <Button
        android:id="@+id/btnRegister"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="@string/new_create_account"
        android:layout_alignParentBottom="true"
        android:layout_marginStart="10dp"
        android:layout_marginEnd="10dp"
        android:layout_marginBottom="35dp"
        android:background="@color/colorAccent"
        android:textColor="@android:color/black"

        ></Button>




</RelativeLayout>

//KAYIT OLMA SAYFASININ XML KODU.
***********************************************************************************************************************************************************************************************************************************************


custom_satirbki.xml
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <TextView
        android:id="@+id/textViewBki"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="@string/k_tle_endeksiniz" />
</LinearLayout>

//VERÝ TABANINDAN ÇEKÝLDÝKTEN SONRA KAYDEDÝLEN KÝTLE ÝNDEKSÝNÝN GÖRÜNTÜLENMESÝNÝ SAGLIYOR.
*****************************************************************************************************************************************************************************************************************************************
custom_satirgida.xml
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <TextView
        android:id="@+id/textViewÝsim"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="@string/name_food" />

    <TextView
        android:id="@+id/textViewKalori"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="@string/calori" />
</LinearLayout>

//VERÝ TABANINDAKÝ EKLEDÝÐÝMÝZ GIDALARI ÇEKERKEN LÝSTELÝ YAZILMASINI SAGLAR.
//GIDA SATIRI XML DOSYASIDIR.
*******************************************************************************************************************************************************************************************************************************************

fragment_adimsayar.xml
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".AdimsayarFragment">


    <!-- TODO: Update blank fragment layout -->
    <TextView
        android:id="@+id/tv_info"
        android:layout_marginTop="120dp"
        android:layout_marginStart="100dp"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/step_calculate" />


    <TextView
        android:id="@+id/tv_steps"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="150dp"
        android:layout_marginStart="100dp"
        android:text="@string/zero"
        android:textSize="40sp"


        />

    <ImageView
        android:layout_width="72dp"
        android:layout_height="wrap_content"
        android:layout_marginStart="100dp"
        android:layout_marginTop="80dp"
        android:src="@drawable/adim_"
        android:contentDescription="@string/todo" />

</FrameLayout>

//KULLANICILARIMIZIN HAREKET HALÝNDE OLDUKLARI ZAMAN ATMIÞ OLDUKLARI ADIM MÝKTARININ SAYISINI GÖSTEREN SAYFAMIZDIR
//ADIMSAYAR SAYSAINDA XML DOSYASIDIR.
*******************************************************************************************************************************************************************************************************************************************


fragment_anasayfa.xml
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".AnasayfaFragment"
    android:orientation="vertical">

    <TextView
        android:id="@+id/kisiselbilgi"
        android:layout_marginTop="60dp"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/ki_isel_bilgileriniz"/>

    <ListView
        android:id="@+id/listviewbki"
        android:layout_width="wrap_content"
        android:layout_height="200dp"
        android:layout_below="@+id/kisiselbilgi"
        />


    <TextView
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:layout_marginTop="300dp"
        android:id="@+id/anasayfasteps"
        />
    <ImageView
        android:layout_width="72dp"
        android:layout_height="wrap_content"
        android:layout_marginTop="400dp"
        android:src="@drawable/adim_"
        android:contentDescription="@string/todo" />


</RelativeLayout>

//BU FRAGMENT SAYFAMIZ ARTIK BÝZÝM UYGULAMAYA GÝRÝÞ YAPTIÐIMIZDA KULLANICIMIZI KARÞILAYAN SAYFAMIZDIR.
//BURADA KULLANICIMIZIN VERÝTABININA KAYDETTÝÐÝ VERÝLERÝ KÝÞÝSEL BÝLGÝLER GÖSTERÝLMEKTEDÝR.
//BU SAYFA BÝZÝM ANASAYFA XML DOSYAMIZDIR.
********************************************************************************************************************************************************************************************************************************************



fragment_aramagida.xml
-------------------------------------------------------------------------------------------------------------------

<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".Aramagida">

    <!-- TODO: Update blank fragment layout -->


    <TextView
        android:id="@+id/textViewgidaa"
        android:layout_width="wrap_content"
        android:layout_height="20dp"
        android:layout_marginTop="60dp"
        android:text="@string/bilgi" />

    <ListView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_marginTop="110dp"
        android:id="@+id/listviewgida"

        />

</RelativeLayout>

//KULLANICI BU SAYFAYA GELEBÝLMESÝ ÝÇÝN MENU PANEL DEN "GIDA ARAMA" SAYFASINA TIKLAMASI GEREKÝR.
//BURADA KULLANICININ DAHA ÖNCEDEN KAYDETTÝÐÝ GIDALAR GÖRÜNTÜLENMEKTEDÝR.
//BU GIDALAR KULLANICININ DAHA ÖNCEDEN VERÝTABANINA KAYDETTÝÐÝ VERÝLERÝ VERÝ TABANINDAN ÇEKEREK LÝSTVÝER
ARACILIÐI ÝLE GÖRÜNTÜLENMESÝNÝ SAÐLAMAKTADIR.
//ARAMA GIDA SAYFASININ XML DOSYASIDIR.
*****************************************************************************************************************************************************************************************************************************************



fragment_gunluk.xml
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".GunlukFragment">

    <!-- TODO: Update blank fragment layout -->
    <TextView
        android:layout_marginTop="60dp"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/ki_isel_belirledi_iniz_hedef_burada_g_r_n_r" />

    <ListView
        android:id="@+id/listView"
        android:layout_width="match_parent"
        android:layout_height="414dp"
        android:layout_marginTop="100dp"
        android:cacheColorHint="#FFFFFF" />

</FrameLayout>

// KULLANICI PANAL KISMINDAKI GÜNLÜK SEKMESÝNDEN BU SAYFAYA ERÝÞMEKTEDÝR.
// KULLANICININ GÜN ÝÇERÝSÝNDE TÜKETMÝÞ OLDUGU GIDALARI VE SU MÝKTARINI GÖSTERMEKTEDÝR.
//GÜNLÜK XML DOSYASISIR.

***********************************************************************************************************************************************************************************************************************************


fragment_hatirlatmalar.xml
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".HatirlatmalarFragment">

    <!-- TODO: Update blank fragment layout -->
    <Button
        android:id="@+id/butonbildirdis"
        android:layout_width="100dp"
        android:layout_height="50dp"
        android:background="@color/colorAccent"
        android:hint="@string/tith_noti"
        android:layout_marginTop="50dp"
        />
    <Button
        android:id="@+id/butonbildiruyku"
        android:layout_width="100dp"
        android:layout_height="50dp"
        android:background="@color/colorAccent"
        android:hint="@string/sleep_notification"
        android:layout_marginTop="50dp"
        android:layout_marginStart="110dp"
        />
    <Button
        android:id="@+id/butonbildirsu"
        android:layout_width="100dp"
        android:layout_height="50dp"
        android:background="@color/colorAccent"
        android:hint="@string/notification_water"
        android:layout_marginTop="50dp"
        android:layout_marginStart="220dp"
        />

    <TextView
        android:id="@+id/sleeps"
        android:layout_width="296dp"
        android:layout_height="wrap_content"
        android:layout_marginTop="150dp"
        android:text="@string/metin" />

    <ImageView
        android:id="@+id/imgsleep"
        android:layout_width="50dp"
        android:layout_height="50dp"
        android:layout_marginTop="150dp"
        android:layout_marginStart="290dp"
        android:src="@drawable/uyku"
        android:contentDescription="@string/save" />
    <TextView
        android:id="@+id/tith"
        android:layout_width="296dp"
        android:layout_height="wrap_content"
        android:text="@string/dis"
        android:layout_marginTop="250dp"

        />
    <ImageView
        android:id="@+id/imgtith"
        android:layout_width="50dp"
        android:layout_height="50dp"
        android:src="@drawable/tith"
        android:layout_marginStart="290dp"
        android:layout_marginTop="250dp"
         />
  <TextView
      android:id="@+id/water"
      android:layout_width="290dp"
      android:layout_height="wrap_content"
      android:text="@string/text_wtr"
      android:layout_marginTop="350dp"
      />
    <ImageView
        android:id="@+id/imgwater"
        android:layout_width="50dp"
        android:layout_height="50dp"
        android:src="@drawable/wat"
        android:layout_marginTop="350dp"
        android:layout_marginStart="290dp"
        />



</FrameLayout>

//GÜNLÜK XML DOSYASIDIR.
//KULLANICININ GÜNLÜK OLARAK DÝÞLERÝNÝ FIRÇALAMASINI HATIRLATIR
//KULLACILARIN GÜNLÜK UYKU DÜZENÝNÝ HATIRLATIR
//KULLANICILARIN GÜNLÜK VUCUDUNA ALMASI GEREKEN SU MÝKTARINI HATIRLATIR.
//BU SAYFA HATIRLATMALAR XML DOSYASIDIR.

**************************************************************************************************************************************************************************************************************************************

fragment_hedef.xml
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".HedefFragment">


    <EditText
        android:id="@+id/gýdaadi"
        android:layout_width="100dp"
        android:layout_height="50dp"
        android:ems="10"
        android:inputType="textPersonName"
        android:layout_marginTop="50dp"

        android:hint="@string/name_food"
        android:autofillHints="" />

    <EditText
        android:id="@+id/kalori"
        android:layout_width="100dp"
        android:layout_height="50dp"
        android:layout_marginTop="50dp"
        android:layout_marginStart="150dp"
        android:hint="@string/calori"
        android:autofillHints=""
        android:inputType="text" />
    <Button
        android:id="@+id/gýdakaydet"
        android:layout_width="100dp"
        android:layout_height="50dp"
        android:hint="@string/save"
        android:layout_marginTop="120dp"

        />

</RelativeLayout>

//HEDEF XML DOSYASIDIR
//KULLANICILARIN VUCÜDLARINA ALMIÞ OLDUKLARI GIDALARIN ADLARINI VE KALORÝ MÝKTARLARINI UYGULAMAMIZA KAYDETTÝÐÝ SAFYADIR.


*******************************************************************************************************************************************************************************************************************

fragment_hedefekle.xml
--------------------------------------------------------------------------------------------------------------------------------------------------------------------

<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".Hedefekle">

  <TextView
    android:id="@+id/hedefkalori"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_marginTop="50dp"
    android:text="@string/kalori_al_m_limitinizi_belirtiniz"/>
  <EditText
        android:id="@+id/gunlukkalori"
        android:layout_width="90dp"
        android:layout_height="50dp"
        android:layout_marginTop="70dp"
        android:autofillHints=""
        android:hint="@string/calori"
        android:inputType="text" />
    <TextView
        android:id="@+id/hedefsu"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="130dp"
        android:text="@string/hedef_su_me_litre"/>
    <EditText
        android:id="@+id/textsu"
        android:layout_width="90dp"
        android:layout_height="50dp"
        android:layout_marginTop="150dp"
        android:autofillHints=""
        android:hint="@string/water"
        android:inputType="text" />
    <TextView
        android:id="@+id/hedefadim"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="210dp"
        android:text="@string/hedef_ad_m_say_s"/>
    <EditText
        android:id="@+id/textadim"
        android:layout_width="90dp"
        android:layout_height="50dp"
        android:layout_marginTop="250dp"
        android:autofillHints=""
        android:hint="@string/step_counter"
        android:inputType="text" />


    <Button
        android:id="@+id/hedefkaydet"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:hint="@string/save"
        android:layout_marginTop="310dp"
        />



</RelativeLayout>

//HEDEF XML DOSYASIDIR
//KULLANICILARIN KENDÝLERÝNE KOYMUÞ OLDUKLARI HEDEF KALORÝ MÝKTARINI GÖSSTERMEKTEDÝR.
//KULLANICILARIN GÜNLÜK HEDEF SU MÝKTARI GÖRÜNTÜLENMEKTEDÝR.
//KULLANICILARIN GÜNLÜK HEDEF ADIMMÝKTARINI GÖSTERMEKTEDÝR.
// HEDEF KAYDETME EKRANI BULUNMAKTADIR.
******************************************************************************************************************************************************************************************************************************************

fragment_nabiz.xml
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".NabizFragment">

    <!-- TODO: Update blank fragment layout -->

    <TextView
        android:layout_width="match_parent"
        android:layout_height="100dp"
        android:layout_marginTop="70dp"
        android:id="@+id/text"
        />


</FrameLayout>

//NABIZ XML DOSYASIDIR.
//KULLANICILARIMIZIN SENSÖR YARDIMI ÝLE ANLIK NABIZINI ÖLÇER
// ARDUÝNO KODLARI SAYESÝNDE ÖLÇÜM YAPMAKTADIR SENSÖRÜMÜZ
//BLUETOOTH ARACILIGI ÝLE ANDROÝD TELEFONUMUZA BAGLANILMAKTADIR.
*******************************************************************************************************************************************************************************************************************************************

fragment_saglikhesapla.xml 

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------



<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".SaglikhesaplaFragment">

    <!-- TODO: Update blank fragment layout -->
    <TextView
        android:id="@+id/txtboy"
        android:layout_marginTop="70dp"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/height"
        android:textStyle="bold"
        android:textSize="18sp"
        />

    <EditText
        android:id="@+id/boy"
        android:layout_width="100dp"
        android:layout_height="wrap_content"
        android:hint="@string/height"
        android:layout_marginTop="70dp"
        android:layout_marginStart="100dp"
        android:importantForAutofill="no"
        android:inputType=""></EditText>
    <TextView
        android:id="@+id/widget34"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
       android:text="@string/weight"
        android:layout_marginTop="140dp"
        android:textStyle="bold"
        android:textSize="18sp"

        ></TextView>
    <EditText
        android:id="@+id/kilo"
        android:layout_width="100dp"
        android:layout_height="wrap_content"
        android:hint="@string/weight"
        android:importantForAutofill="no"
        android:layout_marginStart="100dp"
        android:layout_marginTop="140dp"
        android:inputType=""
        ></EditText>
    <TextView
        android:id="@+id/widget36"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/years"
        android:layout_marginTop="220dp"
        android:textStyle="bold"
        android:textSize="18sp"
        ></TextView>
    <EditText
        android:id="@+id/yas"
        android:layout_width="100dp"
        android:layout_height="wrap_content"
        android:hint="@string/years"
        android:layout_marginTop="220dp"
        android:layout_marginStart="100dp"
        android:inputType=""
        android:importantForAutofill="no"
        ></EditText>
    <Button
        android:id="@+id/sonuc"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:background="@color/colorAccent"
        android:text="@string/calculate_healtly"
        android:layout_marginTop="265dp"
        ></Button>

    <TextView
        android:id="@+id/textVier1"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:textSize="20sp"
        android:textStyle="bold"
        android:layout_marginTop="310dp"
        android:textColor="@android:color/black"
        android:inputType=""
        android:hint=""
        android:autofillHints=""
        ></TextView>
        <TextView
            android:id="@+id/textVier2"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:textSize="20sp"
            android:textStyle="bold"
            android:layout_marginTop="370dp"
            android:textColor="@android:color/black"
            android:inputType=""
            android:importantForAutofill=""></TextView>


</FrameLayout>

//SAGLIK HESAPALAMA XML.DOSYASIDIR.
//KULLANICILARDAN BOY,KÝLO,YAÞ BÝLGÝLERÝ ÝSTENMEKTEDÝR.
//KULLANICILARIN BOY VE KÝLO ORANINA GÖRE KULLANICILARAIN SAGLIK HESAPLAMALARI YAPILMAKTADIR
//HESABI YAPILAN VUCÜD KÝTLE ÝNDEKSÝNE GÖRE KULLANICININ DURUMUNU GÖSTERMEKTEDÝR.


*************************************************************************************************************************************************************************************************************************************


layout_navigation_heder.xml
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    xmlns:app="http://schemas.android.com/apk/res-auto">

    <com.makeramen.roundedimageview.RoundedImageView
        android:layout_width="70dp"
        android:layout_height="70dp"
        android:id="@+id/imageProfile"
        android:scaleType="centerCrop"
        android:src="@drawable/person"
        tools:ignore="MissingConstraints"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:riv_oval="true"

        />
    <View
        android:id="@+id/viewSupported"
        android:layout_width="1dp"
        android:layout_height="1dp"
        tools:ignore="MissingConstraints"
        app:layout_constraintBottom_toBottomOf="@+id/imageProfile"
        app:layout_constraintEnd_toEndOf="@+id/imageProfile"
        app:layout_constraintStart_toStartOf="@+id/imageProfile"
        app:layout_constraintTop_toTopOf="@+id/imageProfile"
        />

    <TextView
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginStart="10dp"
        android:text="@string/username"
        tools:ignore="MissingConstraints" />


</androidx.constraintlayout.widget.ConstraintLayout>

//PANEL XML DOSYASIDIR.
// GÝRÝÞ SAYFA KISMININ YAN TARAFINDA AÇILAN PANEL SEKMESÝ SAYFASIDIR.
//BU PANEL SAYFASINDA UYGULAMAMIZDAKÝ TÜM SAYFALARA GÝRÝÞ YAPILABÝLMEKTEDÝR.



*******************************************************************************************************************************************************************************************************************************************













