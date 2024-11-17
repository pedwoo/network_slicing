# network_slicing

Next generation network project. Topic: network slicing through SDN, using Ryu network traffic controller

Ryu is an SDN framework written in python, manages network traffic by acting as a controller that communicates with network devices using the OpenFlow protocol.
Notes about Ryu:

-   Centralized traffic management: serves as the central intelligence in an SDN setup, it controls the flow of packets across the network by installing flow rules on OpenFlow-enabled switches. On the data plane, the switches forward packets based on flow rules, while on the control plane Ryu decides and dinamically updates the flow rules.
-   Packet processing workflow: when a packet arrives at a switch, if no matching flow rule exists in the switch, the packet is sent to the Ryu controller as "packet-in" event, wherer the controller's application logic processes the packet and determines the action to take (forwarding to specific port, dropping the packet, modifying headers, ...). Ruy then installs a new flow rule on the switch for similar packets in the future in order to minimize the communication overhead between the controller and switches
-   Traffic management features: Ryu provides APIs and libraries to manage various aspects of traffic, like path selection, QoS enforcement, load balancing and monioring. These features can be edited by the programmer of course
-   Custom applications: Ruy's modular architecture allows the programmer to write custom Python applications to manage traffic, such as traffic shaping for network slices, dynamic rerouting in case of link failures, or implementing policies for specific applications or users

## Requirements for the project (draft)

#### Functional requirements

1. Traffic classification: Implement a mechanism to classify traffic into different slices based on criteria such as:
    - Protocol
    - Source/destination IP addresses or ports
    - Application types
2. Dynamic path allocation
    - Configure and enforce separate paths for different slices in the network
    - Ensure low latency paths for high-priority traffic (e.g. real-time applications)
3. Quality of service enforcement
    - Apply bandwidth, latency, or priority policies to each slice
    - Monitor and adjust QoS paramenters dynamically based on network conditions
4. Traffic isolation
    - Ensure complete isolation between slices to prevent cross-slice interference or data leakage
5. Resilience and fault tolerance
    - Dynamically reroute traffic in case of a link or switch failure without disrupting active slices
    - Provide logs or metrics to demonstrate recovery
6. Scalability
    - Demonstrate the system can handle increasing traffic volumes or add/remove slices dynamically without performance degradation
7. Real-time monitoring
    - Display traffic statistic for each slice (throughput, packet loss, latency, ...)
    - Provide a dashboard or log file for administrators to analyze slice performance
8. Policy management
    - Allow easy configuration and updating of slicing policies, either through a configuration file or REST API

#### Non-functional requirements

1. Performance
    - Minimal latency introduced by the controller when processing packet-in events
    - Efficient flow rule installation to reduce controller overhead
2. Reliability
    - The system should handle packet drops, network congestion, and other animalies gracefully
3. Ease of deployment
    - Provide clear documentation for installing and running the system (e.g. Mininet setup, Ryu installation)
    - Use intuitive file structures and configuration methods
4. Security
    - Authenticate communication between the SDN controller and switches
    - Prvent unauthorized modifications to flow rules or slice configurations
5. Interoperability
    - The project should with with any OpenFlow-enabled switch and comply with OpenFlow standards

## Evaluation metrics

1. Traffic slicing accuracy: measure the correctness of traffic classification into slices
2. Latency and bandwidth: compare metrics between slices
3. Fault recovery time: measure the time taken to recover from link or switch failures
4. Scalability: test and report performance with increasing traffic or additional slices
5. Resource utilization: monitor the SDN controller's CPU and memory usage under load
