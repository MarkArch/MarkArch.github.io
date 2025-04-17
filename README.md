Foreach($dc in Get-Content DC.txt){
 $dc = $dc.trim()
 $domain = $dc.split('.')[1..($dc.Length-1)] -join '.';
 Write-Host -NoNewline $dc;
 Write-Host -NoNewline ": ";
 $ldapsearchbase = 'CN=Directory Service,CN=Windows NT,CN=Services,CN=Configuration' + ',DC=' + ($domain.split('.') -join ',DC=')
 $check=(Get-ADObject -Server $dc $ldapsearchbase -Properties dsheuristics).dsheuristics | ft
 if ([string]::IsNullOrEmpty($check)) {
     Write-Host "dsheuristics attribute is at its default value (not explicitly set)."
 } else {
     Write-Host "dsheuristics attribute is explicitly set to: $ds"
 }
}
