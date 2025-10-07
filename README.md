sequenceDiagram
    participant Client
    participant Server

    Client->>Server: ClientHello
    Server-->>Client: ServerHello
    Server-->>Client: Certificate
    Server-->>Client: ServerHelloDone

    Note over Client: Verify certificate
    Client->>Server: ClientKeyExchange
    Client->->Server: ChangeCipherSpec
    Client->>Server: Finished

    Server-->>Client: ChangeCipherSpec
    Server-->>Client: Finished

    rect rgb(230, 255, 230)
        Note over Client,Server: Secure communication begins
    end
