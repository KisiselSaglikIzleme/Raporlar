MANİFEST VE BUİLD.GRADLE DOSYALARININ DÜZENLENMESİ
---------------------------------------------------------------------------------------------------------------------------
---------------------------------------------------------------------------------------------------------------------------

BUİLD.GRADLE(:APP)

apply plugin: 'com.android.application'
apply plugin: 'com.google.gms.google-services'

android {
    compileSdkVersion 29
    buildToolsVersion "29.0.3"

    defaultConfig {
        applicationId "com.example.saglik"
        minSdkVersion 20
        targetSdkVersion 29
        versionCode 1
        versionName "1.0"

        testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"
    }

    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
        }
    }

}

dependencies {
    implementation fileTree(dir: 'libs', include: ['*.jar'])
    implementation 'com.google.firebase:firebase-analytics:17.4.2'
    implementation 'com.google.firebase:firebase-auth:19.3.1'
    implementation 'androidx.appcompat:appcompat:1.1.0'
    implementation 'androidx.constraintlayout:constraintlayout:1.1.3'
    implementation 'androidx.legacy:legacy-support-v4:1.0.0'
    implementation 'com.google.firebase:firebase-database:19.3.0'
    implementation 'com.google.firebase:firebase-messaging:20.2.0'

    testImplementation 'junit:junit:4.13'
    androidTestImplementation 'androidx.test.ext:junit:1.1.1'
    androidTestImplementation 'androidx.test.espresso:espresso-core:3.2.0'

    implementation 'com.google.android.material:material:1.2.0-alpha02'
    implementation 'androidx.navigation:navigation-fragment-ktx:2.2.0-rc03'
    implementation 'androidx.navigation:navigation-ui-ktx:2.2.0-rc03'
    implementation 'com.makeramen:roundedimageview:2.3.0'

    implementation 'pub.devrel:easypermissions:1.2.0'
    implementation 'com.firebaseui:firebase-ui-database:2.3.0'


}

//Kodlarımızın hatasız bir şekilde çalışabilmesi için app klosöründeki gradle dosyası yukarıdaki gibi olmalıdır.

---------------------------------------------------------------------------------------------------------------------------

BUİLD.GRADLE(SAGLİK)


// Top-level build file where you can add configuration options common to all sub-projects/modules.

buildscript {
    
    repositories {
        google()
        jcenter()
        
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:3.6.3'
        classpath 'com.google.gms:google-services:4.3.3'



        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}

allprojects {
    repositories {
        google()
        jcenter()
        
    }
}

task clean(type: Delete) {
    delete rootProject.buildDir
}

//SAĞLIK DOSYASI İÇİNDEKİ BUİLD.GRADLE(SAGLİK) DOSYASININ OLMASI GEREKEN HALİ
---------------------------------------------------------------------------------------------------------------------------
ANDROİDMANİFEST.XML


<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    package="com.example.saglik">

    <uses-permission android:name="android.permission.BODY_SENSORS" />
    <uses-permission android:name="android.permission.CAMERA" />
    <uses-permission android:name="com.google.android.things.permission.USE_PERIPHERAL_IO" />
    <uses-permission android:name="android.permission.FLASHLIGHT" />

    <uses-feature android:name="android.hardware.camera" />
    <uses-feature android:name="android.hardware.camera.flash" />

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/AppTheme">
        <receiver
            android:name=".BildirimYakalayıcı"
            android:enabled="true"
            android:exported="true"></receiver>

        <activity android:name=".MainActivity" />
        <activity
            android:name=".RegisterActivity"
            android:parentActivityName=".MainActivity" />
        <activity
            android:name=".LoginActivity"
            android:parentActivityName=".MainActivity" />
        <activity android:name=".Ana">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
        <service android:name=".MesajServis">
            <intent-filter>
                <action android:name="com.google.firebase.MESSAGİNG_EVENT"/>

            </intent-filter>

        </service>
    </application>

</manifest>

//UYGULAMAMIZIN ÇALIŞMASI İÇİN ANDROİDMANİFEST.XML DOSYAMIZI BU ŞEKİLDE DÜZENLEMELİYİZ.
//YUKARIDA SENSÖRLER İÇİN İZİNLER ALINMIŞTIR.
//UYGULAMANIN RAHAT KULLANILMASI İÇİN ANA KULLANIM ACTİVİTY BELİRLENMİŞTİR.

**************************************************************************************************************************
--------------------------------------------------------------------------------------------------------------------------
.JAVA UZANTILI DOSYALARIMIZ
---------------------------------------------------------------------------------------------------------------------------
MAİNACTİVİTY.JAVA

package com.example.saglik;

import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;

public class MainActivity extends AppCompatActivity {
    private Button btnWelcomeLogin, btnWelcomeRegister;
    public void init(){
        btnWelcomeLogin = (Button) findViewById(R.id.btnWelcomeLogin);
        btnWelcomeRegister= (Button) findViewById(R.id.btnWelcomeRegister);
    }
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        init();
        btnWelcomeLogin.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intentLOgin = new Intent(MainActivity.this, LoginActivity.class);
                startActivity(intentLOgin);
                finish();
            }
        });
        btnWelcomeRegister.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                 Intent intentRegister = new Intent(MainActivity.this, RegisterActivity.class);
                 startActivity(intentRegister);
                 finish();
            }
        });


    }
}
//PROGRAMI YÜKLEDİKTEN SONRA İLK AÇILDIĞINDA KARŞIMIZA ÇIKAN EKRANDIR.
//BURADA İKİ ADET BUTON BULUNMAKTA (GİRİŞYAP VE KAYIT OLUŞTURMAK)
//KULLANICI BURADA HANGİSİNİTERCİH EDERSE O SAYFAYA YÖNLENDİREN İNTENTLER VARDIR.
---------------------------------------------------------------------------------------------------------------------------
REGİSTERACTİVİTY.JAVA

package com.example.saglik;

import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import androidx.appcompat.widget.Toolbar;

import android.app.ProgressDialog;
import android.content.Intent;
import android.os.Bundle;
import android.os.Process;
import android.text.TextUtils;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

import com.google.android.gms.tasks.OnCompleteListener;
import com.google.android.gms.tasks.Task;
import com.google.firebase.auth.AuthResult;
import com.google.firebase.auth.FirebaseAuth;
import com.google.firebase.database.DatabaseReference;
import com.google.firebase.database.FirebaseDatabase;

import java.util.HashMap;

public class RegisterActivity extends AppCompatActivity {
    private Toolbar actionbarregister;
    private ProgressDialog registerDialog;
    private EditText txtUsername, txtEmail, txtPassword;
    private Button btnRegister;

    private FirebaseAuth auth;
    private DatabaseReference mDatabase;

    public void init(){
        actionbarregister = (Toolbar) findViewById(R.id.actionbarregister);
        setSupportActionBar(actionbarregister);
        getSupportActionBar().setTitle("Hesap Oluştur");
        getSupportActionBar().setDisplayHomeAsUpEnabled(true);

        auth = FirebaseAuth.getInstance();



        txtUsername = (EditText) findViewById(R.id.txtUsername);
        txtEmail = (EditText) findViewById(R.id.txtEmail);
        txtPassword = (EditText) findViewById(R.id.txtPassword);
        btnRegister = (Button)findViewById(R.id.btnRegister);
        registerDialog = new ProgressDialog(this);





    }

    private void createNewAccount() {

        String username = txtUsername.getText().toString();
        String email = txtEmail.getText().toString();
        String password = txtPassword.getText().toString();
        if (!TextUtils.isEmpty(username)||!TextUtils.isEmpty(email)||!TextUtils.isEmpty(password)){
            registerDialog.setTitle("Kaydediliyor");
            registerDialog.setMessage("hesabınız oluşturuluyor");
            registerDialog.setCanceledOnTouchOutside(false);
            registerDialog.show();
            register_user(username,password,email);


        }


    }

