> **Experimental. We are just trying this.**
>
> Good intentions, shaky hands. STP does not know what he is doing. We test, we write down what we think we saw, and that is the whole product. A number here is not the truth. A chart is not the truth. Any other sentence that sounds sure of itself is not the truth either. Do not count any of it as a claim.
>
> [Disclaimer](DISCLAIMER.md)

Thank you, Kaspa Pulse (@gokugalax), for the guidance and the input over this stretch, from 4 Oct 2026 on. The 7 Oct 2026 wording stays: sign-and-send processes are senders; runner is the setup; bot is reserved for the operator.

# Desk try for 3500 included transactions a second

Kaspa Testnet-10 only. Every clock on this page is UTC.

The other notes stay separate. The 9 or 13 Oct paste-in is [GROK-BUILD-PROMPT.md](https://github.com/STP-KAS/tn10-storm-throughput-questions/blob/main/plan/GROK-BUILD-PROMPT.md). The desk runs, oldest first, are [tn10-build-desk-tps](https://github.com/STP-KAS/tn10-build-desk-tps). Why a signed payment stops near 3,080 is [what-limits-tx-rate](https://github.com/STP-KAS/what-limits-tx-rate). The questions and the empty result sections are [tn10-storm-throughput-questions](https://github.com/STP-KAS/tn10-storm-throughput-questions).

## What

The bar on this page is an included rate well over 3,500 transactions a second on Testnet-10. Included means the sender saw the transaction in the virtual chain. A submit acknowledgement is a different number. This page is not the 9 Oct or 13 Oct storm, and it does not move that storm's fee.

The long included hold in [tn10-build-desk-tps](https://github.com/STP-KAS/tn10-build-desk-tps) is 2,207 seen-accepted transactions a second for 6 hours 1 minute, from 2026-10-06T23:53:27 UTC to 2026-10-07T05:54:53 UTC, at fee 200/300. The published 6,321 is submit-OK for 20 seconds. Seen-accepted in that same window is about 1,900 a second.

## Why a signed payment stops near 3,080

rusty-kaspa v2.1.0 gives each block 500,000 compute mass. Live Testnet-10 aims at about 10 blocks a second. A signed one-input, one-output payment is about 1,624 grams. One signature is 1,000 grams before the bytes are counted.

500,000 / 1,624 is about 308 of those payments in one block. At 10 blocks a second that shape is about 3,078 included transactions a second. A worker, a miner, a second RPC name, or a higher fee does not add grams. The same reading is in [what-limits-tx-rate](https://github.com/STP-KAS/what-limits-tx-rate).

On 7 Oct 2026 UTC the desk node was already taking full blocks of that shape: about 304 to 307 transactions, compute mass about 497,000 of 500,000, near 3,050 to 3,070 a second for the network. This desk's own seen-accepted share of those blocks stayed about 1,400 to 2,222.

## Why a lighter hop can pass 3,500

An anyone-can-spend hop with no signature measured 643 grams. 500,000 / 643 is 777 of those hops in one block. At 10 blocks a second the mass ceiling is 7,770 included transactions a second. 3,500 of them need about 2.25 million grams a second, which is under the 5 million gram budget. The mass is not the thing in the way. The sender pipeline is.

The redeem is a short script: push a lane number, drop it, leave true. The last saved hold of this shape, depth 1 and 8,192 lanes, included 127.7 a second over its measured minute, with a median lag of 8.3 seconds. Earlier steps of the same shape climbed until about 2,000 lanes and then flattened under 2,700. Depth 1 waits for each hop before the next one, so the send rate cannot run ahead of inclusion.

## What this test will not do

It will not spend coins a live signer is already using. It will not start a second node on this machine. It will not mine. It will not clear an older halt. It stops itself if a public mempool reaches 80,000. A public node started with a low memory scale can die at 100,001. Several public names are still one machine.

## Kaspa Pulse, 7 Oct 2026

Kaspa Pulse ([@gokugalax](https://x.com/gokugalax)) asked, in messages from 19:23 to 19:54 UTC, that the 18:52–19:23 UTC window and the 2,750 figure be read from the log before anyone calls a ceiling. The note is [PULSE-WINDOW-7-OCT.md](https://github.com/STP-KAS/tn10-storm-throughput-questions/blob/main/plan/PULSE-WINDOW-7-OCT.md). The log does not cover 18:52–19:23 UTC. The 2,753 `included_s` sum at 15:20:32 UTC and mempool 9747 at 15:25:33 UTC are different minutes in `status.log`. Neither number is a ceiling. The 3,500 bar on this page is unchanged. A pending dry run for 8 Oct 2026, not the storm, is in [TESTDAY.md](https://github.com/STP-KAS/tn10-storm-throughput-questions/blob/main/plan/TESTDAY.md). A process that signs and sends is a sender. The runner is the whole setup.

## Where it stands

The best included minute on this page is 2,951, from three depth-2 senders. The best single socket is 1,636, from one depth-8 sender, still at 1,413 and 1,343 in the next two minutes. A second depth-8 sender did not add. Raising that socket from 128 in-flight submits to 256 dropped it to 859. Three depth-4 senders together included about 600. After that, one depth-8 sender included 144, and the submit call sat near 580 ms. Three depth-2 sockets with the chain stream on its own socket included 2,753 before the node slowed. A signed payment cannot be included above about 3,078 at all. At 16:16 UTC the same depth-8 socket was tried again and stopped after about 16 seconds. Submit stayed near 400 to 500 a second, the block was near the mass ceiling, and the node logged initial block download. At 16:27 UTC the node was steady. That socket then included about 307 a second, with submit matching inclusion. A full minute on 540 lanes included 46, while the submit call itself was 43 ms. 3,500 has not been read.

3,500 of these hops would be about 225,000 grams of a 500,000 gram block. At 15:16 UTC the block was using about 162,000 of 500,000. In the slow stretch near 15:47 UTC a block was using about 86,000. Grams were free both times. Depth 2 tops a healthy socket near 1,000 included a second, and three of those reached 2,951 once. Depth 8 raised one healthy socket to 1,636, with the submit call near 80 ms. The same shape later submitted in about 580 ms and included 144. The missing piece is a submit call that stays near 80 ms or below while more than one deep socket is running. A wider in-flight window made the call slower. The node was on about one to two cores, so the machine was not out of CPU.

## Journal

Oldest first. Each entry is one try. A number is a reading from that window.

### Earlier signed tries the same day

Higher fees from 1,018 to 2,400, and sender counts from two to four, moved which of this desk's own transactions got a slot. Seen-accepted stayed about 1,400 to 2,222. Public pools climbed into the 60,000s and the 90,000s when the submit rate ran ahead of inclusion. Stopping the extra senders let the pools fall. None of those windows is over 3,500, and none of them replaces the six-hour 2,207.

### 2026-10-07 14:26 UTC — four signed senders, stopped at a public pool of 80,228

**What.** Four signed senders, 3,400 coins, depth 2, fee 1,600 with a cap of 2,400, through the desk node.

**Why.** More signers and a higher fee were a try at a bigger share of a full block.

**Result.** Over 89 seconds the four together were seen-accepted at about 1,870 a second, 0 rejects. Each sender held about 470. That is under the two-sender minute of about 1,920 earlier the same hour, and under 2,207. A public mempool read 80,228 at 14:29:09 UTC and the four were stopped. The stop is a safety stop. It is not a 3,500 result. Those coin files stay spent.

### 2026-10-07 14:35 UTC — lighter hop, depth 2, lanes that were already funded

**What.** Resume 4,096 anyone-can-spend lanes that already hold coins. Depth 2, so a lane may have two hops in flight. Submit through this desk's own synced node. Fee stays the sender's rule: 1.5 times the regular bucket, floor 150, cap 2,000. At the arm, that regular bucket read 191 and the priority bucket read 628.

**Why.** The signed shape cannot be included above about 3,078 a second, and the desk has not held a number near that. The 643 gram hop can. Depth 1 on thousands of lanes did not. A stride-40 sample across the old lane range, 308 lanes, found every sample still funded, about 5.6 tKAS each, so this try does not take new coins from the wallet.

**What was true on the network at the arm.** Three public pools read 15,391, 16,953, and 19,098. The desk node processed about 60 to 112 transactions per block over the minute before the arm, compute mass about 104,000 to 187,000 of 500,000. The block had room.

**Result.** Included 1,601 a second over the first 65 seconds, then 1,671, then 1,447. All 4,096 lanes stayed up. Orphans were 0. Ratio of included to submitted was about 1. Local mempool stayed near 1,300 to 3,300. Fee was 150 sompi per gram. Median time from submit to the virtual-chain mark on the first window was 0 ms. The submit call itself took about 310 ms. Four sockets with 128 submits in flight is 512 at once. 512 / 0.310 is about 1,650. That is the same number the run held. The block wait was not the cap. The sender's own submit queue was. The desk node used about one core while this was running, so the machine was not out of CPU.

### 2026-10-07 14:43 UTC — same lanes, three submit queues

**What.** Stop the single sender. Split those 4,096 lanes into three ranges that do not overlap. Each sender has four sockets and 128 submits in flight. Depth 2. Same fee rule. Still no new coins from the wallet.

**Why.** One sender's submit queue held the rate near 1,650. Three queues on one node are the next measurement. If the node can validate them, the included rate should add. If the node is the cap, each sender will slow down and the total will stay near 1,650.

**Result.** The first 15 seconds added to about 2,450 included a second. The next half minute fell to about 1,845, near 610 on each sender. A block sample in that window was full: compute mass 499,744 of 500,000, about 550 transactions in the block. Public pools were about 23,000 to 28,000. The fee on the hop was still 150 sompi per gram. Other traffic pays more than that, so a full block gives this hop a smaller share. Three queues raised the rate while the block had room, and lost the gain when the block filled.

### 2026-10-07 14:48 UTC — same three queues, fee 1,600

**What.** Same three lane ranges. Fee fixed at 1,600 sompi per gram, under the sender cap of 2,000, and above the 400/600 traffic already on the public nodes.

**Why.** A 643 gram hop only passes 3,500 if it wins mass inside a full block. At 150 it did not. 3,500 of these hops are about 225,000 grams of a 500,000 gram block.

**Result.** Fee on the arm was 1,600. Over the first measured minute the three senders included 956, 995, and 1,000 a second. Together that is 2,951. Orphans were 0. Ratio was about 0.99. Median inclusion lag was about 0.8 seconds. Each sender had one socket, not four: the extra sockets open only when a sender scans more than 2,000 lanes, and these ranges are shorter. A fourth sender on a fresh range then joined. A 23 second overlap read about 3,344 included a second, and the local pool was about 15,000. The next full minute was about 2,500. By 14:52 UTC the lanes had started to die and the four together were near 850, while the local pool fell by about 10,000. Public pools stayed near 16,000 to 20,000. The 2,951 minute is the best included reading of this shape so far. It is not over 3,500. The fourth sender raised the short overlap and then the set stalled.

### 2026-10-07 14:55 UTC — four senders started together, fee 1,600, one socket each

**What.** Stop the stalled set. Start four non-overlapping ranges at the same time. Fee 1,600. One socket each. A lane now waits 90 seconds before it gives up, so a slow minute does not delete it.

**Why.** The 2,951 minute was three fresh senders. The fourth joined late, the local pool rose, and lanes then died. This try asks whether four fresh senders can add before that stall.

**Result.** The measured minute included 338, 341, 332, and 326 a second. Together 1,337. Orphans 0. Median lag about 0.8 seconds. All lanes stayed up. That is worse than the three-sender minute of 2,951. Four full senders at once crowded the node. A follow-up with two local sockets on each of three senders included about 297, 285, and 306 a second, together 888, and one lag tail reached 24 seconds. More local sockets did not raise the rate.

### 2026-10-07 14:58 UTC — one socket on the desk node, one socket on a public node

**What.** Three senders again. Each keeps a socket on the desk node and opens a second socket on a different public node. Fee stays 1,600. The three public names used here are the three machines that answered, not three names on one machine.

**Why.** At 2,951 included, about 38 percent of the compute mass was this hop and the block was still full. The rest of the mass was other traffic. Those blocks are built from the public mempools. A hop that only enters the desk node can lose the race even at a higher fee. Putting the same hop straight into each public mempool is the test of that.

**Result.** Two of the minutes came back at 1,094 and 1,124 included, with median lag about 0.4 seconds and the local pool falling. The third sender, on the machine that already had the larger pool, stayed weaker. A later 23 second read of all three was about 2,495. Public pools sat near 21,000. This is not over 3,500, and it is under the 2,951 minute that used only the desk node.

### 2026-10-07 15:01 UTC — the 2,951 shape again, then one socket went quiet

**What.** Start the same three ranges again. Fee 1,600. Depth 2. One submit socket each on the desk node. No new coins from the wallet.

**Why.** 2,951 was one minute. A second minute of the same shape would show whether that number holds. The block does not have to be full for this to be worth running.

**Result.** The first measured minute included 706, 936, and 986 a second. Together 2,627. The next two minutes were 2,458 and 2,236. Orphans were 0. Ratio stayed about 1. All lanes stayed up. One sender was already the slow one: its submit call took about 214 ms, against 12 to 18 ms on the other two. By 15:13 UTC that slow sender was at 8 a second, then at 0, with every lane still marked live and no reject line. The other two fell through about 220 to about 160 and about 57. Local mempool fell from a few thousand to the tens and the hundreds. In the same later window the desk node processed blocks at about 162,000 compute grams of 500,000, and its own virtual-chain rate was about 834 transactions a second, with about 181 a second arriving by RPC. Public pools were about 14,000 to 17,000. The 2,951 shape did not hold. A socket can go silent while its lanes still count as live. Grams were not the cap in that window. 3,500 was not reached.

### 2026-10-07 15:19 UTC — chain updates on their own socket

**What.** Three fresh ranges that this session had not hopped. Fee 1,600. Depth 2. The virtual-chain stream sits on its own socket. Submits sit on a second socket, one per sender. A submit that does not return in 4 seconds is treated as a dead socket and the sender reconnects.

**Why.** At 15:13 UTC a sender went to 0 included while every lane still counted as live, and the log had no reject. That fits one socket blocked on the chain stream, so submits never return. A separate submit socket, plus a timeout, is the test. The block at the arm was nearly empty, about 51 in the local pool, so a short inclusion wait would also have room to show up.

**Result.** The measured minute included 921, 885, and 947 a second. Together 2,753. Orphans 0. Ratio about 0.99. No lane died. Median submit was 13, 21, and 11 ms. The tail was still about 245 ms. Median lag was 0.8, 0.3, and 0.6 seconds. Local pool moved from about 2,100 to about 4,500. All three sockets stayed healthy, unlike 15:01 UTC, and the total is still under the 2,951 minute. Separating the chain stream did not make a socket faster than about 950 included a second. 3,500 was not reached.

### 2026-10-07 15:24 UTC — a fourth sender with 256 submits in flight

**What.** Leave the three senders from the 15:19 UTC minute running. Add a fourth range, fee 1,600, one submit socket, 256 submits allowed in flight instead of 128.

**Why.** Each healthy socket was including about 900 a second with a submit call of about 11 to 21 ms at the median and about 245 ms at the tail. 128 in flight at a tenth of a second is about 1,000 a second, which matches the reading. A wider in-flight window on one more sender was the try for the missing 500.

**Result.** The fourth sender's measured minute included 539 a second. Median submit was 19 ms. Median lag was 0.8 seconds. Orphans were 0. While it ran, the original three fell to about 340, 180, and 240. A few seconds later the four together were about 980. The fourth was stopped. The three did not climb back; they stayed near 300 each, and the local pool stayed near 9,700. 256 in flight did not raise a sender, and a fourth full sender crowded the set again. Not over 3,500.

### 2026-10-07 15:27 UTC — submit on the three public machines, chain notice stays local

**What.** Three senders. Each submits only to one of the three public machines. The desk node only listens for the virtual chain. Fee 1,600. Depth 2.

**Why.** The desk node was the insert path for every hop that reached 2,951. A public machine has its own pool. Three machines could insert at once if the block still has grams.

**Result.** Two machines included 907 and 925 in the first minute. Median lag was 0.2 and 0.3 seconds. Median submit was 117 ms and 48 ms. Orphans 0. The third machine included 16 a second, with 358 orphans and a median submit of 782 ms. It was stopped. The two that worked did 840 and 959 in the next minute, then 519 and 727. A local sender added beside them, on a range this round had barely touched, included 1,068 with a 12 ms submit. An older range resumed 1,365 lanes and submitted none: the coins were still over the keep-alive floor, and under that floor plus one hop fee, so the hop refused. The set did not add up to the local-only minutes. Not over 3,500.

### 2026-10-07 15:35 UTC — two more local sockets beside a sender that was already at 1,068

**What.** Keep the local sender that had just included 1,068. Start two neighboring ranges on the desk node, same fee, depth 2, one socket each.

**Why.** 1,068 on one socket is above the earlier 950. Two more at that pace would clear 3,500. Adding them after the first is in its hold is the shape that once overlapped near 3,344 for 23 seconds.

**Result.** The two new minutes included 382 and 421. Median submit was about 350 ms. The sender that had been at 1,068 fell to about 540. Together about 1,330. The node answered slowly as soon as the extra sockets arrived. Not over 3,500.

### 2026-10-07 15:36 UTC — depth 8, one sender

**What.** One sender, 1,365 lanes, fee 1,600, one submit socket. A lane may keep eight hops in flight instead of two. The chain stream stays on its own socket.

**Why.** At depth 2 a lane submits one hop and then waits out the inclusion notice. The measured wait was about 0.3 to 0.8 seconds, and a socket topped out near 1,000 included a second. Eight in flight lets the next hops sit in the pool while the notice is still on the way, so a block can take more than one hop from the same lane before the sender hears about the first.

**Result.** The measured minute included 1,636 a second. Submitted 1,641. Ratio 0.997. Orphans 0. No lane died. Median lag was 0 ms, so the hop was already in the virtual chain by the time the sender checked. Median submit was 76 ms and the tail was 84 ms. The local pool stayed near 1,500 to 1,800. The next two minutes were 1,413 and 1,343. A second sender at the same depth, on another 1,365 lanes, included 490 in its minute, with a submit time of about 270 ms. The first sender was at 1,343 in that same stretch, and about 1,140 in the short window after the second sender was stopped. Two deep senders did not add. 1,636 is the best single socket on this page. It is not over 3,500.

### 2026-10-07 15:43 UTC — a wider pipe, then the submit call slowed down

**What.** One sender on about 4,095 lanes, depth 8, 256 submits in flight. Then the same 1,365-lane range that had just included 1,636, still depth 8, with 256 in flight instead of 128. Then three senders at depth 4 and 128 in flight, started together. Then one depth-8 sender again, after the others were stopped and the node had a short rest.

**Why.** 1,636 on one socket matched about 128 submits in flight at about 80 ms each. More lanes, more in-flight submits, or a middle depth on three sockets was the try to move that number to 3,500.

**Result.** About 4,095 lanes at 256 in flight included 213 a second. The median submit was 1,144 ms. The 1,365-lane range at 256 in flight included 859, with a median submit of 290 ms. That is worse than the same range at 128 in flight. Three depth-4 senders included 228, 191, and 181. Together about 600. The median submit was about 530 to 630 ms. One of them, left running alone, stayed near 250. After a short rest, one depth-8 sender included 144, with a median submit of 583 ms. Orphans were 0. The local pool was a few hundred to about 2,000. A block in that slow stretch carried about 86,000 compute grams of 500,000, so the grams were free. The submit call had moved from about 80 ms to about 500 to 1,100 ms. The desk node was also revalidating a few hundred high-priority transactions and logging blocks orphaned and then accepted again. 3,500 was not reached. These senders were stopped.

### 2026-10-07 16:16 UTC — the same depth-8 socket, stopped when the node fell behind

**What.** One sender, the same shape as the 1,636 minute: depth 8, 1,365 lanes, 128 submits in flight, one local socket, fee 1,600. The node had taken no local submits for about two and a half hours.

**Why.** That shape is the fastest single socket on this page, and only while the submit call stays near 80 ms. This try checked whether that call had come back.

**Result.** Stopped at about 16 seconds. It is not a measured minute. In the first 10 seconds it submitted 4,163 and counted 2,539 included, about 416 submitted a second and 254 included. Across the 16 seconds the submit rate stayed near 400 to 500 a second. Inclusion was still catching up when the sender stopped. The local pool moved from 1 to about 3,800. In the same window the node recorded about 406 RPC inserts a second, a block at about 481,000 compute grams of 500,000, and then initial block download. RPC inserts went back to 0 after the stop. Orphans were not scored. 3,500 was not read.

### 2026-10-07 16:27 UTC — the submit call is quick, and the included rate stays near 300

**What.** The node was synced again, with blocks near 130,000 to 190,000 compute grams of 500,000. One depth-8 sender, 128 in flight, on the 1,365 lanes from the 1,636 minute. Then 540 lanes at 32 in flight. Then those 540 lanes at 128 in flight for a full minute. Then the 1,365 lanes again at 128 in flight.

**Why.** The 16:16 UTC try had been cut off while the node was catching up. This set asked whether one socket could hold a high rate once the node was steady.

**Result.** On the 1,365 lanes, inclusion stayed near 307 a second for about 53 seconds, and submit matched it. The node stayed synced, and its RPC intake was about 300 a second. The 540-lane minute included 46.2 a second and submitted 113.7. The median submit call was 43 ms. The median wait from submit to inclusion was 549 ms, and the slow tail was about 28 seconds. Orphans were 0. The local pool climbed by about 2,900. Included over submitted was 0.41, so that minute is not a held rate. The 32-in-flight try burst and then went quiet, and was stopped before a minute. 3,500 was not read. The senders are stopped.

Intentions are good; thought process is questionable. STP remains delusional. Si vis pacem, para bellum.

Intern at https://sixpack.wtf/
X: https://x.com/StppStp · GitHub: https://github.com/STP-KAS
