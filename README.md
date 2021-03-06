# CI_throttle
Codeigniter Login Attempts Throttle

##Background
I was looking for a Codeigniter login throttling library and couldn't find a simple one to use, so I wrote one.

##How it works

* first clean up old logins
* Count matching IP address and type (optional, useful if more than one throttle type. IE: logins, submissions)
* Compare to limit
  * If over limit, show error 503
  * if not over, return number of attempts

##Usage
###install

put files into proper codeigniter directories
* MY_Model [https://github.com/avenirer/CodeIgniter-MY_Model](download from here. The file in the folder will not work.)
* Throttle_model
* Throttle library 
in correct locations (see file structure above)

###initialize
in your controller __construct() or in a function, call 
```PHP
$this->load->library('throttle');
```

###Use
```PHP
$attempts = $this->throttle(1); //run throttle check from throttle library, type 1
```
or
```PHP
$attempts = $this->throttle(5, 5, 60); //run throttle check from throttle library, type 5, limit 5 attempts every hour
```

##Requirements
CodeIgniter 2 or 3
MySQL database or equivalent
MY_Model from avenirer (find it on github. It's great.) or equivalent

database table called throttles with the following:
```
CREATE TABLE throttles
(
  id INT UNSIGNED PRIMARY KEY,
  ip VARCHAR(64),
  created_at DATETIME,
  updated_at DATETIME,
  type INT UNSIGNED
);
```
