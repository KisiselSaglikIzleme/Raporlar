//ANA MENÜDE AKTİF KULLANICI BULAMAZSA BİZİ MAİN ACTİVİTY YÖNLENDİRİR

public void init(){
        auth = FirebaseAuth.getInstance();
        currentUser = auth.getCurrentUser();

    }
@Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_ana);
        init();
@Override
    protected void onStart() {
        if (currentUser == null){
            Intent welcomeIntent = new Intent(Ana.this, MainActivity.class);
            startActivity(welcomeIntent);
            finish();
        }

        super.onStart();
    }
