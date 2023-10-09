
HEX DECODE:

```
xxd -r -p COMMAND
```


BASE64 DECODE

```
1. Check if the string is coding using Base64 and decode it:

   1) Decode: echo "<<string>>" | base64 -d
   2) Successive decoding until it is not base64 -> SCRIPT:   base64_decode_successive.py
   
3. Code: echo "<<string>>" | base64
```

    Successive decoding until it is not base64 -> SCRIPT:   base64_decode_successive.py