    private void register_user(final String username, String password, String email) {
        auth.createUserWithEmailAndPassword(email,password).addOnCompleteListener(new OnCompleteListener<AuthResult>() {
            @Override
            public void onComplete(@NonNull Task<AuthResult> task) {
                if (task.isSuccessful()){
                    String user_id = auth.getCurrentUser().getUid();
                    mDatabase= FirebaseDatabase.getInstance().getReference().child("Users").child(user_id);
                    HashMap<String,String> usermap = new HashMap<>();
                    usermap.put("name",username);

                    mDatabase.setValue(usermap).addOnCompleteListener(new OnCompleteListener<Void>() {
                        @Override
                        public void onComplete(@NonNull Task<Void> task) {
                          if (task.isSuccessful()){
                              registerDialog.dismiss();
                              Intent mainIntent = new Intent(RegisterActivity.this,LoginActivity.class);
                              startActivity(mainIntent);
                          }
                        }
                    });

                }else{
                    registerDialog.dismiss();
                    Toast.makeText(getApplicationContext(),"hata:"+task.getException().getMessage(),Toast.LENGTH_LONG).show();

                }
            }
        });
    }

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_register);
        init();
        btnRegister.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                createNewAccount();
            }
        });
    }
}

//BU SAYFA BİZİM YENİ KULLANICI KAYIT OLUŞTURMAMIZI SAĞLAYAN ACTİVİTY SAYFAMIZDIR.
//KULLANICI BU SAYFAYI GÖREBİLMESİ İÇİN MAİNACTİVİTY SAYFASINDA YENİ HESAP OLUŞTUR BUTONUNA TIKLANILMASI GEREKMEKTEDİR.
/KULLANICI BURADAN SONRA FİREBASE İLE PROGRAMI BAĞLAMIŞ OLMASI GEREKMEKTEDİR.
//FİREBASE DE E-POSTA VE ŞİFRE İE KAYIT-GİRİŞİ ETKİNLEŞTİRİLMESİ GEREKMEKTEDİR.
//KULLANICI BURADA KULLANICI ADINI, E-POSTASINI, ŞİFRESİNİ GİREREK KULLANICI OLUŞTURABİLMEKTEDİR.
---------------------------------------------------------------------------------------------------------------------------

LOGİNACTİVTY.JAVA

package com.example.saglik;

import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import androidx.appcompat.widget.Toolbar;

import android.content.Intent;
import android.os.Bundle;
import android.text.TextUtils;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

import com.google.android.gms.tasks.OnCompleteListener;
import com.google.android.gms.tasks.Task;
import com.google.firebase.auth.AuthResult;
import com.google.firebase.auth.FirebaseAuth;
import com.google.firebase.auth.FirebaseUser;

public class LoginActivity extends AppCompatActivity {
    private Toolbar actionbarlogin;
    private EditText txtEmail, txtPassword;
    private Button btnLogin;
    private FirebaseAuth auth;
    private FirebaseUser currentUser;



    public void init(){
        actionbarlogin = (Toolbar) findViewById(R.id.actionbarlogin);
        setSupportActionBar(actionbarlogin);
        getSupportActionBar().setTitle("Giriş Yap");
        getSupportActionBar().setDisplayHomeAsUpEnabled(true);

        auth = FirebaseAuth.getInstance();
        currentUser = auth.getCurrentUser();

        txtEmail = (EditText) findViewById(R.id.txtEmailLogin);
        txtPassword = (EditText) findViewById(R.id.txtPasswordLogin);
        btnLogin = (Button) findViewById(R.id.btnLogin);

    }

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_login);
        init();

        btnLogin.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                loginUser();
            }
        });

    }

    private void loginUser() {

        String email = txtEmail.getText().toString();
        String password = txtPassword.getText().toString();
        if (TextUtils.isEmpty(email)){
            Toast.makeText(this,"Email alanı boş olamaz", Toast.LENGTH_LONG).show();
        }else if (TextUtils.isEmpty(password)){
            Toast.makeText(this,"Parola alanı boş olamaz", Toast.LENGTH_LONG).show();
        }else {
            auth.signInWithEmailAndPassword(email, password).addOnCompleteListener(new OnCompleteListener<AuthResult>() {
                @Override
                public void onComplete(@NonNull Task<AuthResult> task) {
                    if (task.isSuccessful()){
                        Toast.makeText(LoginActivity.this,"Giriş Başarılı", Toast.LENGTH_LONG).show();
                        Intent mainIntent = new Intent(LoginActivity.this, Ana.class);
                        startActivity(mainIntent);
                        finish();
                    }else{
                        Toast.makeText(LoginActivity.this,"Giriş Başarısız!!", Toast.LENGTH_LONG).show();
                    }
                }
            });
        }

    }
}
//KULLANICI BU PANELE GELEBİLMESİ İÇİN YENİ KULLANICI OLUŞTURDUKTAN SONRADA BURAYA GELEBİLİR VEYA ZATEN KULLANICI İSE 
ANA SAYFADAN GİRİŞ YAP BUTONUNA TIKLAYARAKDA GELEBİLİR.
//KULLANICI BURADA E-MAİL VE ŞİFRESİNİ DOĞRU BİR ŞEKİLDE GİRDİKTEN SONRA UYGULAMAYA YÖNLENDİRİLİR.
//BU KOD FİREBASEUSER DAN AKTİF KULLANICILARI GETİRİR.
//GİRİLEN E-POSTA VE ŞİFRENİN DOĞRULUĞUNU KONTROL EDİYOR
//DOĞRU İSE UYGULAMANIN KARŞILAMAEKRANINA YÖNLENDİRİYOR, DEĞİL İSE TOAST İLE "BAŞARISIZ" MESAJINI VERİYOR.
---------------------------------------------------------------------------------------------------------------------------
ANA.JAVA


package com.example.saglik;

import androidx.annotation.NonNull;
import androidx.appcompat.app.ActionBarDrawerToggle;
import androidx.appcompat.app.AppCompatActivity;
import androidx.appcompat.widget.Toolbar;
import androidx.core.app.NotificationCompat;
import androidx.core.view.GravityCompat;
import androidx.drawerlayout.widget.DrawerLayout;
import androidx.fragment.app.Fragment;
import androidx.navigation.NavController;
import androidx.navigation.Navigation;
import androidx.navigation.ui.NavigationUI;

import android.app.AlarmManager;
import android.app.NotificationChannel;
import android.app.NotificationManager;
import android.app.PendingIntent;
import android.content.Context;
import android.content.Intent;
import android.os.Build;
import android.os.Bundle;
import android.os.SystemClock;
import android.util.Log;
import android.view.MenuItem;
import android.view.View;
import android.widget.Button;
import android.widget.Toast;

import com.google.android.material.navigation.NavigationView;
import com.google.firebase.auth.FirebaseAuth;
import com.google.firebase.auth.FirebaseUser;
import com.google.firebase.database.DataSnapshot;
import com.google.firebase.database.DatabaseError;
import com.google.firebase.database.DatabaseReference;
import com.google.firebase.database.FirebaseDatabase;
import com.google.firebase.database.ValueEventListener;

import java.util.Calendar;

public class Ana extends AppCompatActivity {
    private FirebaseAuth auth;
    private DatabaseReference mDatabase;
    private FirebaseUser currentUser;
    private FirebaseDatabase db;
    private NavigationView navigationView;
    private DrawerLayout drawer;
    private Toolbar toolbar;
    private Fragment fragment;
    private NotificationCompat.Builder builder;





    public void init(){
        auth = FirebaseAuth.getInstance();
        currentUser = auth.getCurrentUser();



    }

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_ana);










        init();
        final DrawerLayout drawerLayout = findViewById(R.id.drawerLayout);
        findViewById(R.id.imageMenu).setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                drawerLayout.openDrawer(GravityCompat.START);
            }
        });
        NavigationView navigationView =findViewById(R.id.navigationView);
        navigationView.setItemIconTintList(null);

        NavController navController = Navigation.findNavController(this,R.id.navHostFragment);
        NavigationUI.setupWithNavController(navigationView, navController);

    }









    @Override
    protected void onStart() {
        if (currentUser == null){
            Intent welcomeIntent = new Intent(Ana.this, MainActivity.class);
            startActivity(welcomeIntent);
            finish();
        }

        super.onStart();
    }


}
//BU SAYFADA AKTİF KULLANICI KONTROLÜ SAĞLANMAKTADIR.
//EĞER BURADA BİR AKTİF KULLANICI YOKSA MAİNACTİVTİY SAYFASINA YÖNLENDİRİLMEKTEDİR.
//ARTIK UYGULAMAYA KULLANICI İLE GİRİŞ YAPTIĞIMIZ SAYFADIR.
//BURADAN SONRA GÖRÜNÜMLERİMİZİ BELİRLEYENLER NAVİGATİONVİEW İLE OLUŞTURULAN BLANKFRAGMENTLARDIR.
---------------------------------------------------------------------------------------------------------------------------
ANASAYFAFRAGMENT.JAVA


