# Encrypt Zeppelin Credentials with Shiro

1. Download the Shiro Tools Hasher from Maven
  - https://repo1.maven.org/maven2/org/apache/shiro/tools/shiro-tools-hasher/

2. Run the following commands to download dependencies
```
$ mvn dependency:get -DgroupId=org.apache.shiro.tools -DartifactId=shiro-tools-hasher -Dclassifier=cli -Dversion=X.X.X
```

3. Once you have access to the jar, you can run the following command:
```
$ java -jar shiro-tools-hasher-X.X.X-cli.jar -p
```
4. Add password that you need to hash
```
Password to hash:
Password to hash (confirm):
```
5. When this command executes, it will print out the securely-salted-iterated-and-hashed password. For example:
```
$shiro1$SHA-256$500000$eWpVX2tGX7WCP2J+jMCNqw==$it/NRclMOHrfOvhAEFZ0mxIZRdbcfqIBdwdwdDXW2dM=
```
6. Take this value and place it in the Zeppelin shiro.ini configuration
```
[users]
user1 = $shiro1$SHA-256$500000$eWpVX2tGX7WCP2J+jMCNqw==$it/NRclMOHrfOvhAEFZ0mxIZRdbcfqIBdwdwdDXW2dM=
```
  And in the [main] section
```
[main]
passwordMatcher = org.apache.shiro.authc.credential.PasswordMatcher
iniRealm.credentialsMatcher = $passwordMatcher
```

- Tutorial: https://shiro.apache.org/command-line-hasher.html
