<?php 

if( isset( $_GET['Login'] ) ) { 

    $user = $_GET['username']; 
     
    $pass = $_GET['password']; 
    $pass = md5($pass); 

    $qry = "SELECT * FROM `users` WHERE user='$user' AND password='$pass';"; 
    $result = mysql_query( $qry ) or die( '<pre>' . mysql_error() . '</pre>' ); 

    if( $result && mysql_num_rows( $result ) == 1 ) { 
        // Get users details 
        $i=0; // Bug fix. 
        $avatar = mysql_result( $result, $i, "avatar" ); 

        // Login Successful 
        echo "<p>Welcome to the password protected area " . $user . "</p>"; 
        echo '<img src="' . $avatar . '" />'; 
    } else { 
        //Login failed 
        echo "<pre><br>Username and/or password incorrect.</pre>"; 
    } 

    mysql_close(); 
} 

?>

______

<?php 

if( isset( $_POST[ 'submit' ] ) ) { 

    $target = $_REQUEST[ 'ip' ]; 

    // Determine OS and execute the ping command. 
    if (stristr(php_uname('s'), 'Windows NT')) {  
     
        $cmd = shell_exec( 'ping  ' . $target ); 
        echo '<pre>'.$cmd.'</pre>'; 
         
    } else {  
     
        $cmd = shell_exec( 'ping  -c 3 ' . $target ); 
        echo '<pre>'.$cmd.'</pre>'; 
         
    } 
     
} 
?>

________

<?php     

if (isset($_GET['Submit'])) { 
     
    // Retrieve data 
     
    $id = $_GET['id']; 

    $getid = "SELECT first_name, last_name FROM users WHERE user_id = '$id'"; 
    $result = mysql_query($getid); // Removed 'or die' to suppres mysql errors 

    $num = @mysql_numrows($result); // The '@' character suppresses errors making the injection 'blind'

    $i = 0; 

    while ($i < $num) { 

        $first = mysql_result($result,$i,"first_name"); 
        $last = mysql_result($result,$i,"last_name"); 
         
        echo '<pre>'; 
        echo 'ID: ' . $id . '<br>First name: ' . $first . '<br>Surname: ' . $last; 
        echo '</pre>'; 

        $i++; 
    } 
} 
?>

____

<?php 
    if (isset($_POST['Upload'])) { 

            $target_path = DVWA_WEB_PAGE_TO_ROOT."hackable/uploads/"; 
            $target_path = $target_path . basename( $_FILES['uploaded']['name']); 

            if(!move_uploaded_file($_FILES['uploaded']['tmp_name'], $target_path)) { 
                 
                echo '<pre>'; 
                echo 'Your image was not uploaded.'; 
                echo '</pre>'; 
                 
              } else { 
             
                echo '<pre>'; 
                echo $target_path . ' succesfully uploaded!'; 
                echo '</pre>'; 
                 
            } 

        } 
?>

_____

<?php 

if(!array_key_exists ("name", $_GET) || $_GET['name'] == NULL || $_GET['name'] == ''){ 

 $isempty = true; 

} else { 
         
 echo '<pre>'; 
 echo 'Hello ' . $_GET['name']; 
 echo '</pre>'; 
     
}

?>
