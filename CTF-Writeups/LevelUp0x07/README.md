# LevelUp0x07

### Level-1
Hello Agent, as you may be aware Obelisk have been causing trouble all over the world. They've launched a world wide cyber attack using a new form of ransomware known as WannaSpy. This worm is designed to target hospital data and aims to delete all information related to COVID 19 worldwide in the next week. As such, the President has assigned this mission to the HACK agency.

We sent Agent Craigie out into the field to infiltrate Obelisk. They were able to plant a radio at the following endpoint: /radio, before we lost communication with them.

We need you to bypass their authentication and bring down their operation.

Good luck Agent.

Sincerely,

cje
Spymaster
HACK Agency


```

    Add secret backdoor to download app - who looks in JS files anyway?
    FLAG{REDATCTED}
  	function return_app_link() {
     var url = window.location.href;
	 if (url.searchParams.get('test')) {
     	document.location.href = "https://07.levelupctf.com/222228a4e79d33a299f5d/s3cretc0mmunications";
    	}
    }
```
### Level-2

```    
    <string name="encrypted_chat_key">8b0955d2682eb74347b9e71ea0558c67</string>
    <string name="flag">FLAG{a445c73c8cb97421d1923a8c51c221fd}</string>
```

##### _forgotPassword()_

```

    public void forgotPassword(View view) throws IOException {
        EditText username = (EditText) findViewById(R.id.username);
        if (username.getText() != null && !username.getText().toString().isEmpty()) {
            OkHttpClient webclient = new OkHttpClient();
            RequestBody post_body = new FormBody.Builder().add("username", username.getText().toString()).build();
            Request.Builder builder = new Request.Builder();
            webclient.newCall(builder.url(this.URL + "/d41d8cd98f00b204e9800998ecf8427e/8cd98f00b204e9800998/forgotpassword").post(post_body).build()).execute().code();
        }
    }
```
##### _encryptedChat()_

```
    public void encryptedChat() {
        String key = getApplicationContext().getString(R.string.encrypted_chat_key);
        new OkHttpClient();
        Request.Builder builder = new Request.Builder();
        Request build = builder.url(this.URL + "/fa694c73da13c94e49cc82b/06a28bdb78b6c02e16862a3/chat").header("3NCRYPT3D-CH4T", key).build();
    }
}
```
