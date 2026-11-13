$path = "C:\path\credential_file"
$bytes = [System.IO.File]::ReadAllBytes($path)
$chunkSize = 256

for ($i = 0; $i -lt $bytes.Length; $i += $chunkSize) {
    $length = [Math]::Min($chunkSize, $bytes.Length - $i)
    $hex = [BitConverter]::ToString($bytes, $i, $length).Replace("-", "")

    Write-Output ("Offset 0x{0:X4}: {1}" -f $i, $hex)
}
