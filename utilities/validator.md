# Validator

The **Validator** class is used to validate the format or contents of any variable (string, number, array, etc).

```
$validator = new Validator($value);
// or
Validator::for($value)

if (Validator::for($password)
    ->isString()
    ->minLength(5)
    ->hasUppercase()
    ->hasLowercase()
    ->hasSpecialChars()
    ->validate())  {
    // Password is valid
}

if (Validator::for($email)
    ->isEmail()
    ->validate())  {
    // Email is valid
}
```

See the following list with all possible methods in the validator:

| Method                 | Description                                                       | Parameters      |
| ---------------------- | ----------------------------------------------------------------- | --------------- |
| isString()             | Check if it's text                                                |                 |
| is( $val )             | If it's exactly (===) that value                                  | mixed $val      |
| isNot( $val )          | If it's not (!==) that value                                      | mixed $val      |
| typeIs( $type )        | Check the type                                                    | string $type    |
| typeIsNot( $type )     | Check if the type is not                                          | string $type    |
| contains( $search )    | Valid both for strings and arrays. Check if $search exists in it. | mixed $search   |
| minLength( $length )   | Check minimum length/size of a string or array                    | int $length     |
| maxLength( $length )   | Check maximum length/size of a string or array                    | int $length     |
| isEmail( )             | Check if string is a valid email                                  |                 |
| isUppercase()          | Check if all letters are uppercase                                |                 |
| isLowercase()          | Check if all letters are lowercase                                |                 |
| hasLowercase($n?)      | Check if string has at least $n lowercase letters                 | int $n = 1      |
| hasUppercase($n?)      | Check if string has at least $n uppercase letters                 | int $n = 1      |
| hasNotUppercase()      | Check if string has not any uppercase letter                      |                 |
| hasNotLowercase()      | Check if string has not any lowercase letter                      |                 |
| isNumber()             | Check if value is a number or a string valid number               |                 |
| hasNumbers($n?)        | Check if string has at least $n numeric characters                | int $n = 1      |
| hasNotNumbers()        | Check if string has not any number                                |                 |
| isLetters()            | Check if string is composed only of letters                       |                 |
| hasLetters($n?)        | Check if string has at least $n letters                           | int $n = 1      |
| hasNotLetters()        | Check if string has not any letter                                |                 |
| isSpecialChars()       | Check if string is composed only of special chahracters           |                 |
| hasSpecialChars( $n? ) | Check if string has at least $n special characters.               | int $n = 1      |
| hasNotSpecialChars()   | Check if string doesn't have any special character                |                 |
| isPhone()              | Check if string has only valid characters for phone numbers.      |                 |
| isBool()               | Check if variable is a boolean                                    |                 |
| has( $prop )           | Check if array or object has this key/property                    | mixed $property |
| notEmpty( $prop )      | Check if array or object has this key, and the value is not empty | mixed $property |
