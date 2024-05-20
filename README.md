# live-audio-transmission-using-socket-programming

### Technical Description of the Project

This project involves creating a real-time audio streaming application using Python. It consists of two main components: a server that transmits audio data and a client that receives and plays the audio data. The application uses sockets for network communication, and the `pyshine` library for audio capture and playback.

#### Components:

1. **Audio Capture and Playback:**
   - The `pyshine` library is used for capturing and playing audio.
   - Two modes are defined: `send` for the server and `get` for the client.

2. **Network Communication:**
   - The `socket` library is used for creating and managing network connections.
   - The server listens for incoming connections and transmits audio data.
   - The client connects to the server, receives audio data, and plays it.

#### Server Code:

1. **Setup:**
   - The server captures audio using `pyshine` in `send` mode.
   - A socket is created and bound to a specific IP address and port.
   - The server listens for incoming connections with a specified backlog.

2. **Connection Handling:**
   - When a client connects, the server enters a loop to continuously capture and send audio frames.
   - The audio frame is serialized using `pickle` and sent over the network.
   - The data is prefixed with a message length packed using `struct`.

3. **Audio Transmission:**
   - Audio frames are captured from the microphone.
   - Each frame is serialized and prefixed with its size before being sent to the client.

#### Client Code:

1. **Setup:**
   - The client is set to receive audio using `pyshine` in `get` mode.
   - A socket is created and connected to the server's address.

2. **Receiving Data:**
   - The client continuously listens for data from the server.
   - It first receives a fixed-size header indicating the size of the incoming audio frame.
   - The client then receives the full audio frame based on the size information.

3. **Audio Playback:**
   - The received audio frame is deserialized using `pickle`.
   - The deserialized frame is played using the `pyshine` library.

### Summary:

- **Server:**
  - Captures audio frames.
  - Serializes and sends frames to the client.
  - Listens for and accepts client connections.

- **Client:**
  - Connects to the server.
  - Receives serialized audio frames.
  - Deserializes and plays audio frames in real-time.

This setup allows real-time audio streaming from a server to a client using sockets and the `pyshine` library for audio capture and playback.
