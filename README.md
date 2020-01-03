poky-app-container-mosquitto
=======================

build local container
=====================

```
pushd local_scripts/
```
```
./docker_build.sh
```
```
popd
```

run local container with ash
============================

```
pushd local_scripts/
```

```
./docker_run-ash.sh reslocal/poky-app-container-mosquitto
```

```
...
+ ID=$(docker run -t -i -d -p 1984:1883 reslocal/poky-app-container-mosquitto ash -l)
+ ID 257af8e7b082629b0d9c2b7b9b4749d9207591441ac61838a04dc59ee9b45734
+ docker attach 257af8e7b082629b0d9c2b7b9b4749d9207591441ac61838a04dc59ee9b45734
...
```

```
root@257af8e7b082:/# /etc/init.d/mosquitto restart
Restarting Mosquitto message broker mosquitto
```

```
root@257af8e7b082:/# mosquitto_sub -t 'test/topic' &

```

```
root@257af8e7b082:/# mosquitto_pub -t 'test/topic' -m 'helloWorld'
helloWorld
root@257af8e7b082:/# mosquitto_pub -t 'test/topic' -m 'helloWorld'
helloWorld
root@257af8e7b082:/# mosquitto_pub -t 'test/topic' -m 'helloWorld'
helloWorld

```

```
root@257af8e7b082:/# cat /var/log/mosquitto.log

```

```
1557925754: mosquitto version 1.5.8 starting
1557925754: Config loaded from /etc/mosquitto/mosquitto.conf.
1557925754: Opening ipv4 listen socket on port 1883.
1557925754: Opening ipv6 listen socket on port 1883.
1557925754: Warning: Mosquitto should not be run as root/administrator.
1557925834: New connection from 127.0.0.1 on port 1883.
1557925834: New client connected from 127.0.0.1 as mosqsub|14-257af8e7b082 (c1, k60).
1557925834: No will message specified.
1557925834: Sending CONNACK to mosqsub|14-257af8e7b082 (0, 0)
1557925834: Received SUBSCRIBE from mosqsub|14-257af8e7b082
1557925834:     test/topic (QoS 0)
1557925834: mosqsub|14-257af8e7b082 0 test/topic
1557925834: Sending SUBACK to mosqsub|14-257af8e7b082
1557925841: New connection from 127.0.0.1 on port 1883.
1557925841: New client connected from 127.0.0.1 as mosqpub|15-257af8e7b082 (c1, k60).
1557925841: No will message specified.
1557925841: Sending CONNACK to mosqpub|15-257af8e7b082 (0, 0)
1557925841: Received PUBLISH from mosqpub|15-257af8e7b082 (d0, q0, r0, m0, 'test/topic', ... (10 bytes))
1557925841: Sending PUBLISH to mosqsub|14-257af8e7b082 (d0, q0, r0, m0, 'test/topic', ... (10 bytes))
1557925841: Received DISCONNECT from mosqpub|15-257af8e7b082
1557925841: Client mosqpub|15-257af8e7b082 disconnected.
1557925843: New connection from 127.0.0.1 on port 1883.
1557925843: New client connected from 127.0.0.1 as mosqpub|16-257af8e7b082 (c1, k60).
1557925843: No will message specified.
1557925843: Sending CONNACK to mosqpub|16-257af8e7b082 (0, 0)
1557925843: Received PUBLISH from mosqpub|16-257af8e7b082 (d0, q0, r0, m0, 'test/topic', ... (10 bytes))
1557925843: Sending PUBLISH to mosqsub|14-257af8e7b082 (d0, q0, r0, m0, 'test/topic', ... (10 bytes))
1557925843: Received DISCONNECT from mosqpub|16-257af8e7b082
1557925843: Client mosqpub|16-257af8e7b082 disconnected.
1557925844: New connection from 127.0.0.1 on port 1883.
1557925844: New client connected from 127.0.0.1 as mosqpub|17-257af8e7b082 (c1, k60).
1557925844: No will message specified.
1557925844: Sending CONNACK to mosqpub|17-257af8e7b082 (0, 0)
1557925844: Received PUBLISH from mosqpub|17-257af8e7b082 (d0, q0, r0, m0, 'test/topic', ... (10 bytes))
1557925844: Sending PUBLISH to mosqsub|14-257af8e7b082 (d0, q0, r0, m0, 'test/topic', ... (10 bytes))
1557925844: Received DISCONNECT from mosqpub|17-257af8e7b082
1557925844root@257af8e7b082:/# 

```


```
root@257af8e7b082:/# exit
```

```
popd
```


run without ash
===============

```
pushd local_scripts/
```
```
./docker_run.sh reslocal/poky-app-container-mosquitto
```

```
...
+ ID=$(docker run -t -i -d -p 1984:1883 reslocal/poky-app-container-mosquitto)
+ ID a81b024b9f4c9255edb37731c3200953b794de769603833c4aa972cc588db957
+ docker attach a81b024b9f4c9255edb37731c3200953b794de769603833c4aa972cc588db957
1557926099: mosquitto version 1.5.8 starting
```
```
popd
```

kill it
=======
from another shell
```
pushd local_scripts/
```

```
./docker_kill.sh reslocal/poky-app-container-mosquitto
```
```
popd
```

