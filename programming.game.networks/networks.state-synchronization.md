https://gafferongames.com/post/state_synchronization/

Send both input + state

No need for determinism since simulation runs on both sides

send state updates for a few objects instead of every

need to be smart about which objects to fit in the packet to save bandwidth

### Priority Accumulator

need a way to distribute updates across all objects in the simulation

Data structure:

- array of floast values, one value per-object that is tracked frame to frame

Algorithm:

- add current priority value for object to its acc value

- sort objects from largest to smallest

- the first n objects in the sorted list are prioritized and sent to the frame

- you might have to limit the number of objects that are updated due to bandwidth constraints

- e.g. 256 kbit/sec

- calculate header size + preamble(sequence, # of objects in packet, etc.) + the rest

the rest = objects that will fit

objects that will fit:

take n most important objects

walk packets in order

if their state update fits, push into packet

otherwise skip

serialize packet once it's full

reset processed object acc to 0

leave skipped objects alone

objects that didn't fit the first time are first in line for update in the next packet


### Jitter Buffer

mitigating jitter

jitter buffer evens out uneven distribution of incoming packets

e.g. 0 packets 1 frame, 2 the next, 1 next, etc.

this causes poor quality extrapolation

### Applying State Updates

### Quantize Both Sides States