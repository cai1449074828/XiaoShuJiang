# Post
## config
```
<?php
session_start();

mysql_connect('127.0.0.1', 'dbadmin', 'NsJidMFXg2QSS9uR');
mysql_select_db('caiLei');

mysql_query("set names 'utf8'");

//Home page file name
$url_home = 'index.php';

//Design Name
$design = 'default';
?>
```
## add
```
<?php
include('config.php')
?>
<?php
if($_POST['name']!=''&&$_POST['account']!=''&&$_POST['grade']!=''&&$_POST['password']!=''&&$_POST['college']!=''&&$_POST['zhuanye']!=''&&$_POST['id']!=''&&$_POST['phone']!='')
{
		$name=$_POST['name'];
		$account=$_POST['account'];
		$grade=$_POST['grade'];
		$college=$_POST['college'];
		$zhuanye=$_POST['zhuanye'];
		$id=$_POST['id'];
		$password=$_POST['password'];
		$phone=$_POST['phone'];
              
        if(mysql_query('insert into login(name,account,grade,college,zhuanye,id,password,phone) values ('.$name.',"'.$account.'","'.$grade.'","'.$college.'","'.$zhuanye.'","'.$id.'","'.$password.'","'.$phone.'")')){
            print("1");
		}
        else print("-1");
}
?>
```
## delete
```

```
## updata
```
<?php
include('config.php')
?>
<?php
if($_POST['name']!=''&&$_POST['account']!=''&&$_POST['grade']!=''&&$_POST['password']!=''&&$_POST['college']!=''&&$_POST['zhuanye']!=''&&$_POST['id']!='')
{
		$name=$_POST['name'];
		$account=$_POST['account'];
		$grade=$_POST['grade'];
		$college=$_POST['college'];
		$zhuanye=$_POST['zhuanye'];
		$id=$_POST['id'];
		$password=$_POST['password'];

        $sql=mysql_query("select * from login where account='$account'");
        $row=mysql_fetch_assoc($sql);
        if(!empty($row)){
	    	if($row['name']==$name&$row['grade']==$grade&
	    		$row['college']==$college&$row['zhuanye']==$zhuanye&
	    		$row['id']==$id) {
		    		if (mysql_query("update login set 
		                password = '$password' where account ='$account'"))print("1");
		            else print("未知错误!");
	   			}
	   		else print("0");
		}
		else{
			print("-1");
		}
}
?>
```
## query
```

<?php
include('config.php')
?>
<?php
if($_POST['account']!='')
{
		$account=$_POST['account'];
        $sql=mysql_query("select * from login where account='$account'");
        $row=mysql_fetch_assoc($sql);
        if(!empty($row)){
            print($row['plan']);
		}
		else{
			print("-1");
		}
}
?>
```
## 接收post媒体类型为:application/json的json数据
```
<?php
include('config.php')
?>
<?php
//媒体类型为:application/json接收json,$_POST接收为空
if($_POST!=null)
{
	print($_POST);
}
else{
//读取 POST 的原始数据。
	$json = file_get_contents("php://input");
    $data = json_decode($json, true);
    print($json);
}
?>
```
## 接收文件
```
<?php
include('config.php')
?>
<?php
//媒体类型为:application/json接收json,$_POST接收为空
$content = file_get_contents("php://input");

$imgName = time();
$file_dir="images/".$imgName.".png";

if($fp = fopen($file_dir,'w')){

if(fwrite($fp,$content)){
	print("上传图片成功");
fclose($fp);
}
}
?>
```
## php取出数据库数据封装为json并处理
```
<?php
include('config.php')
?>
<?php
if($_POST['account']!='')
{
		$account=$_POST['account'];
        $sql=mysql_query("select * from login where account='$account'");
        $sql2=mysql_query("select * from login where account!='$account'");
        $row=mysql_fetch_assoc($sql);
        if(!empty($row)){
        	print("[");
            $plan_json1=json_decode($row['plan'],TRUE);
        	$xiangsi_zong=count($plan_json1)+1;
      		$index_sql2=0;
        	while($row2=mysql_fetch_assoc($sql2)){
             	$plan_json2=json_decode($row2['plan'],TRUE);

        		$zhuanye_xiangtong="0";
        		$xiangsi=0;
        		if($row['zhuanye']==$row2['zhuanye']){
        			$xiangsi++;
        			$zhuanye_xiangtong="1";
        		}
        		$ii=0;
				for ($i=0; $i < count($plan_json1); $i++){ 
				      for ($j=0; $j < count($plan_json2); $j++) { 
				        		if($plan_json1[$i]['number']==$plan_json2[$j]['number']){
				        			$xiangsi++;
				        			$plan_xiangtong[$ii++]=$plan_json1[$i]['name'];
				        		}
				        	}
				    }
				 $xiangsudu=$xiangsi/$xiangsi_zong;
				print("{");
				print("\"name\":");
				print("\"");
				print($row2['name']);
				print("\"");
				print(",");
				print("\"phone\":");
				print("\"");
				print($row2['phone']);
				print("\"");
				print(",");
				print("\"xiangsidu\":");
				print("\"");
				print($xiangsudu);
				print("\"");
				print(",");
				print("\"zhuanye_xiangtong\":");
				print("\"");
				print($zhuanye_xiangtong);
				print("\"");
				print(",");
				print("\"plan_xiangtong\":");
				print("[");
				for ($i=0; $i <count($plan_xiangtong); $i++) { 
					print("\"");
					print($plan_xiangtong[$i]);
					print("\"");
					if($i!=count($plan_xiangtong)-1)print(",");
				}
				print("]");
				print("}");
				if ($index_sql2++!=mysql_num_rows($sql2)-1)print(",");
        		echo "\n";
        	}
        	print("]");
		}
		else{
			print("-1");
		}
}
?>

```