//Открываем терминал PowerShell в Windows 10 или другой от имени администратора
Win+R -> PowerShell
//Генерируем SSH-ключ
ssh-keygen -t -rsa -b 4096 -C "(тут_ваша_почта_из_github)"
//Далее можно изменить путь и ввести пароль, или же просто нажать 'Enter'
//Проверьте, установлен ли OpenSSH в Windows
Get-WindowsCapability -Online | ? Name -like 'OpenSSH.Client*'
//если нет, то устанавливаем одним из способов:
С помощью команды PowerShell: Add-WindowsCapability -Online -Name OpenSSH.Client*
С помощью DISM: dism /Online /Add-Capability /CapabilityName:OpenSSH.Client~~~~0.0.1.0
//Запускаем вручную сервиса ssh в windows
Get-Service -Name ssh-agent | Set-Service -StartupType Manual
//Запускаем SSH-агента
Start-Service ssh-agent
//Добавьте ваш закрытый ключ в базу ssh-agent:
ssh-add "C:\Users\user\.ssh\id_rsa"
//Отображаем публичный ключ
cat "C:\ProgramData\ssh\sshd_config"| Select-String "Authentication"
//Копируем ответное сообщение и вставляем текст в
https://github.com/settings/keys