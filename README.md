# online-exam
php and html code for online examination
php and html code for online exam system

Below is the sample code for an online exam system using PHP and HTML. This is just a basic structure and can be modified as per the specific requirements and functionalities needed.

index.php (homepage)
```
<!DOCTYPE html>
<html>
<head>
	<title>Online Exam System</title>
</head>
<body>
	<h1>Welcome to Online Exam System</h1>
	<form method="post" action="exam.php">
		<label for="username">Username:</label>
		<input type="text" name="username" id="username">
		<label for="password">Password:</label>
		<input type="password" name="password" id="password">
		<input type="submit" name="login" value="Login">
	</form>
</body>
</html>
```

exam.php (main exam page)
```
<?php
session_start();
//check if user is logged in
if(!isset($_SESSION['username'])){
	header("Location: index.php");
	exit;
}

//get questions from database or file
$questions = array(
			1 => array(
				'question' => 'What is the capital of France?',
				'choices' => array(
						'1' => 'Paris',
						'2' => 'London',
						'3' => 'Berlin'
				),
				'answer' => '1'
			),
			2 => array(
				'question' => 'Who is the first president of the United States?',
				'choices' => array(
						'1' => 'John Adams',
						'2' => 'George Washington',
						'3' => 'Thomas Jefferson'
				),
				'answer' => '2'
			)
		);

//check if user submitted the exam	
if(isset($_POST['submit'])){
	//get user's answers
	$user_answers = $_POST['answers'];

	//calculate marks
	$marks = 0;
	foreach ($user_answers as $q_no => $answer) {
		if($questions[$q_no]['answer'] == $answer){
			$marks++;
		}
	}

	//save marks in session
	$_SESSION['marks'] = $marks;

	//redirect to result page
	header("Location: result.php");
	exit;
}
?>
<!DOCTYPE html>
<html>
<head>
	<title>Online Exam</title>
</head>
<body>
	<h1>Online Exam</h1>
	<form method="post" action="">
		<?php foreach ($questions as $q_no => $q) { ?>
		<p><?php echo $q_no . '. ' . $q['question'];?></p>
		<?php 
		foreach ($q['choices'] as $key => $choice) { ?>
		<input type="radio" name="answers[<?php echo $q_no;?>]" value="<?php echo $key;?>"> <?php echo $choice;?><br>
		<?php } ?>
		<br>
		<?php } ?>
		<input type="submit" name="submit" value="Submit">
	</form>
</body>
</html>
```

result.php (result page)
```
<?php
session_start();
//check if user is logged in
if(!isset($_SESSION['username'])){
	header("Location: index.php");
	exit;
}

//get marks
$marks = $_SESSION['marks'];
?>
<!DOCTYPE html>
<html>
<head>
	<title>Result</title>
</head>
<body>
	<h1>Result</h1>
	<p>Your marks: <?php echo $marks;?></p>
	<a href="index.php">Logout</a>
</body>
</html>
```

Note: This is just a basic structure. Additional functionalities such as storing user's information, timer limit, multiple exam categories, etc. can be added as required. Also, make sure to validate and sanitize user inputs for security purposes. 
source : <a href="https://www.tnpscgroup4.in/online-test.html">TNPSC Group 4 online test</a>
