``• comando importante para obtener todos .txt de un Path: ChildItem -Path C:\Users -Recurse -Filter "*.txt" (Para que no muestre los errores) -Recurse -ErrorAction SilentlyContinue
•`` Para buscar un fichero en CMD → where /R c:\ bash.exe   
• dir /r /s
```
Get-ChildItem -Path C:\ -Include *.kdbx -File -Recurse -ErrorAction SilentlyContinue
```