package com.example.saglik;

import android.annotation.SuppressLint;
import android.app.Activity;
import android.content.Context;
import android.content.Intent;
import android.database.sqlite.SQLiteDatabase;
import android.hardware.SensorManager;
import android.media.session.PlaybackState;
import android.os.Bundle;

import androidx.annotation.NonNull;
import androidx.fragment.app.Fragment;

import android.provider.ContactsContract;
import android.telephony.RadioAccessSpecifier;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.ArrayAdapter;
import android.widget.Button;
import android.widget.EditText;
import android.widget.ListAdapter;
import android.widget.ListView;
import android.widget.TextView;

import com.google.firebase.auth.FirebaseAuth;
import com.google.firebase.auth.FirebaseUser;
import com.google.firebase.auth.UserProfileChangeRequest;
import com.google.firebase.database.DataSnapshot;
import com.google.firebase.database.DatabaseError;
import com.google.firebase.database.DatabaseReference;
import com.google.firebase.database.FirebaseDatabase;
import com.google.firebase.database.ValueEventListener;

import java.util.ArrayList;
import java.util.List;
import java.util.Objects;


public class AnasayfaFragment extends Fragment {
    private EditText kisiselbilgi;
    private ListView listviewbki;
    private  ArrayList<BkiModel> bkilist;
    FirebaseDatabase database;

    private TextView tv_steps;






    public AnasayfaFragment() {



    }


    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container,
                             Bundle savedInstanceState) {
        // Inflate the layout for this fragment
        View view= inflater.inflate(R.layout.fragment_anasayfa, container, false);

        tv_steps = (TextView)view.findViewById(R.id.anasayfasteps);


        bkilist = new ArrayList<BkiModel>();
        listviewbki = (ListView)view.findViewById(R.id.listviewbki);
        database=FirebaseDatabase.getInstance();
        final DatabaseReference dbRef = database.getReference("bki");
        dbRef.addValueEventListener(new ValueEventListener() {
            @Override
            public void onDataChange(@NonNull DataSnapshot dataSnapshot) {
                for(DataSnapshot ds:dataSnapshot.getChildren()){
                    String bki = ds.child("bki").getValue().toString();
                    bkilist.add(new BkiModel(bki));
                }
                CustomAdapterBki customAdapter= new CustomAdapterBki(getActivity(),bkilist);
                listviewbki.setAdapter(customAdapter);
                dbRef.removeEventListener(this);

            }

            @Override
            public void onCancelled(@NonNull DatabaseError databaseError) {

            }
        });






        return view;
    }

}

//BU FRAGMENT SAYFAMIZ ARTIK BİZİM UYGULAMAYA GİRİŞ YAPTIĞIMIZDA KULLANICIMIZI KARŞILAYAN SAYFAMIZDIR.
//BURADA KULLANICIMIZIN VERİTABININA KAYDETTİĞİ VERİLERİ KİŞİSEL BİLGİLER GÖSTERİLMEKTEDİR.
---------------------------------------------------------------------------------------------------------------------------

HEDEFFRAGMENT.JAVA


package com.example.saglik;

import android.app.AlertDialog;
import android.content.Context;
import android.database.sqlite.SQLiteCursorDriver;
import android.database.sqlite.SQLiteDatabase;
import android.os.Bundle;

import androidx.annotation.NonNull;
import androidx.appcompat.widget.Toolbar;
import androidx.fragment.app.Fragment;
import androidx.recyclerview.widget.RecyclerView;

import android.os.strictmode.SqliteObjectLeakedViolation;
import android.util.Log;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.Button;
import android.widget.EditText;
import android.widget.ListView;
import android.widget.TextView;
import android.widget.Toast;


import com.google.android.material.floatingactionbutton.FloatingActionButton;
import com.google.firebase.database.DataSnapshot;
import com.google.firebase.database.DatabaseError;
import com.google.firebase.database.DatabaseReference;
import com.google.firebase.database.FirebaseDatabase;
import com.google.firebase.database.ValueEventListener;

import java.util.ArrayList;


public class HedefFragment extends Fragment  {
    private EditText gıdaadı,calori;
    private Button kaydet;
    private ListView ListView;
   private FirebaseDatabase database;
    private Context Context;
    private Toolbar toolbar2;
    private RecyclerView rv;
    private FloatingActionButton fab;


    public HedefFragment() {


    }


    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container,
                             Bundle savedInstanceState) {
        // Inflate the layout for this fragment
      View aramaGida = inflater.inflate(R.layout.fragment_hedef, container, false);

        gıdaadı=(EditText) aramaGida.findViewById(R.id.gıdaadi);
        calori=(EditText) aramaGida.findViewById(R.id.kalori);
        kaydet =(Button)aramaGida.findViewById(R.id.gıdakaydet);
        database=FirebaseDatabase.getInstance();
        final DatabaseReference dbRef = database.getReference("aramagida");
        kaydet.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                DatabaseReference idRef= dbRef.push();
                String g_adi, kalori;
                g_adi = gıdaadı.getText().toString();
                kalori = calori.getText().toString();

                if (!g_adi.equals("") && !calori.equals("")){
                    idRef.child("Gida_Adi").setValue(g_adi);
                    idRef.child("Kalorisi").setValue(kalori);
                    gıdaadı.setText("");
                    calori.setText("");
                }else{
                    Toast.makeText(Context, "alanlar boş olamaz", Toast.LENGTH_SHORT).show();
                }

            }
        });


        return aramaGida;

     }


    }


// KULLANICININ BU SAYFAYA GELMESİ İÇİN MENÜ PANELİNİ AÇIP "GIDA EKLE" YAZISININ ÜSTÜNE TIKLAMASI GEREKİYOR.
//DAHA SONRA BURADA KULLANICI GÜNLÜK ALINAN GIDALARDAN İSTEĞİNİ GIDA ADINI VE KALORİSİNİ GİREREK KAYDEDİLMESİNİ SAĞLAR.

---------------------------------------------------------------------------------------------------------------------------

GUNLUKFRAGMENT.JAVA
package com.example.saglik;

import android.os.Bundle;

import androidx.fragment.app.Fragment;

import android.view.View;



import com.google.firebase.database.DataSnapshot;
import com.google.firebase.database.DatabaseError;
import com.google.firebase.database.DatabaseReference;
import com.google.firebase.database.FirebaseDatabase;
import com.google.firebase.database.ValueEventListener;

import androidx.annotation.NonNull;

import android.view.LayoutInflater;
import android.view.ViewGroup;
import android.widget.ListView;

import java.util.ArrayList;


public class GunlukFragment extends Fragment {
    private  FirebaseDatabase database;
   private  ArrayList<HedefModel> hedefList;
   private ListView listView;
   private CustomAdapter adapter;




    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container,
                             Bundle savedInstanceState) {
        // Inflate the layout for this fragment
         View gunluk =inflater.inflate(R.layout.fragment_gunluk, container, false);
        hedefList = new ArrayList<HedefModel>();
        listView = (ListView) gunluk.findViewById(R.id.listView);
        database =FirebaseDatabase.getInstance();

        final DatabaseReference dbRef=database.getReference("hedef");

        dbRef.addValueEventListener(new ValueEventListener() {
            @Override
            public void onDataChange(@NonNull DataSnapshot dataSnapshot) {
                for (DataSnapshot ds:dataSnapshot.getChildren()){

                    String kalori = ds.child("Hedef_Kalori").getValue().toString();
                    String adim = ds.child("Hedef_Adim").getValue().toString();
                    String su =ds.child("Hedef_Su").getValue().toString();
                    hedefList.add(new HedefModel(kalori,adim,su));
                }
                CustomAdapter adapter = new CustomAdapter(getActivity(),hedefList);
                listView.setAdapter(adapter);
                dbRef.removeEventListener(this);

            }

            @Override
            public void onCancelled(@NonNull DatabaseError databaseError) {

            }
        });







         return gunluk;
    }
}

//KULLANICI BU SAYFAYA GELEBİLMESİ İÇİN MENÜ PANELİNDE GÜNLÜK YAZISINA TIKLADIĞINDA BU SAYFAYA GELECEKTİR.
//BURADA KULLANICININ BELİRLEDİĞİ HEDEFLER GÖRÜLMEKTEDİR.
//BU HEDEFLER KULLANACININ DAHA ÖNCE KAYDETTİĞİ VERİTABANINDAN ÇEKİLMEKTEDİR.

