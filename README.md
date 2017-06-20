# wTool1CD

CGI-обёртка для утилиты tool_1CD.

## Настройка

В Apache в httpd.conf нужно прописать:
```

# Где будут лежать наши CGI
Alias "/oscgi/" "C:/opt/oscgi"
ScriptAlias "/oscgi-bin/" "C:/opt/oscript/bin/"  # тут путь к установленному ОдноСкрипту
<Directory "C:/opt/oscgi">
	Options +ExecCGI
	AddHandler cgi-script .os
</Directory>


LoadModule actions_module modules/mod_actions.so
Alias "/rep" "C:/1C/Rep/"          # Алиас для доступа
<Directory "C:/1C/Rep/Retail">     # Каталог хранилища
	Allow from all
	AddHandler tool1cd-file .1CD
	Action tool1cd-file /oscgi/tcd/wtool1cd.os # путь к CGI-обработчику 
	                                           #  (/oscgi - алиас, который мы настроили выше)
</Directory>


```