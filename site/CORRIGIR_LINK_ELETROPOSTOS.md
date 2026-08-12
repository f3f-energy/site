@echo off

title CORRIGINDO LINK DO ELETROPOSTOS - F3F GESTAO

color 0A



echo.

echo ============================================================

echo    🔧 CORRIGINDO LINK DO CARDE "ELETROPOSTOS" NO INDEX

echo ============================================================

echo.



set "INDEX=index.html"

set "BACKUP=index\_backup\_%date:\~6,4%%date:\~3,2%%date:\~0,2%\_%time:\~0,2%%time:\~3,2%%time:\~6,2%.html"



echo 📦 Criando backup do index.html...

copy "%INDEX%" "%BACKUP%" >nul

echo    ✅ Backup criado: %BACKUP%



echo.

echo 📝 Corrigindo link do card "Eletropostos"...



powershell -Command "(Get-Content '%INDEX%') -replace '<a class=\\"svc-link\\" onclick=\\"abrirPaginaMobilidade\\(event\\)\\">Ver detalhes da Solução →</a>', '<a class=\\"svc-link\\" href=\\"pages/eletropostos.html\\">Ver detalhes da Solução →</a>' | Set-Content '%INDEX%'"



if %errorlevel% == 0 (

&#x20;   echo    ✅ Link corrigido com sucesso!

) else (

&#x20;   echo    ❌ Erro ao corrigir. Tentando metodo alternativo...

&#x20;   powershell -Command "$conteudo = Get-Content '%INDEX%' -Raw; $conteudo = $conteudo -replace 'onclick=\\"abrirPaginaMobilidade\\(event\\)\\"', 'href=\\"pages/eletropostos.html\\"'; Set-Content '%INDEX%' -Value $conteudo"

)



echo.

echo ============================================================

echo    ✅ CORRECAO FINALIZADA!

echo ============================================================

echo.

echo 📋 O que foi feito:

echo    1. Backup criado: %BACKUP%

echo    2. Link do card "Eletropostos" atualizado

echo    3. Agora aponta para: pages/eletropostos.html

echo.

echo 🚀 Agora execute:

echo    git add .

echo    git commit -m "🔗 Corrige link do card Eletropostos"

echo    git push

echo.

pause