---------------------------------------------------------------------------------------------------------------------------

HATIRLATMALAR.JAVA

package com.example.saglik;

import android.app.AlarmManager;
import android.app.NotificationChannel;
import android.app.NotificationManager;
import android.app.PendingIntent;

import android.content.Context;
import android.content.Intent;
import android.os.Build;
import android.os.Bundle;

import androidx.core.app.NotificationCompat;
import androidx.fragment.app.Fragment;

import android.os.SystemClock;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.Button;
import android.widget.EditText;
import android.widget.ImageView;
import android.widget.TextView;

import java.util.Calendar;


/**
 * A simple {@link Fragment} subclass.
 */
public class HatirlatmalarFragment extends Fragment {

    private Button butonbildirdis,butonbildiruyku,butonbildirsu;
    private NotificationCompat.Builder builder;
    private TextView tith,water,sleep;
    private ImageView imgsleep,imgwater,imgtith;
    public HatirlatmalarFragment() {
        // Required empty public constructor
    }


    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container,
                             Bundle savedInstanceState) {
        // Inflate the layout for this fragment
        View Hatırlatmalar = inflater.inflate(R.layout.fragment_hatirlatmalar, container, false);
        imgsleep = (ImageView)Hatırlatmalar.findViewById(R.id.imgsleep);
        imgtith=(ImageView)Hatırlatmalar.findViewById(R.id.imgtith);
        imgwater = (ImageView)Hatırlatmalar.findViewById(R.id.imgwater);
        tith = (TextView) Hatırlatmalar.findViewById(R.id.tith);
        water=(TextView)Hatırlatmalar.findViewById(R.id.water);
        sleep=(TextView)Hatırlatmalar.findViewById(R.id.sleeps);
        butonbildirdis = (Button) Hatırlatmalar.findViewById(R.id.butonbildirdis);
        butonbildirsu= (Button) Hatırlatmalar.findViewById(R.id.butonbildirsu);
        butonbildiruyku = (Button)Hatırlatmalar.findViewById(R.id.butonbildiruyku);
        butonbildirsu.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                gecikmeliBildirim();

            }

            private void gecikmeliBildirim() {
                NotificationManager bildirimyoneticisi = (NotificationManager)getActivity().getSystemService(Context.NOTIFICATION_SERVICE);
                Intent intent = new Intent(getActivity(),HedefFragment.class);
                PendingIntent gidilecekintent = PendingIntent.getActivity(getActivity(),1,intent,PendingIntent.FLAG_UPDATE_CURRENT);




                if (Build.VERSION.SDK_INT>=Build.VERSION_CODES.O){
                    String kanalId ="kanalId";
                    String kanalAd ="kanalAd";
                    String kanalTanim="kanalTanim";
                    int kanalOnceligi = NotificationManager.IMPORTANCE_HIGH;
                    NotificationChannel kanal = bildirimyoneticisi.getNotificationChannel(kanalId);
                    if (kanal == null){
                        kanal = new NotificationChannel(kanalId,kanalAd,kanalOnceligi);
                        kanal.setDescription(kanalTanim);
                        bildirimyoneticisi.createNotificationChannel(kanal);
                    }
                    builder = new NotificationCompat.Builder(getActivity(),kanalId);
                    builder.setContentTitle("Saglik");
                    builder.setContentText("Su İçmeyi Unutma !");
                    builder.setSmallIcon(R.drawable.resim);
                    builder.setAutoCancel(true);
                    builder.setContentIntent(gidilecekintent);



                }else {
                    builder = new NotificationCompat.Builder(getActivity());
                    builder.setContentTitle("Saglik");
                    builder.setContentText("Su İçmeyi Unutma !");
                    builder.setSmallIcon(R.drawable.resim);
                    builder.setAutoCancel(true);
                    builder.setContentIntent(gidilecekintent);
                    builder.setPriority(NotificationCompat.PRIORITY_HIGH);

                }
                Intent boradcastIntent =new Intent(getActivity(),BildirimYakalayıcı.class);
                boradcastIntent.putExtra("nesne",builder.build());
                PendingIntent gidilecekBroadcast = PendingIntent.getBroadcast(getActivity(),0,boradcastIntent,PendingIntent.FLAG_UPDATE_CURRENT);
                long gecikme = SystemClock.elapsedRealtime()+5000;

                Calendar calendar= Calendar.getInstance();
                calendar.set(Calendar.HOUR_OF_DAY,8);
                calendar.set(Calendar.MINUTE,30);



                AlarmManager alarmManager = (AlarmManager)getActivity().getSystemService(Context.ALARM_SERVICE);
                alarmManager.setRepeating(AlarmManager.RTC_WAKEUP,calendar.getTimeInMillis(),1000*60*30,gidilecekBroadcast);



                bildirimyoneticisi.notify(1,builder.build());

            }
        });

        butonbildiruyku.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                uykuBildirim();
            }

            private void uykuBildirim() {
                NotificationManager bildirimyoneticisi = (NotificationManager)getActivity().getSystemService(Context.NOTIFICATION_SERVICE);
                Intent intent = new Intent(getActivity(),HedefFragment.class);
                PendingIntent gidilecekintent = PendingIntent.getActivity(getActivity(),1,intent,PendingIntent.FLAG_UPDATE_CURRENT);




                if (Build.VERSION.SDK_INT>=Build.VERSION_CODES.O){
                    String kanalId ="kanalId";
                    String kanalAd ="kanalAd";
                    String kanalTanim="kanalTanim";
                    int kanalOnceligi = NotificationManager.IMPORTANCE_HIGH;
                    NotificationChannel kanal = bildirimyoneticisi.getNotificationChannel(kanalId);
                    if (kanal == null){
                        kanal = new NotificationChannel(kanalId,kanalAd,kanalOnceligi);
                        kanal.setDescription(kanalTanim);
                        bildirimyoneticisi.createNotificationChannel(kanal);
                    }
                    builder = new NotificationCompat.Builder(getActivity(),kanalId);
                    builder.setContentTitle("Saglik");
                    builder.setContentText("Uyku Vakti !");
                    builder.setSmallIcon(R.drawable.resim);
                    builder.setAutoCancel(true);
                    builder.setContentIntent(gidilecekintent);



                }else {
                    builder = new NotificationCompat.Builder(getActivity());
                    builder.setContentTitle("Saglik");
                    builder.setContentText("Uyku Vakti !");
                    builder.setSmallIcon(R.drawable.resim);
                    builder.setAutoCancel(true);
                    builder.setContentIntent(gidilecekintent);
                    builder.setPriority(NotificationCompat.PRIORITY_HIGH);

                }
                Intent boradcastIntent =new Intent(getActivity(),BildirimYakalayıcı.class);
                boradcastIntent.putExtra("nesne",builder.build());
                PendingIntent gidilecekBroadcast = PendingIntent.getBroadcast(getActivity(),0,boradcastIntent,PendingIntent.FLAG_UPDATE_CURRENT);
                long gecikme = SystemClock.elapsedRealtime()+5000;

                Calendar calendar= Calendar.getInstance();
                calendar.set(Calendar.HOUR_OF_DAY,21);
                calendar.set(Calendar.MINUTE,30);



                AlarmManager alarmManager = (AlarmManager)getActivity().getSystemService(Context.ALARM_SERVICE);
                alarmManager.setRepeating(AlarmManager.RTC_WAKEUP,calendar.getTimeInMillis(),1000*60*60*24,gidilecekBroadcast);



                bildirimyoneticisi.notify(1,builder.build());

            }
        });
        butonbildirdis.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {


                disfırcalamaBildirim();
            }

            private void disfırcalamaBildirim() {
                NotificationManager bildirimyoneticisi = (NotificationManager)getActivity().getSystemService(Context.NOTIFICATION_SERVICE);
                Intent intent = new Intent(getActivity(),HedefFragment.class);
                PendingIntent gidilecekintent = PendingIntent.getActivity(getActivity(),1,intent,PendingIntent.FLAG_UPDATE_CURRENT);




                if (Build.VERSION.SDK_INT>=Build.VERSION_CODES.O){
                    String kanalId ="kanalId";
                    String kanalAd ="kanalAd";
                    String kanalTanim="kanalTanim";
                    int kanalOnceligi = NotificationManager.IMPORTANCE_HIGH;
                    NotificationChannel kanal = bildirimyoneticisi.getNotificationChannel(kanalId);
                    if (kanal == null){
                        kanal = new NotificationChannel(kanalId,kanalAd,kanalOnceligi);
                        kanal.setDescription(kanalTanim);
                        bildirimyoneticisi.createNotificationChannel(kanal);
                    }
                    builder = new NotificationCompat.Builder(getActivity(),kanalId);
                    builder.setContentTitle("Saglik");
                    builder.setContentText("Diş Fırçalama Zamanı !");
                    builder.setSmallIcon(R.drawable.resim);
                    builder.setAutoCancel(true);
                    builder.setContentIntent(gidilecekintent);



                }else {
                    builder = new NotificationCompat.Builder(getActivity());
                    builder.setContentTitle("Saglik");
                    builder.setContentText("Diş Fırçalama Zamanı !");
                    builder.setSmallIcon(R.drawable.resim);
                    builder.setAutoCancel(true);
                    builder.setContentIntent(gidilecekintent);
                    builder.setPriority(NotificationCompat.PRIORITY_HIGH);

                }
                Intent boradcastIntent =new Intent(getActivity(),BildirimYakalayıcı.class);
                boradcastIntent.putExtra("nesne",builder.build());
                PendingIntent gidilecekBroadcast = PendingIntent.getBroadcast(getActivity(),0,boradcastIntent,PendingIntent.FLAG_UPDATE_CURRENT);
                long gecikme = SystemClock.elapsedRealtime()+5000;

                Calendar calendar= Calendar.getInstance();
                calendar.set(Calendar.HOUR_OF_DAY,8);
                calendar.set(Calendar.MINUTE,30);



                AlarmManager alarmManager = (AlarmManager)getActivity().getSystemService(Context.ALARM_SERVICE);
                alarmManager.setRepeating(AlarmManager.RTC_WAKEUP,calendar.getTimeInMillis(),1000*60*60*12,gidilecekBroadcast);



                bildirimyoneticisi.notify(1,builder.build());
            }


        });







        return Hatırlatmalar;
    }



}

