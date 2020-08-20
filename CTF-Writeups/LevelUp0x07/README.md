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
### Level-3

```
ExifTool Version Number         : 11.16
File Name                       : chall.png
Directory                       : .
File Size                       : 63 kB
File Modification Date/Time     : 2020:08:13 04:03:45+05:30
File Access Date/Time           : 2020:08:16 20:28:19+05:30
File Inode Change Date/Time     : 2020:08:16 20:28:15+05:30
File Permissions                : rw-r--r--
File Type                       : PNG
File Type Extension             : png
MIME Type                       : image/png
Image Width                     : 228
Image Height                    : 152
Bit Depth                       : 8
Color Type                      : RGB
Compression                     : Deflate/Inflate
Filter                          : Adaptive
Interlace                       : Noninterlaced
SRGB Rendering                  : Relative Colorimetric
Pixels Per Unit X               : 2835
Pixels Per Unit Y               : 2835
Pixel Units                     : meters
Exif Byte Order                 : Big-endian (Motorola, MM)
Resolution Unit                 : inches
Y Cb Cr Positioning             : Centered
Exif Version                    : 0231
Components Configuration        : Y, Cb, Cr, -
User Comment                    : FLAG{e8606532b027bfd324ea31d1b4f116c2}
Flashpix Version                : 0100
GPS Latitude Ref                : North
GPS Longitude Ref               : West
GPS Latitude                    : 37 deg 43' 58.53" N
GPS Longitude                   : 122 deg 30' 8.48" W
GPS Position                    : 37 deg 43' 58.53" N, 122 deg 30' 8.48" W
Image Size                      : 228x152
Megapixels                      : 0.035
```
### Level-4 

```
Password Reset Functionality
Our self-reset password functionality is currently down. Please use the following temporary password to login: 9a76a913ee9ae8d5b2
```

```
> python icmp-listener.py
Waiting for pings...


agent
ive noticed
obelisk hides
missions
in images
check out
the
target list
secret is
pwn4llthebugz
FLAG{f514875849460428b4dc40dd72a5a29a}

Learn how to exfiltrate data via ping in a realistic situation: https://www.bengrewell.com/2019/01/01/slipping-out-through-the-front-door
```
### Level-5

```
Dear agent_521bcd5,

As ordered by Matriarch, I have created a backdoor console that will allow us to launch WannaSpy when time is right.

We're not worried about anyone getting in since they have to go through many doors to actually get in.

Once you are ready, you will find that the console lives on 3389.

FLAG{f0dee25f617e2cb820b9b44fcdf90ed8}

Regards
agent_1337

```
