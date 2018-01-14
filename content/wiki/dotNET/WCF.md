===Chapter 3: Message Exchange Patterns, Topologies, and Choreographies===

==Message Exchange Patterns (MEP)==

The Datagram MEP

 * 1-way, send and forget
 * May or may not elicit a response, which would require a new connection
 * A datagram MEP is expressed in Web Services Description Language (WSDL) as an operation that contains a wsdl:input element and no wsdl:output elements
 * In WCF, the contract method must have a void return type, and the OperationContract attribute needs IsOneWay set to true
  * WCF applications that receive datagrams over HTTP send the 202 reply upon receipt of the datagram but before processing the datagram. This optimization means that the client does not wait unnecessarily for the transport reply, and the exchange is as close to one-way as possible.

The Request/Reply MEP

 * WCF operation contracts use the Request/Reply MEP by default. Any return type that is considered serializable by WCF can be specified as a return type
 * As of the initial release of WCF, there is no out-of-the-box support for the Request/Reply MEP using MSMQ, and there is no support for UDP. Using the MSMQ transport with a Request/Reply MEP requires a connection between the sender and the receiver as well as a connection between the receiver and the sender. As a result, a custom channel is also required

 The Duplex MEP

 * Duplex communication requires two contracts. By convention, the contract that describes the messages (and replies, if they are present) inbound to the receiver application are called service contracts, and contracts that describe messages sent from the receiver to the sender are called callback contracts
  * When creating a duplex contract, it is typically a good idea to make the operations one-way. If the OperationContractAttribute’s IsOneWay property is not set, the message exchanges will be request-reply, and both participants will incur the overhead of creating reply messages. Setting the IsOneWay property to true reduces the overhead required for each messaging interaction.

==Message Topologies==

A message topology is composed of one or more MEPs e.g. Point-to-point, datagram point-to-point, brokered, and peer-to-peer (P2P).

==Message Choreographies==

A message choreography is an organized set of message exchanges that represents one logical operation.
