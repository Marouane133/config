$path = "C:\path\credential_file"
$bytes = [System.IO.File]::ReadAllBytes($path)
$chunkSize = 1152

New-Item -ItemType Directory -Path ".\hex_chunks" -Force | Out-Null

for ($i = 0; $i -lt $bytes.Length; $i += $chunkSize) {
    $length = [Math]::Min($chunkSize, $bytes.Length - $i)
    $hex = [BitConverter]::ToString($bytes, $i, $length).Replace("-", "")

    $filename = ".\hex_chunks\chunk_{0:D3}.txt" -f [int]($i / $chunkSize)
    Set-Content -Path $filename -Value $hex
}
