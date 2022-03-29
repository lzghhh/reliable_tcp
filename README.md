### High level approach:

We have implemented the sender and receiver as well as the window in both of them. The sender will send what it has read from the stdin and send the first packet.
At this time, our window size is 1 from our sender's view and it will wait for receiver to acknowledge this packet. If this packet is successfully reached receiver and ack
to the sender, then we will increase the window size by 2 times. By doing this, we will be able to capture the situation of network and whether it will corrupt, duplicate or dropping
the sender's packets. If these happens frequently, then we need to slow down our speed in sending packets to receiver due to what we observe and increase the frequency if network is good.
Meanwhile, sender need also keep track of the ability to resend a timed out packet that it has already send but not receiving any ack from the receiver. In this case, we will notice that the network
has delaying and we need to decrease our window size as well as increasing our estimation of RTT(round trip time). If the ack is successfully delivered within our estimation, then we decrease our
RTT estimation because now we believe the internet is better.

From the receiver side, it will check for whether the packets has duplicated, corrupted, or in different order comparing to what have sent. Thus in this case, what it will do is to drop any packet that
are duplicated on the ground and send an ack back because it might be the case that previous ack is dropped, ignore the corrupted packet, and finally dealing with the in ordering by keep track of
whether the current data received is in correct order before print out to stdout.

### Challenges:

We believe the most challenges thing is dealing with all sorts of errors and delays that may happen in the network and capturing them in our code in different situation. Among them, the correctness
of our window size is the most challenging and we have spent a lot of time on debugging them. Also, to correctly improving our program to pass the performance test is also challenging as we need
to come out ways to decrease bytes sent and our running time.

### Properties/Features:

We have used hashing technique instead of checksum when detecting the corruption happens in our message which is faster and safer than calculating a one bit checksum.
Meanwhile, we have implemented our own way of time out functionality that keep tracks the time using the original time library in python
We have also use try except block that not only captures Json decode error, but also errors like duplicate packets that reusing our previous codes.

### Testing:

We have tested our code by running through all the tests given in the config file and printing out important information that we believe is vital for our debugging.
Meanwhile, we have also used debugging techniques like grep in order to fetch important messages from the run script that may be helpful.
Furthermore, we have also conducted a thorough run on both our sender and receiver both in compile time and dynamic time.
