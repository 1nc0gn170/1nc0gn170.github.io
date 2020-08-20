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
