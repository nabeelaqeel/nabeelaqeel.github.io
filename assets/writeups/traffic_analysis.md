## Traffic Analysis

## 1st Challenge : Data Breach
### category : traffic analysis
![alt text](images/traffic-8.png)


We received a PCAP file. Let's fire up Wireshark using this command:


```sh
open databreach.pcapng
```


Lets try seach `flag{` and change the packet bytes to packet details

![](images/traffic-9.png)

Let's follow the packet stream by right-clicking and selecting "Follow" then "Follow HTTP Stream".

As we scroll, we see the flag

![alt text](images/traffic-11.png)

flag{Information_disclosure_in_the_head}


## 2st Challenge : Wild Wild West
### category : traffic analysis
![](images/traffic-12.png)

It's another PCAP file. So let's fire up Wireshark once more.

Let's try using the search function again. We found the previous flag, but if we go to the next search, we get this:

![alt text](images/traffic-14.png)

Let's follow the stream, and we found the flag

![](images/traffic-15.png)

flag{kerbrute_finding_users}

Here is something cool I found while doing the challenge: I tried using a filter with HTTP and saw there's a PNG file. Then I thought, "Hmm, can I extract it?" So I googled it, and yes, I can. Here's how to do it:

![alt text](images/traffic-17.png)

Follow the PNG packet.

To extract it, we need to get only the PNG data. From a Google search and ChatGPT, we learned that the start of a PNG file is `89 50 4E 47 0D 0A 1A 0A` and the end is `49 45 4E 44 AE 42 60 82`.

Every PNG file will follow this format. So let's change the "Show data as" section from `UTF-8` to `raw` and start by finding the start of the PNG

![alt text](images/traffic-18.png)

here it is lets find the end of the png

![alt text](images/traffic-19.png)

Lets copy the from start till the end

Lets paste it to hexed.it
and click export

and now you yourself an image of Window Server

![alt text](images/traffic-20.png)