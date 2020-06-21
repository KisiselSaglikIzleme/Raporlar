// APP İÇERİSİNE GOOGLE-SERVİCES.JSON(JSON.FİLE) EKLENMELİDİR.
----------------------------------------------------------------------
----------------------------------------------------------------------

BUİLD.GRADLE(:APP)
----------------------------------------------------------------------
apply plugin: 'com.google.gms.google-services'

depencies{
....
 implementation 'com.google.firebase:firebase-database:19.3.0'
    implementation 'com.google.firebase:firebase-messaging:20.2.0'
 implementation 'com.google.firebase:firebase-analytics:17.4.2'
    implementation 'com.google.firebase:firebase-auth:19.3.1'
  implementation 'com.firebaseui:firebase-ui-database:2.3.0'

//BUİLD.GRADLE(:APP) İÇERİSİNE YUKARIDAKİLER EKLENMELİDİR.
*****************************************************************************

BUİLD.GRADLE(SAGLİK)
---------------------------------------------------------------------------
buildscript {
    
    repositories {
        google()

....
dependencies {
        ...
        classpath 'com.google.gms:google-services:4.3.3'

....
allprojects {
    repositories {
        google()


//BUİLD.GRADLE(SAGLİK) İÇERİSİNE YUKARIDAKİLER EKLENMELİDİR.

