> **Experimental. We are just trying this.**
>
> Good intentions, shaky hands. STP does not know what he is doing. We test, we write down what we think we saw, and that is the whole product. A number here is not the truth. A chart is not the truth. Any other sentence that sounds sure of itself is not the truth either. Do not count any of it as a claim.
>
> [Disclaimer](DISCLAIMER.md)

# Desk try for 3500 included transactions a second

## What

The bar on this page is an included rate well over 3,500 transactions a second on Testnet-10. Included means the sender saw the transaction in the virtual chain. A submit acknowledgement is a different number. This page is not the 9 Oct or 13 Oct storm, and it does not move that storm's fee.

The long included hold in [tn10-build-desk-tps](https://github.com/STP-KAS/tn10-build-desk-tps) is 2,207 seen-accepted transactions a second for 6 hours 1 minute, from 2026-10-06T23:53:27Z to 2026-10-07T05:54:53Z, at fee 200/300. The published 6,321 is submit-OK for 20 seconds. Seen-accepted in that same window is about 1,900 a second.

## Why a signed payment stops near 3,080

rusty-kaspa v2.1.0 gives each block 500,000 compute mass. Live Testnet-10 aims at about 10 blocks a second. A signed one-input, one-output payment is about 1,624 grams. One signature is 1,000 grams before the bytes are counted.

500,000 / 1,624 is about 308 of those payments in one block. At 10 blocks a second that shape is about 3,078 included transactions a second. A worker, a miner, a second RPC name, or a higher fee does not add grams. The same reading is in [what-limits-tx-rate](https://github.com/STP-KAS/what-limits-tx-rate).

On 7 Oct 2026 the desk node was already taking full blocks of that shape: about 304 to 307 transactions, compute mass about 497,000 of 500,000, near 3,050 to 3,070 a second for the network. This desk's own seen-accepted share of those blocks stayed about 1,400 to 2,222.

## Why a lighter hop can pass 3,500

An anyone-can-spend hop with no signature measured 643 grams. 500,000 / 643 is 777 of those hops in one block. At 10 blocks a second the mass ceiling is 7,770 included transactions a second. 3,500 of them need about 2.25 million grams a second, which is under the 5 million gram budget. The mass is not the thing in the way. The sender pipeline is.

The redeem is a short script: push a lane number, drop it, leave true. The last saved hold of this shape, depth 1 and 8,192 lanes, included 127.7 a second over its measured minute, with a median lag of 8.3 seconds. Earlier steps of the same shape climbed until about 2,000 lanes and then flattened under 2,700. Depth 1 waits for each hop before the next one, so the send rate cannot run ahead of inclusion.

## What this test will not do

It will not spend coins a live signer is already using. It will not start a second node on this machine. It will not mine. It will not clear an older halt. It stops itself if a public mempool reaches 80,000. A public node started with a low memory scale can die at 100,001. Several public names are still one machine.

## Journal

Newest first. Each entry is one try. A number is a reading from that window.

### 2026-10-07 15:01Z — the 2,951 shape again, then one socket went quiet

**What.** Start the same three ranges again. Fee 1,600. Depth 2. One submit socket each on the desk node. No new coins from the wallet.

**Why.** 2,951 was one minute. A second minute of the same shape would show whether that number holds. The block does not have to be full for this to be worth running.

**Result.** The first measured minute included 706, 936, and 986 a second. Together 2,627. The next two minutes were 2,458 and 2,236. Orphans were 0. Ratio stayed about 1. All lanes stayed up. One sender was already the slow one: its submit call took about 214 ms, against 12 to 18 ms on the other two. By 15:13Z that slow sender was at 8 a second, then at 0, with every lane still marked live and no reject line. The other two fell through about 220 to about 160 and about 57. Local mempool fell from a few thousand to the tens and the hundreds. In the same later window the desk node processed blocks at about 162,000 compute grams of 500,000, and its own virtual-chain rate was about 834 transactions a second, with about 181 a second arriving by RPC. Public pools were about 14,000 to 17,000. The 2,951 shape did not hold. A socket can go silent while its lanes still count as live. Grams were not the cap in that window. 3,500 was not reached.

### 2026-10-07 14:35Z — lighter hop, depth 2, lanes that were already funded

**What.** Resume 4,096 anyone-can-spend lanes that already hold coins. Depth 2, so a lane may have two hops in flight. Submit through this desk's own synced node. Fee stays the sender's rule: 1.5 times the regular bucket, floor 150, cap 2,000. At the arm, that regular bucket read 191 and the priority bucket read 628.

**Why.** The signed shape cannot be included above about 3,078 a second, and the desk has not held a number near that. The 643 gram hop can. Depth 1 on thousands of lanes did not. A stride-40 sample across the old lane range, 308 lanes, found every sample still funded, about 5.6 tKAS each, so this try does not take new coins from the wallet.

**What was true on the network at the arm.** Three public pools read 15,391, 16,953, and 19,098. The desk node processed about 60 to 112 transactions per block over the minute before the arm, compute mass about 104,000 to 187,000 of 500,000. The block had room.

**Result.** Included 1,601 a second over the first 65 seconds, then 1,671, then 1,447. All 4,096 lanes stayed up. Orphans were 0. Ratio of included to submitted was about 1. Local mempool stayed near 1,300 to 3,300. Fee was 150 sompi per gram. Median time from submit to the virtual-chain mark on the first window was 0 ms. The submit call itself took about 310 ms. Four sockets with 128 submits in flight is 512 at once. 512 / 0.310 is about 1,650. That is the same number the run held. The block wait was not the cap. The sender's own submit queue was. The desk node used about one core while this was running, so the machine was not out of CPU.

### 2026-10-07 14:43Z — same lanes, three submit queues

**What.** Stop the single sender. Split those 4,096 lanes into three ranges that do not overlap. Each sender has four sockets and 128 submits in flight. Depth 2. Same fee rule. Still no new coins from the wallet.

**Why.** One sender's submit queue held the rate near 1,650. Three queues on one node are the next measurement. If the node can validate them, the included rate should add. If the node is the cap, each sender will slow down and the total will stay near 1,650.

**Result.** The first 15 seconds added to about 2,450 included a second. The next half minute fell to about 1,845, near 610 on each sender. A block sample in that window was full: compute mass 499,744 of 500,000, about 550 transactions in the block. Public pools were about 23,000 to 28,000. The fee on the hop was still 150 sompi per gram. Other traffic pays more than that, so a full block gives this hop a smaller share. Three queues raised the rate while the block had room, and lost the gain when the block filled.

### 2026-10-07 14:48Z — same three queues, fee 1,600

**What.** Same three lane ranges. Fee fixed at 1,600 sompi per gram, under the sender cap of 2,000, and above the 400/600 traffic already on the public nodes.

**Why.** A 643 gram hop only passes 3,500 if it wins mass inside a full block. At 150 it did not. 3,500 of these hops are about 225,000 grams of a 500,000 gram block.

**Result.** Fee on the arm was 1,600. Over the first measured minute the three senders included 956, 995, and 1,000 a second. Together that is 2,951. Orphans were 0. Ratio was about 0.99. Median inclusion lag was about 0.8 seconds. Each sender had one socket, not four: the extra sockets open only when a sender scans more than 2,000 lanes, and these ranges are shorter. A fourth sender on a fresh range then joined. A 23 second overlap read about 3,344 included a second, and the local pool was about 15,000. The next full minute was about 2,500. By 14:52Z the lanes had started to die and the four together were near 850, while the local pool fell by about 10,000. Public pools stayed near 16,000 to 20,000. The 2,951 minute is the best included reading of this shape so far. It is not over 3,500. The fourth sender raised the short overlap and then the set stalled.

### 2026-10-07 14:55Z — four senders started together, fee 1,600, one socket each

**What.** Stop the stalled set. Start four non-overlapping ranges at the same time. Fee 1,600. One socket each. A lane now waits 90 seconds before it gives up, so a slow minute does not delete it.

**Why.** The 2,951 minute was three fresh senders. The fourth joined late, the local pool rose, and lanes then died. This try asks whether four fresh senders can add before that stall.

**Result.** The measured minute included 338, 341, 332, and 326 a second. Together 1,337. Orphans 0. Median lag about 0.8 seconds. All lanes stayed up. That is worse than the three-sender minute of 2,951. Four full senders at once crowded the node. A follow-up with two local sockets on each of three senders included about 297, 285, and 306 a second, together 888, and one lag tail reached 24 seconds. More local sockets did not raise the rate.

### 2026-10-07 14:58Z — one socket on the desk node, one socket on a public node

**What.** Three senders again. Each keeps a socket on the desk node and opens a second socket on a different public node. Fee stays 1,600. The three public names used here are the three machines that answered, not three names on one machine.

**Why.** At 2,951 included, about 38 percent of the compute mass was this hop and the block was still full. The rest of the mass was other traffic. Those blocks are built from the public mempools. A hop that only enters the desk node can lose the race even at a higher fee. Putting the same hop straight into each public mempool is the test of that.

**Result.** Two of the minutes came back at 1,094 and 1,124 included, with median lag about 0.4 seconds and the local pool falling. The third sender, on the machine that already had the larger pool, stayed weaker. A later 23 second read of all three was about 2,495. Public pools sat near 21,000. This is not over 3,500, and it is under the 2,951 minute that used only the desk node.

## Where it stands

The best included minute on this page is 2,951. Three senders, one socket each on the desk node, fee 1,600, 643 gram hops, orphans 0, for about one minute. Started again at 15:01Z, that shape included 2,627, then 2,458, then 2,236, and one socket then went to 0 while its lanes still counted as live. Four senders at once fell to 1,337. Two local sockets on each sender fell to 888. A signed payment cannot be included above about 3,078 at all.

3,500 of these hops would be about 225,000 grams of a 500,000 gram block. At 15:16Z the block was using about 162,000 of 500,000, so grams were free and the included rate was still far under 3,500. The missing piece is a submit path that stays up. One socket delivered about 1,000 included a second while it was healthy. Three sockets delivered about 3,000 for a minute. A fourth full sender made every socket slower. A socket that shares its connection with the virtual-chain stream can go silent with no reject line. The node was on about one to two cores, so the machine was not out of CPU.

### 2026-10-07 14:26Z — four signed senders, stopped at a public pool of 80,228

**What.** Four signed senders, 3,400 coins, depth 2, fee 1,600 with a cap of 2,400, through the desk node.

**Why.** More signers and a higher fee were a try at a bigger share of a full block.

**Result.** Over 89 seconds the four together were seen-accepted at about 1,870 a second, 0 rejects. Each sender held about 470. That is under the two-sender minute of about 1,920 earlier the same hour, and under 2,207. A public mempool read 80,228 at 14:29:09Z and the four were stopped. The stop is a safety stop. It is not a 3,500 result. Those coin files stay spent.

### Earlier signed tries the same day

Higher fees from 1,018 to 2,400, and sender counts from two to four, moved which of this desk's own transactions got a slot. Seen-accepted stayed about 1,400 to 2,222. Public pools climbed into the 60,000s and the 90,000s when the submit rate ran ahead of inclusion. Stopping the extra senders let the pools fall. None of those windows is over 3,500, and none of them replaces the six-hour 2,207.

Intentions are good; thought process is questionable. STP remains delusional. Si vis pacem, para bellum.

Intern at https://sixpack.wtf/
X: https://x.com/StppStp · GitHub: https://github.com/STP-KAS
