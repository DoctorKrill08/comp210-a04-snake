# A4 Write-up

**Name:** Ethan Kim
**Onyen:** ewk
**Game URL:** [https://bridges-cs.herokuapp.com/assignments/4/](https://bridges-games.herokuapp.com/assignments/4/DoctorKrill#)
**Bomb rule I played with (SHRINK or GAME_OVER):** SHRINK

Three questions, 20 points. A few sentences each. Where a question asks for a
number, show where it came from.

---

## Question 1: The tail pointer (7 points)

Your `LinkedQueue` keeps a `tail` reference. Suppose you deleted it and found
the back of the queue by starting at `head` and following `next` until you ran
out of nodes.

What would `enqueue` cost then, in Big-O? The game calls `enqueue` once per
tick and runs about 7 ticks a second. For a snake 500 cells long, roughly how
many nodes would `enqueue` alone visit each second, and would you notice?

Now do the same for the autograder's speed test. It fills a queue with
400,000 items, then does 400,000 more rounds of dequeue-then-enqueue, so the
queue stays at 400,000. Roughly how many nodes would those enqueues visit?

```
Enqueue would run at O(n) because it has to go through each node in the linked list once. 
Enqueue would visit 3500 nodes a second. You would probably notice because the game will be using signficantly more memory than necessary.

The enqueues visit about 2.4 x 10^11 nodes.
Because to build the 400,000 initial nodes it would need to visit 1 + 2 + 3 + 4 ... + 400,000 which is about 8 x 10^10.
For the 400,000 dequeue enqueue sequence, the corresponding enqueue would visit 400,000 nodes x 400,000 times so about 1.6 x 10^11 nodes
So in total this adds up to 8x10^10 + 1.6x10^11 equals about 2.4x10^11 or 240000000000 nodes visited.
```

---

## Question 2: The one method allowed to walk (7 points)

`contains` is O(n), and the game calls it through `snake.occupies(...)`. Read
`GameState.tick()` and `GameState.freeCell()` and find every call.

On a tick where the snake eats an apple, roughly how many nodes do those
`contains` calls visit in total, for a snake of length n on the 30 by 30
board? Give an expression in n. Then name a data structure from later in this
course that would make "is the snake on this cell?" fast, and say what it
would cost to keep it up to date as the snake moves.

```
When a snake eats an apple, contains visits n cells and is called 30 x 30 times so 900n nodes are iterated through.
An array/matrix where when you check a specific coordinate, it returns what is occupying it.
```

---

## Question 3: Which end is the head? (6 points)

The snake's head is the **back** of the queue, and its tail end is the
**front**. Explain why, using what happens to the body on each tick.

Then suppose you flipped it, so the head was the front. Which operation would
each tick need that `LinkedQueue` does not have, and why is that operation hard
to make O(1) on a singly linked list?

```
The head is in the back because it makes it easy to remove the current head without effecting other nodes. The tail is in the front because it makes it easy to add another node to the snake.
If it were flipped, then to move, the tail would have to be popped/removed (and the item before the tail would have to become a tail) and the head would have to grow meaning the added node's next value would have to be the head value and the head will become this added node.
This is hard to make O(1) because for the tail operation, the code would need to iterate through and find the item before the tail (because queues are FIFO) to set its next value to null.
```
