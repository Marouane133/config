$hex = (Get-Content ".\hex.txt" -Raw).Trim()
$chunkSize = [int][Math]::Ceiling($hex.Length / 10)

New-Item -ItemType Directory -Path ".\hex_chunks" -Force | Out-Null

for ($i = 0; $i -lt $hex.Length; $i += $chunkSize) {
    $length = [Math]::Min($chunkSize, $hex.Length - $i)
    $chunk = $hex.Substring($i, $length)

    $filename = ".\hex_chunks\chunk_{0:D3}.txt" -f [int]($i / $chunkSize)
    Set-Content -Path $filename -Value $chunk
}
