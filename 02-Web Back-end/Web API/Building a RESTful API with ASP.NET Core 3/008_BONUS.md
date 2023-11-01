BONUS

Wednesday, April 29, 2020

12:00 PM

Instead of having my DB created locally, I used Docker to get things potentially easily moved later...

<https://octopus.com/blog/running-sql-server-developer-install-with-docker>

\^\^\^ Used this link as guide

docker pull microsoft/mssql-server-windows-developer

docker run \--name AbrigoKeyValueStoreDB -d -p 1433:1433 \--volume C:\\Docker\\Volumes\\SQLServer:C:\\SQLData -e sa_password=HelloAbrigo123 -e ACCEPT_EULA=Y microsoft/mssql-server-windows-developer

Then later in SSMS:

![](008_BONUS_000.png)

DONE

mssql:\
image: microsoft/mssql-server-linux:2017-CU4\
environment:\
SA_PASSWORD: \"MySuperRandomStrong!Passw0rd!\"\
ACCEPT_EULA: \"Y\"\
volumes:\
- ./data/mssql:/var/opt/mssql\
ports:\
- \"1433:1433\"

To SSH into the contianer:

**docker exec -it \<containerName\> powershell**

To leave:

CTRL+P CTRL+Q
