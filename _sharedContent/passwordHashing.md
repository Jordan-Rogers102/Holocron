# What is Password Hashing

Password hashing is used to store a password in the database without actually storing the password. The password is taken by the website or application, hashed and the hash is stored in the database. Therefore if anyone read the database, they wouldn't know the original file.

When users log in, their password is checked against the hashed password by running it through the same algorithm to see if it matches.

[https://youtu.be/cczlpiiu42M](https://youtu.be/cczlpiiu42M)

## Summary

![passwordHashing](_sharedContent/_images/passwordHashing.png)

# Security Concerns

Storing passwords in databases without being hashed is a serious security concern. It means that employees or hackers can read the database and are then able to log into the database as any user they wish.

[**https://hub.packtpub.com/g-suite-administrators-passwords-were-unhashed-for-14-years-notifies-google/?fbclid=IwAR1Ei98rlPM0Rlk6rH9Wq-7oK1hOkTVmfpLbTfRbA3IMBUrKyl4aCnCi8Vk**](https://www.google.com/url?q=https%3A%2F%2Fhub.packtpub.com%2Fg-suite-administrators-passwords-were-unhashed-for-14-years-notifies-google%2F%3Ffbclid%3DIwAR1Ei98rlPM0Rlk6rH9Wq-7oK1hOkTVmfpLbTfRbA3IMBUrKyl4aCnCi8Vk&sa=D&sntz=1&usg=AOvVaw2UaSfbXsq8QJinPA3x_a5W)