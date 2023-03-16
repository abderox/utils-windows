@echo off

set port=%1

if not defined port (
  echo Port number not specified.
  goto :eof
)

echo Trying to find process using port %port%...

rem Find the PID 
for /f "tokens=5" %%a in ('netstat -ano ^| findstr ":%port%"') do set pid=%%a

if not defined pid (
  echo No process found using port %port%
) else (
  echo Found process with PID %pid%
  taskkill /F /PID %pid%
  echo Process terminated.
)
