1a)bit stuffing

def bit_stuffing(N, arr):
    brr = []  # Output array after bit stuffing
    count = 0

    for i in range(N):
        brr.append(arr[i])
        if arr[i] == 1:
            count += 1
        else:
            count = 0

        # After 5 consecutive 1's, insert a 0
        if count == 5:
            brr.append(0)
            count = 0

    # Print the stuffed bits
    print("After Bit Stuffing:")
    print(" ".join(map(str, brr)))


# ✅ Main section
if __name__ == "__main__":
    N = 6
    arr = [1, 1, 1, 1, 1, 1]  # Example input
    print("Original Data:")
    print(" ".join(map(str, arr)))
    bit_stuffing(N, arr)

1b)character stuffing

def characters_stuffing(data, flag='F', escape='E'):
    stuffed_data = ''
    for ch in data:
        if ch == flag or ch == escape:
            stuffed_data += escape + ch
        else:
            stuffed_data += ch
    return flag + stuffed_data + flag

data = "HelloF EwogE!"
stuffed_data = characters_stuffing(data)
print("Original data:", data)
print("Stuffed data:", stuffed_data)

2a)crc code
def crc_encode():
    Polynomial = input("Enter polynomial: ")
    frame = input("Enter the frame: ")
    m = len(Polynomial)
    n = len(frame)

    for i in range(m):
        if Polynomial[i] == '1':
            Polynomial = Polynomial[i:]
            m = len(Polynomial)
            break

    Polynomial = list(Polynomial)
    cl = m + n - 1
    c = list(frame) + ['0'] * (cl - n)

    for i in range(n):
        if c[i] == '1':
            for j in range(m):
                c[i + j] = '0' if Polynomial[j] == c[i + j] else '1'

    c[:n] = frame
    message = ''.join(c)
    print(f"The message is: {message}")

crc_encode()

2b)crc-12,crc-16,ccit
def compute_crc(data: str, poly: int, width: int, init_crc: int = 0) -> int:
    data_int = int(data, 2) << (width - 1)
    mask = 1 << (data_int.bit_length() - 1)

    while mask >= (1 << (width - 1)):
        if data_int & mask:
            data_int ^= poly << (data_int.bit_length() - width)
        mask >>= 1

    return data_int

def format_crc(crc: int, width: int) -> str:
    return format(crc, '0{}b'.format(width))

def main():
    binary_data = input("Enter binary data: ")

    # CRC-12
    poly_12 = 0x80F
    crc12 = compute_crc(binary_data, poly_12, 12)
    print(f"CRC-12     : {format_crc(crc12, 12)}")

    # CRC-16
    poly_16 = 0x8005
    crc16 = compute_crc(binary_data, poly_16, 16)
    print(f"CRC-16     : {format_crc(crc16, 16)}")

    # CRC-CCITT
    poly_ccitt = 0x1021
    crc_ccitt = compute_crc(binary_data, poly_ccitt, 16)
    print(f"CRC-CCITT  : {format_crc(crc_ccitt, 16)}")

if __name__ == "__main__":
    main()


3)gobackn

import threading
import time
import random

class GoBackN:
    def __init__(self, window_size, total_frames):  # ✅ fixed __init__
        self.window_size = window_size
        self.total_frames = total_frames
        self.sent_frames = 0
        self.acknowledged_frames = 0
        self.lock = threading.Lock()

    def send_frame(self, frame):
        print(f"Sender: Sending frame {frame}")

    def receive_ack(self, frame):
        print(f"Receiver: Acknowledgment received for frame {frame}")

    def transmit(self):
        while self.acknowledged_frames < self.total_frames:
            with self.lock:
                # Send frames within the window
                while self.sent_frames < min(self.acknowledged_frames + self.window_size, self.total_frames):
                    self.send_frame(self.sent_frames)
                    self.sent_frames += 1

            time.sleep(1)  # Simulate transmission delay

            with self.lock:
                for frame in range(self.acknowledged_frames, self.sent_frames):
                    # Randomly simulate success or failure
                    if random.randint(0, 2) > 0:
                        self.receive_ack(frame)
                        self.acknowledged_frames += 1
                    else:
                        print(f"Receiver: Frame {frame} lost ❌, retransmitting from frame {frame}")
                        self.sent_frames = self.acknowledged_frames
                        break

        print("✅ All frames acknowledged!")


