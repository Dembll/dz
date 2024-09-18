#Task 1
import re

def find_RbR_fragments(text):
    pattern = r'[Rr][Bb]+[Rr]'
    return re.findall(pattern, text)

print(find_RbR_fragments("RbR rBr RBBR RbbbR rbbbR"))

#Task 2
import re

def validate_card_number(card_number):
    return bool(re.fullmatch(r'\d{4}(-\d{4}){3}', card_number))

print(validate_card_number("1234-5678-1234-5678"))
print(validate_card_number("1234-5678-1234-567"))

#Task 3
import re

def validate_email(email):
    pattern = r'^[a-zA-Z0-9]+[a-zA-Z0-9_-]*[a-zA-Z0-9]+@[a-zA-Z]+\.[a-zA-Z]{2,}$'
    return bool(re.fullmatch(pattern, email))

print(validate_email("example_email@domain.com"))
print(validate_email("_invalid@domain.com"))
print(validate_email("valid-email@domain.com"))

#Task 4
import re

def validate_login(login):
    return bool(re.fullmatch(r'[a-zA-Z0-9]{2,10}', login))

print(validate_login("user123"))
print(validate_login("1"))
print(validate_login("validlogin"))
