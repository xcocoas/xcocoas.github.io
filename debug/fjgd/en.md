
# <span class="color-white">福建广电PHP</span>

### <span class="color-white">源码</span>

<div class="color-orange">

	<?php

	$id = isset($_GET['id']) ? $_GET['id'] : 'cctv1hd_2000';

	// 从抓包中获取
	$user = 'freeuser';
	$ptoken = '...';
	$l = '...';

	$t = time();
	$nonce = rand(100000,999999);
	$str = 'sumasalt-app-portalpVW4U*FlS'.$t.$nonce.$user;
	$hmac = substr(sha1($str),0,10);
	$uas = parse_url(curl('http://portal.setvn.com:8080/PortalServer-App/new/aaa_aut_aut002?pversion=1.3.2(32)&secondAuthid=&ptoken='.$ptoken.'&pserverAddress=portal.setvn.com&d=07543d06d77f6cf8&l='.$l.'&n='.$id.'&p=6&t='.$ptoken.'&u='.$user.'&v=2&ot=0&cid=4&pid=&pkv=&ptn=29tLmZqY20udHZob21Yl&hmac='.$hmac.'&timestamp='.$t.'&appId=FuJianShengWang&epgID=&nonce='.$nonce.'&ptype=6&puser='.$user.'&DRMtoken=&pappName=A1092E5E010194AF&plocation='.$l.'&authType=0&pserialNumber='.$ptoken.''));
	parse_str($uas["query"],$a);
	$token = "ptype=".$a['ptype']."&plocation=".$a['plocation']."&puser=".$a['puser']."&ptoken=".$a['ptoken']."&ot=".$a['ot']."&d=".$a['d']."&l=".$a['l']."&pid=&cid=".$a['cid']."&v=".$a['v']."&u=".$a['u']."&t=".$a['t']."&p=".$a['p']."&sid=".$a['sid']."&r=".$a['r']."&e=".$a['e']."&nc=".$a['nc']."&a=".$a['a'];
	$m3u8 = "http://gslb.aj.setvn.com:8070/live/".$id.".m3u8?".$token;
	header('Location: ' . $m3u8);

	function curl($url) {
		$curl = curl_init($url);
		curl_setopt($curl, CURLOPT_SSL_VERIFYPEER, false);
		curl_setopt($curl, CURLOPT_SSL_VERIFYHOST, false);
		curl_setopt($curl, CURLOPT_RETURNTRANSFER, 1);
		$data = curl_exec($curl);
		curl_close($curl);
		return $data;
	}

	?>

</div>

### <span class="color-white">参数</span>

<div class="color-yellow">
	更换`$ptoken`和`$l`即可
</div>

### <span class="color-white">ID对照表</span>

<div class="color-green">

	CCTV央视
	'cctv1hd_2000',		//CCTV-1高清
	'cctv2hd_2000',		//CCTV-2高清
	'cctv3hd_2000',		//CCTV-3高清
	'cctv4hd_2000', 	//CCTV-4高清
	'cctv5hd_2000', 	//CCTV-5高清
	'cctv5plushd_2000', //CCTV-5+高清
	'cctv6hd_2000', 	//CCTV-6高清
	'cctv7hd_2000', 	//CCTV-7高清
	'cctv8hd_2000', 	//CCTV-8高清
	'cctv9hd_2000', 	//CCTV-9高清
	'cctv10_1200', 		//CCTV-10高清
	'cctv11hd_2000',	//CCTV-11高清
	'cctv12hd_2000', 	//CCTV-12高清
	'cctv13_1200', 		//CCTV-13高清
	'cctv14_2000', 		//CCTV-14高清
	'cctv15_2000', 		//CCTV-15高清
	'cctv16hd_2000', 	//CCTV-16高清
	'cctv17_2000', 		//CCTV-17高清

	WS卫视
	'bjwshd_2000', 	//北京卫视高清
	'dfwshd_2000', 	//东方卫视高清
	'tjwshd_2000', 	//天津卫视高清
	'hljwshd_2000', //黑龙江卫视高清
	'lnwshd_2000', 	//辽宁卫视高清
	'sdwshd_2000', 	//山东卫视高清
	'ahwshd_2000', 	//安徽卫视高清
	'hbwshd_2000', 	//湖北卫视高清
	'hnwshd_2000', 	//湖南卫视高清
	'jxwshd_2000', 	//江西卫视高清
	'jswshd_2000', 	//江苏卫视高清
	'zjwshd_2000',	//浙江卫视高清
	'dnwshd_2000',	//东南卫视高清
	'xm1_1200', 	//厦门卫视
	'gdwshd_2000',	//广东卫视高清
	'szwshd_2000',	//深圳卫视高清
	'gzwshd_2000',	//贵州卫视高清
	'ssws_1200',	//三沙卫视

	FJ福建
	'dspd_1200',	//福建导视
	'fj1hd_2000',	//福建综合高清
	'fjxwhd_2000',	//福建新闻高清
	'fjdsjhd_2000',	//福建电视剧高清
	'zz1_1200',		//漳州1套
	'zz2hd_2000',	//漳州2套高清
	'xm1hd_2000',	//厦视-1高清
	'xm2hd_2000',	//厦视-2高清
	'xm3hd_2000',	//厦视-3高清
	'qz1_1200',		//泉州1套
	'qz2hd_2000',	//泉州2套高清
	'qz3hd_2000',	//泉州3套高清
	'qz4hd_2000',	//泉州4套高清
	'fz1hd_2000',	//福州1套高清
	'fz2hd_2000',	//福州2套高清
	'fz3hd_2000',	//福州3套高清
	'fz4hd_2000',	//福州4套高清
	'ptan1_1200',	//平潭1套
	'ptian1_1200',	//莆田1套
	'ptian2hd_2000',//莆田2套高清
	'nd1_1200',		//宁德1套
	'nd2hd_2000',	//宁德2套高清
	'np1_1200',		//南平1套
	'np2_1200',		//南平2套
	'sm1_1200',		//三明1套
	'ly1_1200',		//龙岩1套
	'jjdsthd_2000',	//晋江高清

	补充
	'jykthd_2000',	//金鹰卡通高清
	'fhzwhd_2000',	//凤凰中文高清
	'fhzxhd_2000',	//凤凰资讯高清
	'chchd_2000',	//CHC影迷电影
	'chchd_2000',	//CHC高清电影
	'chcdzhd_2000',	//CHC动作电影
	'chcjthd_2000',	//CHC家庭影院
</div>