//KULLLANICI BU SAYFAYA GİRİŞ YAPABİLMESİ İÇİN MENÜ PANELİNDEN HATIRLATMALARA TIKLANMASI GEREKMEKTEDİR.
//BU SAYFA DA KULLANICI GÜNLÜK ALMAK İSTEDİĞİ HATIRLATM.ALRA TIKLAYARAK BUNLARI AKTİFLEŞTİRİR.
//BU HATIRLATMALAR SU İÇME, UYKU(21.30),DİŞ FIRÇALAMA (8.30-20.30) HATIRLATMALARIDIR.
//BU KOD İÇİN ALARM_SERVİCE İ VE RTC_WAKEUP İLE GERÇEK SAATİ ALDIK.

---------------------------------------------------------------------------------------------------------------------------

package com.example.saglik;

import android.database.sqlite.SQLiteDatabase;
import android.os.Bundle;

import androidx.annotation.IntegerRes;
import androidx.fragment.app.Fragment;

import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;

import com.google.firebase.database.DatabaseReference;
import com.google.firebase.database.FirebaseDatabase;


/**
 * A simple {@link Fragment} subclass.
 */


public class SaglikhesaplaFragment extends Fragment {
    Button sonuc;
    EditText boy,kilo,yas;
    TextView text,text2;
    Float bki, boytext,kilotext;
    Integer yuvarlama;
    FirebaseDatabase database;


    public SaglikhesaplaFragment() {
        // Required empty public constructor




    }


    @Override
    public View onCreateView(final LayoutInflater inflater, ViewGroup container,
                             Bundle savedInstanceState) {
        // Inflate the layout for this fragment
       View view= inflater.inflate(R.layout.fragment_saglikhesapla, container, false);
        database=FirebaseDatabase.getInstance();
        final DatabaseReference dbRef = database.getReference("bki");
       sonuc =(Button)view.findViewById(R.id.sonuc);
       kilo = (EditText)view.findViewById(R.id.kilo);
       boy = (EditText)view.findViewById(R.id.boy);
       yas = (EditText)view.findViewById(R.id.yas);
       text = (TextView) view.findViewById(R.id.textVier1);
       text2 = (TextView) view.findViewById(R.id.textVier2);

       sonuc.setOnClickListener(new View.OnClickListener() {
           @Override
           public void onClick(View v) {


               kilotext=Float.parseFloat(kilo.getText().toString());
               boytext=Float.parseFloat(boy.getText().toString());
               bki= kilotext/(boytext*boytext);
               yuvarlama=(int)Math.ceil(bki);

               text.setText("Vücut Kütle Endeksiniz:"+yuvarlama.toString());

               if(yuvarlama<=18.5){
                   text2.setText("Zayıf");
               }else if(18.5<= yuvarlama && yuvarlama <= 24.5){
                   text2.setText("Kilonuz Normal");
               }else if(25.0<= yuvarlama && yuvarlama <= 29.9){
                   text2.setText("Fazla Kilolu");
               }else if(30.0<= yuvarlama && yuvarlama<=34.9){
                   text2.setText("1. Derece Obez");
               }else if (35.0<=yuvarlama && yuvarlama <= 40){
                   text2.setText("2. Derece Obez");
               }else {
                   text2.setText("3. Derece Obez");
               }


               DatabaseReference idRef= dbRef.push();
               String t_yuvarlama;
               t_yuvarlama = text.getText().toString();

               if (!t_yuvarlama.equals("")){
                   idRef.child("bki").setValue(t_yuvarlama);
               }

           }
       });




        return view;
    }
}

//BULLANICI BU SAYFAYA GELMESİ İÇİN MENÜ PANELİNDEN SAĞLIK HESAPLAMAYA TIKLAMASI GEREKMEKTEDİR.
//KULLANICI BURADA BOY,KİLO,YAŞINI GİRDKTEN SONRA SİSTEM BUNU HESAPLAYIP KİLO ENDEKSİNİ SÖYLÜYOR VE BUNA BAĞLI OLARAK
KİLOSU HAKKINDA YORUMDA BULUNUYOR BU KİLOENDEKSİNİ VERİTABANINA KAYDEDEREK ANASAYFADA GÖRÜNTÜLENMESİNİ SAĞLIYOR.



---------------------------------------------------------------------------------------------------------------------------
ADİMSAYARFRAGMENT.JAVA 

package com.example.saglik;

import android.content.Context;
import android.hardware.Sensor;
import android.hardware.SensorEvent;
import android.hardware.SensorEventListener;
import android.hardware.SensorManager;
import android.os.Bundle;
import android.widget.Toast;

import androidx.fragment.app.Fragment;

import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.TextView;
import android.widget.Toast;

import com.google.firebase.database.DatabaseReference;
import com.google.firebase.database.FirebaseDatabase;

import java.util.Objects;


/**
 * A simple {@link Fragment} subclass.
 */
public class AdimsayarFragment extends Fragment implements SensorEventListener {
    private SensorManager sensorManager;
    private TextView tv_steps;
    private boolean running =false;
    FirebaseDatabase database;


    public AdimsayarFragment() {
        // Required empty public constructor
    }


    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container,
                             Bundle savedInstanceState) {
        // Inflate the layout for this fragment
        View adimview=  inflater.inflate(R.layout.fragment_adimsayar, container, false);
        tv_steps = (TextView) adimview.findViewById(R.id.tv_steps);
        sensorManager = (SensorManager) Objects.requireNonNull(getContext()).getSystemService(Context.SENSOR_SERVICE);





        return adimview;
    }
    @Override
    public void onResume() {
        super.onResume();
        running = true;
        Sensor countSensor = sensorManager.getDefaultSensor(Sensor.TYPE_STEP_COUNTER);
        if (countSensor != null){
            sensorManager.registerListener(this,countSensor, SensorManager.SENSOR_DELAY_UI);
        }else {
            Toast.makeText(getView().getContext(), "default", Toast.LENGTH_SHORT).show();
        }


    }


    @Override
    public void onPause() {
        super.onPause();
        running = false;


    }

    @Override
    public void onSensorChanged(SensorEvent event) {

        if (running){
            tv_steps.setText(String.valueOf(event.values[0]));
        }

    }

    @Override
    public void onAccuracyChanged(Sensor sensor, int accuracy) {

    }
}

