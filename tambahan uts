<?php
session_start();

if (!isset($_SESSION['username'])) {
    header("Location: login.php");
    exit;
}

$host = "localhost";
$user = "root";
$pass = "";
$dbname = "login_count"; 

$conn = new mysqli($host, $user, $pass, $dbname);
if ($conn->connect_error) {
    die("Koneksi gagal: " . $conn->connect_error);
}

$username = $_SESSION['username'];


$sql = "SELECT login_count FROM users WHERE username = ?";
$stmt = $conn->prepare($sql);
$stmt->bind_param("s", $username);
$stmt->execute();
$stmt->bind_result($login_count);
$stmt->fetch();
$stmt->close();


$login_count++;


$update = $conn->prepare("UPDATE users SET login_count = ? WHERE username = ?");
$update->bind_param("is", $login_count, $username);
$update->execute();
$update->close();
$conn->close();
?>

<html>
<head>
    <title>::Login Page::</title>
    <style type="text/css">
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            font-family: Arial, sans-serif;
        }
        h1 {
            font-size: 24px;
        }
    </style>
</head>
<body>
    <h1><?php echo "Selamat datang " . htmlspecialchars($username) . " Ke-" . $login_count; ?></h1>
</body>
</html>
