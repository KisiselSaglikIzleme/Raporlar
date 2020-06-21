//SAĞLIK HESAPLA SAYFASINDA VÜCUT KİTLE ENDEKSİNİN HESAPLANMASI VE HESAPLANAN VÜCUT KİTLE ENDEKSİNİN GÖSTERİLMESİ

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

//ANASAYDA GÖSTERİLMESİ

public void onDataChange(@NonNull DataSnapshot dataSnapshot) {
                for(DataSnapshot ds:dataSnapshot.getChildren()){
                    String bki = ds.child("bki").getValue().toString();
                    bkilist.add(new BkiModel(bki));
                }
                CustomAdapterBki customAdapter= new CustomAdapterBki(getActivity(),bkilist);
                listviewbki.setAdapter(customAdapter);
                dbRef.removeEventListener(this);




