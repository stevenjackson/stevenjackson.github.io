Host bastion
  Hostname bastion.example.com
  User awesomedude

Host *.example.com
  ProxyCommand ssh -W %h:%p bastion

Host web
  Hostname web-00.example.com
