# Android-Facebook-Connection-Success

**Connection to Facebook**

Couple of notes:
- I have added the Facebook SDK manually but I believe you can add the SDK within the App build.gradle 

        compile 'com.facebook.android:facebook-android-sdk:4.0.0'

- Had issues with with Project build.gradle "top level build.gradle".  Had to change the classpath within the Project build.gradle in order to get it to work

        classpath 'com.android.tools.build:gradle:1.1.0'
        
        to
        
        classpath 'com.android.tools.build:gradle:1.0.0'

- **HashKey** It took me some time to get the HashKey.  I tried two different methods to get the HashKey:
  - **Terminal** was generating the wrong HashKey.  I posted to [stackoverflow HashKey Question](http://stackoverflow.com/questions/29612943/getting-two-different-hashkeys-with-different-methods) to find the reason and I will update this when I get a working result.
  - **Within the application**  I created an Activity and retured the working HashKey trough the LogCat. 
	
    	   public class GetHashKey extends ActionBarActivity {

			@Override
			protected void onCreate(Bundle savedInstanceState) {
				super.onCreate(savedInstanceState);
				setContentView(R.layout.activity_get_hash_key);
				try {
					PackageInfo info = getPackageManager().getPackageInfo(getPackageName(), PackageManager.GET_SIGNATURES);
					for (Signature signature : info.signatures) {
						MessageDigest md;

						md = MessageDigest.getInstance("SHA");
						md.update(signature.toByteArray());
						String something = new String(Base64.encode(md.digest(), 0));
						Log.e("hash key", something);
					}
				} catch (Exception e1) {
					// TODO Auto-generated catch block
					Log.e("name not found", e1.toString());
				}
			}
           }

- I used Facebook's working example.  You can click the link below to download their SDK and the sample project.  
  - https://developers.facebook.com/resources/facebook-android-sdk-current.zip
  - The working example **HelloFacebookSample** can be located at:
path\Downloads\facebook-android-sdk-4.0.1.zip\facebook-android-sdk-4.0.1\samples\HelloFacebookSample 