//YUKARIDAKİ KODUN ÇALIŞTIRILMASI İÇİN PROGRAMA GİRİŞYAPILDIĞINDAN İTİBAREN ÇALIŞIYOR.
//DEĞER OKUMAK İÇİN YANİ ATILAN ADIM SAYISINI GÖRMEK İÇİN BU FRAGMENT A GİRİLMESİ GEREKİYOR.
//KODDA SENSÖRLERİ AKTİFLEŞTİRDİK VE BU SENSÖRLERDEN ELDE ETTİĞİMİZ VERİYİ TV_STEPS DİYE ADLANDIRDIĞIMIZ 
TEXTVİEW DA GÖSTERDİK.
---------------------------------------------------------------------------------------------------------------------------

ARAMAGIDA.JAVA

package com.example.saglik;

import android.app.Activity;
import android.app.DirectAction;
import android.os.Bundle;

import androidx.annotation.NonNull;
import androidx.fragment.app.Fragment;
import androidx.recyclerview.widget.LinearLayoutManager;
import androidx.recyclerview.widget.RecyclerView;

import android.provider.ContactsContract;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.Adapter;
import android.widget.EditText;
import android.widget.ImageButton;
import android.widget.ListView;
import android.widget.TextView;

import com.firebase.ui.database.FirebaseRecyclerAdapter;
import com.google.firebase.database.DataSnapshot;
import com.google.firebase.database.DatabaseError;
import com.google.firebase.database.DatabaseReference;
import com.google.firebase.database.FirebaseDatabase;
import com.google.firebase.database.Query;
import com.google.firebase.database.ValueEventListener;

import java.util.ArrayList;

import pub.devrel.easypermissions.EasyPermissions;


public class Aramagida extends Fragment {
    FirebaseDatabase database;
    private ArrayList<Gıda> gıdaList;
    ListView listviewgıda;



    public Aramagida() {

    }

    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container,
                             Bundle savedInstanceState) {

        View GıdaArama =inflater.inflate(R.layout.fragment_aramagida, container, false);
        gıdaList =new ArrayList<Gıda>();
        listviewgıda = (ListView) GıdaArama.findViewById(R.id.listviewgida);
        database =FirebaseDatabase.getInstance();
        final DatabaseReference dbRef = database.getReference("aramagida");
        dbRef.addValueEventListener(new ValueEventListener() {
            @Override
            public void onDataChange(@NonNull DataSnapshot dataSnapshot) {
                for (DataSnapshot ds:dataSnapshot.getChildren()){
                    String name = ds.child("Gida_Adi").getValue().toString();
                    String kalori = ds.child("Kalorisi").getValue().toString();
                    gıdaList.add(new Gıda(kalori,name));
                }
                CustomAdaptergida customAdaptergida = new CustomAdaptergida(getActivity(),gıdaList);
                listviewgıda.setAdapter(customAdaptergida);
                dbRef.removeEventListener(this);
            }

            @Override
            public void onCancelled(@NonNull DatabaseError databaseError) {

            }
        });



        return GıdaArama;
    }





}

//KULLANICI BU SAYFAYA GELEBİLMESİ İÇİN MENU PANEL DEN "GIDA ARAMA" SAYFASINA TIKLAMASI GEREKİR.
//BURADA KULLANICININ DAHA ÖNCEDEN KAYDETTİĞİ GIDALAR GÖRÜNTÜLENMEKTEDİR.
//BU GIDALAR KULLANICININ DAHA ÖNCEDEN VERİTABANINA KAYDETTİĞİ VERİLERİ VERİ TABANINDAN ÇEKEREK LİSTVİEW
ARACILIĞI İLE GÖRÜNTÜLENMESİNİ SAĞLAMAKTADIR.
 
---------------------------------------------------------------------------------------------------------------------------

HEDEFEKLE.JAVA

package com.example.saglik;

import android.content.Context;
import android.os.Bundle;

import androidx.fragment.app.Fragment;

import android.provider.ContactsContract;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import android.widget.Toast;

import com.google.firebase.auth.FirebaseAuth;
import com.google.firebase.database.DatabaseReference;
import com.google.firebase.database.FirebaseDatabase;

import java.util.HashMap;


public class Hedefekle extends Fragment {

   private Button hedefkaydet;
   private EditText gunlukkalori,textadim,textsu;
  private TextView hedefsu,hedefadim,hedefkalori;
    private FirebaseDatabase database;
    private Context Context;
    private FirebaseAuth mAuth;

    public Hedefekle() {


    }


    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container,
                             Bundle savedInstanceState) {

       View hedefekle =inflater.inflate(R.layout.fragment_hedefekle, container, false);
       mAuth = FirebaseAuth.getInstance();
        final String user_id = mAuth.getCurrentUser().getUid();
        database=FirebaseDatabase.getInstance();
        final DatabaseReference dbRef = database.getReference("hedef");
        gunlukkalori = (EditText)hedefekle.findViewById(R.id.gunlukkalori);
        textadim = (EditText)hedefekle.findViewById(R.id.textadim);
        textsu = (EditText) hedefekle.findViewById(R.id.textsu);
        hedefsu = (TextView)hedefekle.findViewById(R.id.hedefsu);
        hedefadim = (TextView)hedefekle.findViewById(R.id.hedefadim);
        hedefkalori = (TextView)hedefekle.findViewById(R.id.hedefkalori);
        hedefkaydet = (Button)hedefekle.findViewById(R.id.hedefkaydet);
        hedefkaydet.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {

                DatabaseReference idRef = dbRef.push();
                String h_adim,h_kalori,h_su;
                h_adim=textadim.getText().toString();
                h_kalori = gunlukkalori.getText().toString();
                h_su = textsu.getText().toString();


                if (!h_adim.equals("") && !h_kalori.equals("") && !h_su.equals("")){


                    idRef.child("Hedef_Kalori").setValue(h_kalori);
                    idRef.child("Hedef_Adim").setValue(h_adim);
                    idRef.child("Hedef_Su").setValue(h_su);

                    gunlukkalori.setText("");
                    textadim.setText("");
                    textsu.setText("");
                }else{
                    Toast.makeText(Context,"alanlar boş olamaz",Toast.LENGTH_SHORT).show();
                }

            }
        });









       return hedefekle;
    }
}

// KLLANICI BU SAYFAYA GELEBİLMEK İÇİN MENÜ PANELİNDEN "HEDEF" E TIKLAMASI GEREKMEKTEDİR.
//KULLANICI İLGİLİALANLARA HEDEF OLARAK ALMAK İSTEDİĞİ KALORİYİ,LİMİT SU İÇİMİNİ, LİMİT ATMASI GEREKEN ADIM SAYISINI
GİREREK KENDİNE HEDEF BEİRLER.
//KADYET BUTONUNA TIKLANILDIĞINDA KULLANICININ BU HEDEFİ OLUŞTURDUĞUMUZ REFERANS İLE KAYDEDİLİR.
/DAHA SONRA GÜNLÜK SAYFASINDA LİSTELİBİRŞEKİLDE GÖRÜNTÜLENİR.
***************************************************************************************************************************

YARDIMCI JAVA CLASS LARIMIZ
---------------------------------------------------------------------------------------------------------------------------


HEDEFMODEL.JAVA

package com.example.saglik;

public class HedefModel {
    private String kalori,adim,su;
    public HedefModel (String kalori, String adim,String su){
        this.kalori = kalori;
        this.adim = adim;
        this.su = su;


    }
    public String getKalori(){
        return kalori;
    }
    public void setKalori(String kalori){
        this.kalori = kalori;
    }
    public String getAdim(){
        return adim;
    }
    public void setAdim(String adim){
        this.adim = adim;
    }
    public String getSu(){
        return su;
    }
    public void setSu(String su){
        this.su = su;
    }




}

//BU CLASS IMIZ VERİTABANIMIZA KAYDETTİĞİMİZ HEDEFİ VERİTABANINDAN ÇEKMEK İÇİN KULLANDIĞIMIZ BİR MODEL CLASSIMIZDIR.



---------------------------------------------------------------------------------------------------------------------------
CUSTOMADAPTER.JAVA


package com.example.saglik;

import android.annotation.SuppressLint;
import android.app.Activity;
import android.content.Context;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.BaseAdapter;
import android.widget.TextView;

import java.util.ArrayList;

