---- sockData - send other data types via socket ----

This library can send other data types than just strings with socket.
You can normally only send strings with socket.
But with this library, you can send all data types that are supported by pickle.

How to use it:
	Sending:
		instead of '<yourConnectedSocket>.send(<string>.encode())'
		type: 'import sockData.send
		sockData.send.sendData(<yourConnectedSocket>, <data>)'
	Receiving:
		instead of '<yourConnectedSocket>.recv(<bufferSize>)'
		type: 'import sockData.receive
		sockData.receive.recvData(<yourConnectedSocket>, <bufferSize>)'

Examples:

server.py:
	
	import socket
	import sockData.receive

	sock = socket.socket()
	sock.bind(("", 50505))
	sock.listen(1)

	client, addr = sock.accept()

	dictionary = sockData.receive.recvData(client, 1024)
	print(dictionary)

	client.close()

client.py:
	
	import socket
	import sockData.send

	sock = socket.socket()
	sock.connect(("127.0.0.1", 50505))

	dictionary = {"message": {"from": "127.0.0.1", "msg": "hello!"}}
	sockData.send.sendData(sock, dictionary)

	sock.close()
