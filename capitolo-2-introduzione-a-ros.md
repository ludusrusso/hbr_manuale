# Capitolo 2. Introduzione a ROS

## Utilizzando la piattaforma di Cloud Robotics

ROS \(the Robot Operating System\) è un framework per lo sviluppo di applicazioni Robotiche connesse! Nato nel 2007 a Stanford, è diventato in poco tempo uno standard di fatto a livello Universitario e Industriale, grazie all'enorme community di ricercatori e sviluppatori che gravitano intorno al progetto.

In questo capitolo, impareremo le basi di ROS, implemetando passo passo dei semplici progetti per mezzo della piattaforma di Cloud Robotics.

## Implementiamo un semplice Publisher

```py
from dotbot_ros import DotbotNode, Rate, Publisher
from std_msgs.msg import String

class Node(DotbotNode):
    node_name = 'simple_publisher'

    def setup(self):
        self.loop_rate = Rate(1)
        self.pub = Publisher('chatter', String)
        self.cnt = 0

    def loop(self):
        s = "ciao: %s!"%self.cnt
        self.pub.publish(s)
        self.cnt += 1
```

## ![](/assets/Schermata 2017-05-28 alle 11.49.11.png)Implementiamo un semplice Subscriber

```py
from dotbot_ros import DotbotNode, Subscriber
from std_msgs.msg import String

from sys import stdout

class Node(DotbotNode):
    node_name = 'simple_subscriber'

    def setup(self):
        print 'starting'
        stdout.flush()
        self.chatter_sub = Subscriber('chatter', String, self.chatter_cb)

    def chatter_cb(self, msg):
        print 'Ho ricevuto: %s'%msg.data
        stdout.flush()
```