public class CustomAdapter extends BaseAdapter {
    LayoutInflater layoutInflater;
    ArrayList<HedefModel> hedefList;
    public CustomAdapter(Activity activity, ArrayList<HedefModel> hedefList){
        layoutInflater = (LayoutInflater) activity.getSystemService(Context.LAYOUT_INFLATER_SERVICE);
        this.hedefList = hedefList;
    }
    @Override
    public int getCount() {
        return hedefList.size();
    }

    @Override
    public Object getItem(int position) {
        return hedefList.get(position);
    }

    @Override
    public long getItemId(int position) {
        return position;
    }

    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
       HedefModel hedef = hedefList.get(position);
       @SuppressLint({"ViewHolder", "InflateParams"}) View satir = layoutInflater.inflate(R.layout.custom_satir,null);
       TextView kalori = (TextView)satir.findViewById(R.id.Hedef_kalori);
       TextView adim = (TextView)satir.findViewById(R.id.Hedef_adim);
       TextView su = (TextView)satir.findViewById(R.id.Hedef_Su);
       kalori.setText(hedef.getKalori());
       adim.setText(hedef.getAdim());
       su.setText(hedef.getSu());
       return satir;
    }
}
// BU SINIFIMIZ BİZE VERİTABANINDAN GETİRELEECEK OLAN BELİRDELİĞİMİZ HEDEF, SU ,KALORİ Yİ ARRAYLİST OLUŞTURARAK 
LİSTELEMEMİZİ SAĞLAR.

---------------------------------------------------------------------------------------------------------------------------
GIDA.JAVA

package com.example.saglik;

public class Gıda {
    public String kalori,name;
    public Gıda(String kalori,String name){
        this.kalori = kalori;
        this.name = name;
    }
    public String getKalori(){
        return kalori;
    }
    public void setKalori(String kalori){
        this.kalori = kalori;
    }
    public String getName(){
        return name;
    }
    public void setName(String name){
        this.name= name;
    }


}
//BU SINIFIMIZ HEDEFMODEL.JAVA DA Kİ GİBİ AMA EKLEDİĞİMİZ GIDALARI GIDA ARAMA SAYFASINDA GÖSTERİLMESİ İÇİN YARDIMCI 
SINIFIMIZDIR.
//BURADA LİSTELENECEK OLAN VERİLERİ TANIMLAMASINI YAPILDI.
---------------------------------------------------------------------------------------------------------------------------




CUSTOMADAPTERGİDA.JAVA 
package com.example.saglik;

import android.app.Activity;
import android.content.Context;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.BaseAdapter;
import android.widget.TextView;

import java.util.ArrayList;

public class CustomAdaptergida extends BaseAdapter {
    LayoutInflater layoutInflater;
    ArrayList<Gıda> gıdaList;

    public CustomAdaptergida (Activity activity,ArrayList<Gıda> gıdaList){
        layoutInflater = (LayoutInflater)activity.getSystemService(Context.LAYOUT_INFLATER_SERVICE);
        this.gıdaList = gıdaList;
    }


    @Override
    public int getCount() {
        return gıdaList.size();
    }

    @Override
    public Object getItem(int position) {
        return gıdaList.get(position);
    }

    @Override
    public long getItemId(int position) {
        return position;
    }

    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        Gıda gıda = gıdaList.get(position);
        View satir = layoutInflater.inflate(R.layout.custom_satirgida,null);
        TextView name = (TextView) satir.findViewById(R.id.textViewİsim);
        TextView kalori = (TextView)satir.findViewById(R.id.textViewKalori);
        name.setText(gıda.getName());
        kalori.setText(gıda.getKalori());
        return satir;
    }
}

//BURADA GIDA.JAVA DA TANIMLAMASI YAILAN VERİLERİLERİN NEREYE YERLEŞECEĞİ BELİRLENDİ
//BELİRLENEN YERLER ARRAYLİST YÖNTEMİ İLE LİSTELİ OLARAK GÖSTERİLMESİ SAĞLANMIŞTIR.

---------------------------------------------------------------------------------------------------------------------------

BKİMODEL.JAVA

package com.example.saglik;

public class BkiModel {
    private String bki;
    public BkiModel(String bki){
        this.bki = bki;
    }
    public String getBki(){return bki;
    }
    public void setBki(String bki){
        this.bki= bki;
    }
}

//BURADA KULLANICININ VERİLERİNİGİREREK HESAPLANAN VE VERİTABANINA KAYDEDİLEN VÜCUT KÜTLE ENDEKSİNİ VERİTABANINDAN 
ÇEKİLİP KULLANICIYA GÖSTERİLMESİ İÇİN YARDIMCI BİR JAVA SINIFI OLUŞTURDUK.
//BU SINIF VERİNİN GÖSTERİLMESİNİSAĞLAYACAKTIR.

---------------------------------------------------------------------------------------------------------------------------

CUSTOMADAPTERBKİ.JAVA

package com.example.saglik;

import android.app.Activity;
import android.content.Context;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.BaseAdapter;
import android.widget.TextView;

import java.util.ArrayList;

public class CustomAdapterBki extends BaseAdapter {
    LayoutInflater layoutInflater;
    ArrayList<BkiModel> bkiList;
    public CustomAdapterBki(Activity activity, ArrayList<BkiModel> bkiList){
        layoutInflater = (LayoutInflater)activity.getSystemService(Context.LAYOUT_INFLATER_SERVICE);
        this.bkiList = bkiList;
    }
    @Override
    public int getCount() {
        return bkiList.size();
    }

    @Override
    public Object getItem(int position) {
        return bkiList.get(position);
    }

    @Override
    public long getItemId(int position) {
        return position;
    }

    @Override
    public View getView(int position, View convertView, ViewGroup parent) {

        BkiModel bki = bkiList.get(position);
        View satir = layoutInflater.inflate(R.layout.custom_satirbki,null);
        TextView bkilist = (TextView) satir.findViewById(R.id.textViewBki);
        bkilist.setText(bki.getBki());

        return satir;
    }
}

//BU SINIF BKİMODEL.JAVA SINIFINDA GÖSTERİLMESİNİ SAĞLAYACAĞIMIZ BKİ VERİSİNİ NEREDE GÖSTERİLECEĞİNİ SAĞLAYAN
ADAPTER SINIFIDIR.
//BURADA VERİYİ ARRAY LİST OLUŞTURARAK KULLANICININ ZAMAN İÇERİSİNDEKİ DEĞİŞİKLİKLERİ GÖSTERMEK AMACI İLE LİSTELİ
ŞEKİLDE TUTMAK HEDEFLENDİ.

---------------------------------------------------------------------------------------------------------------------------

BİLDİRİMYAKALAYICI.JAVA
package com.example.saglik;

import android.app.Notification;
import android.app.NotificationManager;
import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;

public class BildirimYakalayıcı extends BroadcastReceiver {

    @Override
    public void onReceive(Context context, Intent intent) {
        NotificationManager bildirimYoneticisi = (NotificationManager) context.getSystemService(Context.NOTIFICATION_SERVICE);
        Notification bildirim =intent.getParcelableExtra("nesne");
        bildirimYoneticisi.notify(1,bildirim);


    }
}

//BU SINIFIMIZ BİZE HATIRLATMALAR SINIFINDAN BUTONLARA TIKLANILDIĞINDA BİLDİRİM GÖNDERMESİNİ SAĞLAYAN RECEİVER SINIFIMIZDIR.
****************************************************************************************************************************

XML DOSYALARIMIZ (LAYOUT İÇERİSİNDEKİ)
---------------------------------------------------------------------------------------------------------------------------
ACTİONBAR_APP.XML

<?xml version="1.0" encoding="utf-8"?>
<androidx.appcompat.widget.Toolbar xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:background="@color/colorAccent"
    android:theme="@style/ThemeOverlay.AppCompat.Dark.ActionBar"
    android:id="@+id/pnlActionBar"

    />

---------------------------------------------------------------------------------------------------------------------------
ACTİVİTY_ANA.XML

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

//ANA.JAVA CLASS SAYFASININ XML DOSYASI

---------------------------------------------------------------------------------------------------------------------------
ACTİVİTY_LOGİN.XML

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

//ACTİVİTYLOGİN.JAVA SAYFASININ XML KODLARIDIR.
//KULLANICININ GÖRDÜĞÜ GÖRSELLİKLER BURADA YER ALMAKTADIR.

---------------------------------------------------------------------------------------------------------------------------

ACTİVİTY_MAİN.XML

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


