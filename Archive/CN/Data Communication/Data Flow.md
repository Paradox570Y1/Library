Communication between two devices can be simplex, half-duplex, or full-duplex
- __Simplex__
     - In simplex mode, the communication is unidirectional, as on a one-way street. Only one of the two devices on a link can transmit; the other can only receive.
     - `Keyboards and traditional monitors` are examples of simplex devices. The key board can only introduce input; the monitor can only accept output.
     - The simplex mode can use the entire capacity of the channel to send data in one direction.
     ![[Pasted image 20240630113909.png|500]]
- __Half-Duplex__
     - In half-duplex mode, each station can both transmit and receive, but not at the same time. When one device is sending, the other can only receive, and vice versa.
     - This mode is like a one-lane road with traffic allowed in both directions. When cars are traveling in one direction, cars going the other way must wait.
     - In a half-duplex transmission, the entire capacity of a channel is taken over by whichever of the two devices is transmitting at the time.
     - `Walkie-talkies` and `CB (citizens band) radios` are both half-duplex systems.
     - This mode is used in cases where there is no need for communication in both directions at the same time; the entire capacity of the channel can be utilized for each direction.
     ![[Pasted image 20240630114230.png|500]]
- __Full-Duplex__
     - In full-duplex mode (also called duplex), both stations can transmit and receive simultaneously.
     - This mode is like a two-way street with traffic flowing in both directions at the same time.
     - In this mode, signals going in one direction share the capacity of the link with signals going in the other direction. This sharing can occur in two ways: 
         - Either the link must contain two physically separate transmission paths, one for sending and the other for receiving.
         - The capacity of the channel is divided between signals traveling in both directions.
     - One common example of full-duplex communication is the `telephone network`. When two people are communicating by a telephone line, both can talk and listen at the same time.
     - This mode is used when communication in both directions is required all the time. The capacity of the channel, however, must be divided between the two directions.
     ![[Pasted image 20240630114943.png|500]]
