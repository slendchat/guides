There are bits of data written on a drive. There is some sort of recipe book that lists how to construct files and directories from those bits and pieces: take five bytes from here (1), glue it to 1000 bytes from there (2) and append 600 bytes (3) here to build cat-standing-up.jpeg

Snapshot is that recipe book. When you take snapshot — you create a readonly copy of that recipe book. Now you go and modify the cat-standing-up.jpg to photoshop funny hat on his silly face. Let’s assume you ended up modifying some portion of that file and the rest of the file did it change. lets assume it was block (2)

Because original bits and pieces that make the file are still referenced in the previous snapshot the system creates a copy of the blocks (2) you are about to modify before letting you save the changes there. This is called CoW — Copy on Write. Let’s call this copied data (2a). Now your current snapshot references blocks (1),(2a),(3) and your old snapshot still references (1),(2),(3).

See what happened here? Even though you have access to both versions of the file it does not take double disk space — only difference is stored and unchanged blocks are reused.

What does it mean practically:

- taking snapshot is instantaneous — only cookbook is copied, not actual data
    
- replicating snapshots is efficient — only cookbook and new blocks it references are transferred, not entire data
    
- restoring snapshot is also quick — you replace current recipe book with preciously saved one. This gives you instant way-back machine and versioning at minimum possible cost.
    
- you should not defragment that volume. Why — exercise for the reader. (Hint — moooo)
    

So, is it a backup? Sort of. It is perfectly fine local backup. It will protect your against accidental change, malicious corruption, ransomware, etc.

It will not protect you against flood, fire, physical theft, hardware failure. So you still need offsite backup.

Replicating snapshots to the cloud may not be the best way to accomplish that — you would want to use tools like HyperBackip which will operate on a current filesystem (current snapshot) and create deduplicated, compressed, and encrypted datastore at the destination: this will be faster (compression), take little space (deduplication), and secure (client side encryption)— you don’t want your data in the plain text on a third party cloud you don’t control.

![[snapshots.gif]]


https://habr.com/ru/companies/netapp/articles/112367/
