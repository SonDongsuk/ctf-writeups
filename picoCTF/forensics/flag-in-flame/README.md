
# Flag in Flame

## Problem Situation

Inside the file, there is an encoded text block instead of a typical log format. Find the hidden information inside the log file.

## Solution Approach

After checking **logs.txt**, there was a long string block that did not match a typical log format but appeared to be base64.

Since base64 is commonly used to represent binary data as text, decoding it could restore the original file (such as an image).

Therefore, base64 decoding was performed to convert it into an image file.

After checking the decoded file type, it was identified as a PNG file and opened.

The string at the bottom of the image consisted only of **0-9 and A-F (uppercase)**, which matches the hexadecimal format.  
Therefore, a **hex → ASCII conversion** was performed.

As a result, the final flag was obtained.

cat logs.txt
base64 -d logs.txt > output
file outupt
xdg-open output
echo "7069636F..." | xxd -r -p

## Reason for identifying Base64

The string in **logs.txt** consisted of characters **A–Z, a–z, 0–9, +, /** and its length was a multiple of 4, which is a typical pattern of base64 encoding.

## Answer
picoCTF{forensics_analysis_is_amazing_5daa4a2f}
