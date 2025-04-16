$bytes = [System.IO.File]::ReadAllBytes("C:\Tools\tool.enc")
$pwd = "mypassword"

for ($i = 0; $i -lt $bytes.Length; $i++) {
    $bytes[$i] = $bytes[$i] -bxor [byte][char]$pwd[$i % $pwd.Length]
}

[System.IO.File]::WriteAllBytes("C:\Tools\tool_restored.exe", $bytes)
