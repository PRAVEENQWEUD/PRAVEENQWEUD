- 👋 Hi, I’m @PRAVEENQWEUD
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
PRAVEENQWEUD/PRAVEENQWEUD is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
#This script only run on latest version of amino.py

import amino
import asyncio
import pyfiglet
print("\t\033[1;31mNewAdvertiseingBot\n\n")
print("\t\033[1;32m Script by \033[1;36mMr.comrade  \n\n")
async def main():
	client = amino.Client()    
	email = input("Email:-phsdv99450@uxsolar.com")
	password = input("Password:-123456")
	msg = input("Advertising Message:-http://aminoapps.com/p/2g28tt")
	await client.login(email=email, password=password)
	clients = await client.sub_clients(start=0, size=1000)
	for x, name in enumerate(clients.name, 1):
		print(f"{x}.{name}")
	communityid = clients.comId[int(input("choose the community >> "))-1]
	sub_client = await amino.SubClient(comId=communityid, profile=client.profile)
	while True:
		try:
			users = await sub_client.get_online_users(start=0, size=1000)
			for userId, level, nickname in zip(users.profile.userId, users.profile.level, users.profile.nickname):
				starting = await sub_client.start_chat(userId=[sub_client.profile.userId, userId], message=msg)
				print(f"Sended Advertise {nickname}, level = {level}")
		except amino.lib.util.exceptions.VerificationRequired as e:
			print(f"VerificationRequired")
			link = e.args[0]['url']
			print(link)
			verify = input("Waiting for verification >> ")
		except Exception as e:
			print(e)

loop = asyncio.get_event_loop()
loop.run_until_complete(main())
