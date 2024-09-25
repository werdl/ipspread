# White Paper for ipspreader
> A system to mask the IP address of a server, for theoretical use in a decentralized network (aka no reason other than learning)
## Abstract
- Tor is a system that masks the IP of the client to the server
- Is it possible, and how, to mask the IP of the server to the client?
- Whilst obviously not as secure as Tor, it could be useful in a decentralized network
- The insecutity comes from the requirement to have a trusted "post node" that can be trusted to not log the IP of the server
### Basic Principles
- A post node from a list of trusted nodes, agreed by both the client and the server, will be the site of the request
- An entry node takes the initial requests from the client
- There are 4 or 8 carrier nodes, each of which wrap their IP octet around the request in a layer of encryption, the private key of which is known only to the post node.
- The post node unwraps the request and IP, and forwards the request to the server
- The server responds to the post node, which wraps the response in their private key followed by the post node's public key, and returns it to the post node
- Embedded in the initial request, the client's public key is sent to the server, which is used to encrypt the response
- Also in the initial request, the client's IP is sent to the server, which is used to know where to send the response
- The request will be a sent through a series of carrier nodes, however without encryption or decryption, to the client with the response
- The TCP response will have been stripped of MAC and Ethernet headers, and the IP header will be replaced with the UID (unique identifier) of the server, which is how the client knows which server it wants to find.
- Each carrier node is responsible for only one octet, which it stores in a list. This allows for less, albeit still significant, vetting of the carrier nodes by the network operator - a community, presumably as I don't intend to run this network to avoid the "centralization in practice" problem.