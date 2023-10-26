//��������� �������� PowerShell � Windows 10 ��� ������ �� ����� ��������������
Win+R -> PowerShell
//���������� SSH-����
ssh-keygen -t -rsa -b 4096 -C "(���_����_�����_��_github)"
//����� ����� �������� ���� � ������ ������, ��� �� ������ ������ 'Enter'
//���������, ���������� �� OpenSSH � Windows
Get-WindowsCapability -Online | ? Name -like 'OpenSSH.Client*'
//���� ���, �� ������������� ����� �� ��������:
� ������� ������� PowerShell: Add-WindowsCapability -Online -Name OpenSSH.Client*
� ������� DISM: dism /Online /Add-Capability /CapabilityName:OpenSSH.Client~~~~0.0.1.0
//��������� ������� ������� ssh � windows
Get-Service -Name ssh-agent | Set-Service -StartupType Manual
//��������� SSH-������
Start-Service ssh-agent
//�������� ��� �������� ���� � ���� ssh-agent:
ssh-add "C:\Users\user\.ssh\id_rsa"
//���������� ��������� ����
cat "C:\ProgramData\ssh\sshd_config"| Select-String "Authentication"
//�������� �������� ��������� � ��������� ����� �
https://github.com/settings/keys