def main():
    window_size = 4
    total_frames = 10
    gbn = GoBackN(window_size, total_frames)

    sender_thread = threading.Thread(target=gbn.transmit)
    sender_thread.start()
    sender_thread.join()

    print("\nTransmission complete ✅")


# ✅ Correct main check
if __name__ == "__main__":
    main()


4).Dijkstra’s Algorithm
import sys

class Graph:
    def __init__(self, vertices):  # ✅ fixed __init__
        self.u = vertices
        self.graph = [[0 for column in range(vertices)] for row in range(vertices)]

    def printSolution(self, dist):
        print("Vertex \t Distance from Source")
        for node in range(self.u):
            print(node, "\t", dist[node])

    def minDistance(self, dist, sptSet):
        min_val = sys.maxsize
        min_index = -1
        for u in range(self.u):
            if dist[u] < min_val and sptSet[u] == False:
                min_val = dist[u]
                min_index = u
        return min_index

    def dijkstra(self, src):
        dist = [sys.maxsize] * self.u
        dist[src] = 0
        sptSet = [False] * self.u

        for _ in range(self.u):
            x = self.minDistance(dist, sptSet)
            sptSet[x] = True

            for y in range(self.u):
                if self.graph[x][y] > 0 and not sptSet[y] and dist[y] > dist[x] + self.graph[x][y]:
                    dist[y] = dist[x] + self.graph[x][y]

        self.printSolution(dist)


if __name__ == "__main__":  # ✅ fixed __name__
    g = Graph(9)
    g.graph = [
        [0, 4, 0, 0, 0, 0, 0, 8, 0],
        [4, 0, 8, 0, 0, 0, 0, 11, 0],
        [0, 8, 0, 7, 0, 4, 0, 0, 2],
        [0, 0, 7, 0, 9, 14, 0, 0, 0],
        [0, 0, 0, 9, 0, 10, 0, 0, 0],
        [0, 0, 4, 14, 10, 0, 2, 0, 0],
        [0, 0, 0, 0, 0, 2, 0, 1, 6],
        [8, 11, 0, 0, 0, 0, 1, 0, 7],
        [0, 0, 2, 0, 0, 0, 6, 7, 0]
    ]
    g.dijkstra(0)


5)subnet nodes

def main():
    n = int(input("Enter the number of nodes: "))
    adjacency_matrix = [[0 for _ in range(n + 1)] for _ in range(n + 1)]

    print("Enter adjacency matrix values (0 or 1 for each pair):")
    for i in range(1, n + 1):
        for j in range(1, n + 1):
            adjacency_matrix[i][j] = int(input(f"Enter connection between node {i} and node {j} (0 or 1): "))

    root = int(input("Enter the root node: "))
    print(f"Adjacent nodes of root node {root}:")

    for j in range(1, n + 1):
        if adjacency_matrix[root][j] == 1:
            print(j, end=" ")
    print("\n")


if __name__ == "__main__":  # ✅ Fixed
    main()


6)distance vector routing algorithm

print("Distance Vector Routing Algorithm\n")

# Number of nodes
n = int(input("Enter number of nodes: "))

print("Enter cost matrix (use a large number like 999 for infinity):")
cost = []
for i in range(n):
    row = list(map(int, input().split()))
    cost.append(row)

# Initialize distance matrix
dist = [row[:] for row in cost]

# Distance Vector Algorithm
for it in range(1, n):
    print(f"\nIteration {it}:")
    for i in range(n):
        for j in range(n):
            for k in range(n):
                if dist[i][j] > dist[i][k] + dist[k][j]:
                    dist[i][j] = dist[i][k] + dist[k][j]

        print(f"Routing table for node {i}: {dist[i]}")

# Final routing tables
print("\nFinal Routing Tables:")
for i in range(n):
    print(f"Node {i}: {dist[i]}")



