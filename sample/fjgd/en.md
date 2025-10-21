
# 福建广电PHP

````

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
$uas = parse_url(curl('http://portal.setvn.com:8080/PortalServer-App/new/aaa_aut	_aut002?pversion=1.3.2(32)&secondAuthid=&ptoken='.$ptoken.'&pserverAddress=portal.setvn.com&d=07543d06d77f6cf8&l='.$l.'&n='.$id.'&p=6&t='.$ptoken.'&u='.$user.'&v=2&ot=0&cid=4&pid=&pkv=&ptn=29tLmZqY20udHZob21Yl&hmac='.$hmac.'&timestamp='.$t.'&appId=FuJianShengWang&epgID=&nonce='.$nonce.'&ptype=6&puser='.$user.'&DRMtoken=&pappName=A1092E5E010194AF&plocation='.$l.'&authType=0&pserialNumber='.$ptoken.''));
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

```