//GİRİŞ EKRANININ TASARIM XML TASARIM KODUDUR.
//BURADA İKİ ADET BUTTON VE BİR ADET TEXTVİEW VE BİR ADET IMAGEVİEW TANIMLAMASI YAPILDI.

---------------------------------------------------------------------------------------------------------------------------

ACTİVİTY_REGİSTER.XML

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

//KAYIT OLMA SAYFASINDAKİ TASARIMIN GÖSTERİLDİĞİ BÖLÜMDÜR.
//BURADA BİR ADET BUTTON, ÜÇ ADET EDİTTEXT, İKİ ADET TEXTVİEW TANIMLANDI.

---------------------------------------------------------------------------------------------------------------------------

FRAGMENT_ADİMSAYAR.XML

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

// ADIMSAYAR SAYFAMIZIN XML KODLARIDIR. 
// BURADA BİR ADET IMAGEVİEW KULLANILDI, İKİ ADET TEXTVİEW KULLANILDI.
//TV_STEPS İD Lİ TEXTVİEW BİZİM ADIM SAYISINI GÖSTERMEKTEDİR.

---------------------------------------------------------------------------------------------------------------------------

FRAGMENT_ANASAYFA.XML

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

//ANASAYFAFRAGMENT.JAVA  SINIFIMIZIN VE ANASAYFA OLARAK ADLANDIRDIĞIMIZ SAYFANIN TASARIM KISMI,XML KODLARIDIR.
// BİR ADET LİSTVİEW KULLANILDI.
//İD:LİSTVİEWBKİ OLARAK ADLANDIRILAN LİSTVİEW BİZİM KULLANICIMIZIN HESAPLADIĞI KÜTLE ENDEKSLERİNİ LİSTELEMEYE YARIYOR.
---------------------------------------------------------------------------------------------------------------------------

FRAGMENT_ARAMAGİDA.XML

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

//GIDA ARAMA DİYE ADLANDIRDIĞIMIZ ARAMAGIDA.JAVA SINIFIMIZIN XML KODLARIDIR.
//BİR ADET TEXTVİEW VARDIR O DA BİLGİ METNİ VERMEKTEDİR.
//BİRADET LİSTVİEW BULUNMAKTADIR O DA BİZLERE EKLENEN GIDALARIN ADI VE KALORİ OLARAK LİSTELEMEKTEDİR.

---------------------------------------------------------------------------------------------------------------------------

FRAGMENT_GUNLUK.XML

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

//GUNLUK OLARAK ADLANDIRDIĞIMIZ GUNLUKFRAGMENT.JAVA İSİMLİ SINIFIMIZIN TASARIM KODLARIDIR.
//BİR ADET TEXTVİEW VARDIR.BU TEXTVİEW BİZE BİLGİ METNİSUNMAKTADIR.
//BİR ADETLİSTVİEW BULUNMAKTADIR.BU DA BİZE KULLANICININ HEDEFLERİNİ BELİRLEYİP KAYDETTİKTEN SONRA BURADA LİSTELENMESİNİ 
SAĞLAMAKTADIR.
---------------------------------------------------------------------------------------------------------------------------

FRAGMENT_HATIRLATMALAR.JAVA
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


//HATIRLATMALARFRAGMENT.JAVA İSİMLİ SINIFIN XML TASARIM KODLARIDIR.
//BURADA ÜÇ ADET IMAGEVİEW,ÜÇ ADET TEXTVİEW,ÜÇADET BYTTON TANIMLANMIŞTIR.
//TEXTVİEW LAR KULLANICIYA BİLGİ METNİ SUNMAKTADIR.
//BUTTON LAR İSE BUTO İSMİYLE İLGİLİ TEXTVİEW BİLGİSİNE GÖRE HATIRLATMALAR KURMAKTADIR.
---------------------------------------------------------------------------------------------------------------------------

FRAGMENT_HEDEF.XML

<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".HedefFragment">


    <EditText
        android:id="@+id/gıdaadi"
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
        android:id="@+id/gıdakaydet"
        android:layout_width="100dp"
        android:layout_height="50dp"
        android:hint="@string/save"
        android:layout_marginTop="120dp"

        />

</RelativeLayout>

//HEDEFFRAGMENT.JAVA İSİMLİKLASÖRÜN LAYOUT XML DOSYASIDIR.
//BURADA KULLANICI GIDA ADI VE KALORİSİNİ YAZMASI İÇİN İKİ ADET EDİTTEXT VE BUNLARIN KAYITI YAPLIABİLMESİ İÇİN BİR 
BUTTON TANIMLANMASI YAPILMIŞTIR.


---------------------------------------------------------------------------------------------------------------------------
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

//HEDEFEKLE.JAVA İSİMLİ SINIFIMIZIN LAYOUR XML KOD YAPISIDIR.
//TASARIMI RESMEDER.
//BURADA KULLANICILARIN HEDEF KAYITLARI OLUŞTURABİLMESİ İÇİN ÜÇ ADET TEXTVİEW, ÜÇ ADET EDİTTEXT, BİRADET BUTTON
 BULUNMAKTADIR.
//TEXTVİEW LER BİLGİ METNİ VERMEKTEDİR.
//EDİTTEXT LER İLGİLİ BİLGİ METNİN ALTINDA NEYİN YAZILACAĞINI BELİRTEN BİR TEXT E SAHİP OLMAKLA KULLANICI İLGİLİ
HEDEFİ TUTARLAR.
//BUTTON BU EDİTTEXT LERDE BULUNAN VERİLERİ VERİTABANINA KAYDEDER.

---------------------------------------------------------------------------------------------------------------------------


FRAGMENT_NABİZ.XML
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

//DAHA TASARIM AŞAMASINDA OLMAKTADIR.
---------------------------------------------------------------------------------------------------------------------------

FRAGMENT_SAGLİKHESAPLA.XML

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

//SAGLİKHESAPLAFRAGMENT.JAVA SINFIMIZIN LAYOUT XML KOD YAPISIDIR.TASARIM BARINDIRIR.
//BURADA BEŞ ADET TEXTVİEW , ÜÇ ADET EDİTTEXT , BİR ADET BUTTON BULUNMAKTADIR.
//TEXTVİER1 VE TEXTVİER2 İD SİNE SAHİP TEXTVİERLAR EDİTTEXTLERDEN GELEN VERİLERİN HESAPLANMASI SONUCU YORUMLAR
BARINDIRIRLAR.
//BUTTON BİZE HEM HESAPLAMALAR YAPAR DAHA SONRA VÜCUT KÜTLE ENDEKSİMİZİ HESAPLADIKTAN SONRA BUNU KAYDEDER.
//KULLANICI VERİLERİNİ İLGİLİ EDİTTEXTLERE GİRER.
---------------------------------------------------------------------------------------------------------------------------
LAYOUT_NAVİGATİON_HEDER.XML

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
//BU KOD BİZİM PANELDE AÇILAN KISIMDA BİR TASARIMDIR.
----------------------------------------------------------------------------------------------------------------------------
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">


            <item android:id="@+id/birinci"
                android:title="@string/menu"
                android:icon="@drawable/ic_home_black_24dp"
                ></item>

            <item android:id="@+id/ikinci"
                android:title="@string/create_food"
                android:icon="@drawable/add"
                ></item>
            <item android:id="@+id/üçüncü"
                android:title="@string/day"
                android:icon="@drawable/dayly"
                ></item>
            <item android:id="@+id/dördüncü"
                android:title="@string/pulse"
                android:icon="@drawable/nabiz"
                ></item>
            <item android:id="@+id/beşinci"
                android:title="@string/reminders"
                android:icon="@drawable/bildirim"
                ></item>
            <item android:id="@+id/altıncı"
                  android:title="@string/calculate_health"
                android:icon="@drawable/saglik_hesaplama"
                ></item>
            <item android:id="@+id/yedinci"
                android:title="@string/step_counter"

                android:icon="@drawable/adim_"></item>
    <item android:id="@+id/sekizinci"
        android:title="@string/searc_gıda"

        android:icon="@drawable/resim"></item>
    <item android:id="@+id/dokuzuncu"
        android:title="@string/hedef"

        android:icon="@drawable/tick"></item>






</menu>

//MENU KALSÖRÜMÜZÜN ALTINDA BULUNAN PANELDEKİ MENÜLERİMİZİ BELİRLEDİĞİMİZİ PANELLER VE İCONLARI BULUNYOR.
---------------------------------------------------------------------------------------------------------------------------





















