7)encryption and decreption

from cryptography.fernet import Fernet
# Step 1: Generate a key for encryption and decryption
key = Fernet.generate_key()
cipher = Fernet(key)
# Step 2: Take input from user
data = input("Enter text to encrypt: ").encode()  # convert string to bytes
# Step 3: Encrypt the data
encrypted_data = cipher.encrypt(data)
print("\nEncrypted text:", encrypted_data.decode())
# Step 4: Decrypt the data
decrypted_data = cipher.decrypt(encrypted_data)
print("Decrypted text:", decrypted_data.decode())
# Step 5: Display the key
print("\nKeep this secret key safe if you want to decrypt later:")
print(key.decode())


8)leaky bucket 

# Leaky Bucket Algorithm

bucket_size = int(input("Bucket size: "))
output_rate = int(input("Output rate: "))
n = int(input("No. of packets: "))

bucket = 0

for i in range(n):
    incoming = int(input(f"Packet {i+1} size: "))

    # Check overflow
    if bucket + incoming > bucket_size:
        print("Packet dropped!")
    else:
        bucket += incoming

    # Leak packets
    if bucket >= output_rate:
        bucket -= output_rate
    else:
        bucket = 0 def __init__(self, seq, pages, idx):  # ✅ Fixed constructor name
        self.seq = seq
        self.pages = pages
        self.idx = idx


def input_frames():
    n = int(input("Enter number of frames: "))
    frames = []
    for i in range(n):
        seq = int(input(f"\nEnter sequence number for frame {i + 1}: "))
        pages = list(map(int, input("Enter pages separated by space: ").split()))
        frames.append(Frame(seq, pages, i))

    # Sort frames by sequence number for correct transmission order
    frames.sort(key=lambda x: x.seq)
    return frames
class Frame:
   

def round_robin(frames, q):

    done = False
    idx = [0 for _ in range(len(frames))]  # Track how many pages are sent per frame
    print("\n=== Round Robin Output ===")

    while not done:
        done = True  # Assume done unless we find a frame still transmitting
        for i in range(len(frames)):
            cnt = 0
            while cnt < q and idx[i] < len(frames[i].pages):
                print(f"Frame: {frames[i].seq}, Page Content: {frames[i].pages[idx[i]]}")
                idx[i] += 1
                cnt += 1
                done = False  # Still transmitting
        if all(idx[i] == len(frames[i].pages) for i in range(len(frames))):            break


if __name__ == "__main__":  # ✅ Fixed main condition
    frames = input_frames()
    quantum = int(input("\nEnter quantum: "))
    round_robin(frames, quantum)


    print("Bucket now:", bucket)


9)buffers
 def __init__(self, seq, pages, idx):  # ✅ Fixed constructor name
        self.seq = seq
        self.pages = pages
        self.idx = idx


def input_frames():
    n = int(input("Enter number of frames: "))
    frames = []
    for i in range(n):
        seq = int(input(f"\nEnter sequence number for frame {i + 1}: "))
        pages = list(map(int, input("Enter pages separated by space: ").split()))
        frames.append(Frame(seq, pages, i))

    # Sort frames by sequence number for correct transmission order
    frames.sort(key=lambda x: x.seq)
    return frames
class Frame:
   

def round_robin(frames, q):

    done = False
    idx = [0 for _ in range(len(frames))]  # Track how many pages are sent per frame
    print("\n=== Round Robin Output ===")

    while not done:
        done = True  # Assume done unless we find a frame still transmitting
        for i in range(len(frames)):
            cnt = 0
            while cnt < q and idx[i] < len(frames[i].pages):
                print(f"Frame: {frames[i].seq}, Page Content: {frames[i].pages[idx[i]]}")
                idx[i] += 1
                cnt += 1
                done = False  # Still transmitting
        if all(idx[i] == len(frames[i].pages) for i in range(len(frames))):            break


if __name__ == "__main__":  # ✅ Fixed main condition
    frames = input_frames()
    quantum = int(input("\nEnter quantum: "))
    round_robin(frames, quantum)