# FitokimiaUH
Hasil Open Recruitment 2018
<?php
	error_reporting(E_ALL ^ (E_NOTICE | E_WARNING));
// koneksi ke database

$connect = mysqli_connect("localhost","root","","db_mahasiswa");

// cek tombol submit sudahditekan atau belum
if(isset($_POST['submit'])){
	$query=$_POST['query'];
	$result = mysqli_query ($connect, "SELECT*FROM tb_hasil_oprec_fito WHERE NIM LIKE '".$query."' ");
}else{
	$result = mysqli_query ($connect, "SELECT*FROM tb_hasil_oprec_fito");
}


?>

<!DOCTYPE html>
<html>
<head>
	<title>Open Recruitment FITO</title>
</head>
<body>
	
	<div style="margin: 50px auto 0;width: 600px">
	<h1 style="color:green" font-size="200px" font-weight="bold">Open Recruitment Korps Asisten Fitokimia</h1><br>

	<form action="" method="POST" class="box" align="center">
		<input type="text" name="query" placeholder="Enter NIM without Spacing" autocomplete="off" />
		<button type="submit" name="submit" bgcolor="silver">Search</button>
	</form><br><br>


	<table border="1" width="500px" cellspacing="0" align="center">
		<tr style="font-weight:bold;" bgcolor="#33FFBE#33FFBE">
			<td align="center">NO</td>
			<td align="center">NIM</td>
			<td align="center">NAMA</td>
			<td align="center">KETERANGAN</td>
		</tr>
		<?php
		$no = 1;

		$query = $_POST['query'];
		if($query != ''){
			$select = mysqli_query($connect, "SELECT * FROM tb_hasil_oprec_fito WHERE NIM LIKE '".$query."' ");
		}

		if(mysqli_num_rows($select)){
		while($baris = mysqli_fetch_array($select)){
		?>

		<tr>
			<td align="center"><?php echo $no++ ?></td>
			<td align="center"><?php echo $baris['NIM'] ?></td>
			<td align="center"><?php echo $baris['Nama'] ?></td>
			<td align="center" ><?php echo $baris['Keterangan'] ?></td>
		</tr>

		<?php }}else{
			echo '<tr><td colspan="4" align="center">Tidak Ada Data</td></tr>';
			} ?>
	</table><br>

	<foot>
	<p style="color:black; font-weight: bold" align="center">Korps Asisten Farmakognosi Fitokimia</p>
	</foot>
</body>
</html>
