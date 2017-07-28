```
package mx.paracrecer.posttojson1;

import android.os.AsyncTask;
import android.os.Bundle;
import android.os.Debug;
import android.support.v7.app.AppCompatActivity;
import android.util.JsonReader;
import android.util.Log;
import android.view.View;
import android.widget.Button;

import org.json.JSONException;
import org.json.JSONObject;

import java.io.BufferedInputStream;
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.OutputStream;
import java.io.OutputStreamWriter;
import java.io.UnsupportedEncodingException;
import java.net.HttpURLConnection;
import java.net.MalformedURLException;
import java.net.URL;
import java.net.URLEncoder;
import java.util.HashMap;
import java.util.Map;

import javax.net.ssl.HttpsURLConnection;


public class MainActivity extends AppCompatActivity {

    Button boton;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        boton = (Button)findViewById(R.id.button);
        boton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {

                Log.d("A:", "kha");
                /*JSONObject jo = new JSONObject();

                try {
                    jo.put("first", 1);
                    jo.put("second", 2);
                } catch (JSONException e) {
                    e.printStackTrace();
                    Log.d("ERROR", "Valio barriga");
                }*/


                AsyncTask.execute(new Runnable() {
                    @Override
                    public void run() {
                        // All your networking logic
                        // should be here

                        /*
                        HashMap<String, Integer> map = new HashMap<String, Integer>();
                        map.put("Color1",1);
                        map.put("Color2",2);
                        */

                        //String url = "http://165.227.2.102:41062/www/probandoJSON.php";
                        String stringUrl = "https://pcubicacion.firebaseio.com/usuarios.json";

                        //enviarServdor(url, map);


                        try {
                            URL url = new URL(stringUrl);
                            HttpURLConnection urlConnection = (HttpURLConnection) url.openConnection();
                            //InputStream in = new BufferedInputStream(urlConnection.getInputStream());
                            //Log.d("seee", in.toString());

                            //InputStreamReader in = new InputStreamReader(urlConnection.getInputStream(), "UTF-8");
                            BufferedReader streamReader = new BufferedReader(new InputStreamReader(urlConnection.getInputStream(), "UTF-8"));
                            StringBuilder responseStrBuilder = new StringBuilder();

                            String inputStr;
                            while ((inputStr = streamReader.readLine()) != null)
                                responseStrBuilder.append(inputStr);
                                Log.d("json..: ", responseStrBuilder.toString());
                            new JSONObject(responseStrBuilder.toString());



                        } catch (IOException e) {
                            Log.d("","");
                        } catch (JSONException e) {
                            e.printStackTrace();
                        }


                    }
                });




            }


        });
    }

    private void enviarServdor(String url, HashMap<String, Integer> map){

        Log.d("A: ", "Llega a A");
        try {
            Log.d("URL: ", "Llega a URL");
            // Create URL
            URL endpoint = new URL(url);

            Log.d("CON: ", "Llega a CON");
            // Create connection
            HttpURLConnection myConnection = (HttpURLConnection) endpoint.openConnection();

            Log.d("HEAD: ", "Llega a HEAD");
            // Headers
            //myConnection.setRequestProperty("Content-Type", "application/json");

            Log.d("STREAM: ", "Llega a STREAM");

            //InputStream in = new BufferedInputStream(myConnection.getInputStream());
            InputStreamReader in = new InputStreamReader(myConnection.getInputStream());
            Log.d("RETURN: ", in.toString());

            JsonReader jsonReader = new JsonReader(in);
            Log.d("JSON", String.valueOf(jsonReader));

            } catch (MalformedURLException e) {
                Log.d("CATCH: ", "1");
                e.printStackTrace();

        } catch (IOException e) {
            Log.d("CATCH: ", "2");
            e.printStackTrace();
        }

    }


}

```