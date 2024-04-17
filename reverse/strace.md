# Pipe Random Data And watch system calls
cat /dev/urandom | strace ./<file> |& cut -d\( -f1 

# Stace to file

strace --output result ./<file> 

memfd_create(":^)", 0)                  = 3

it creates a file :^) inside the process /proc/pid/fd/3

We can then extract it 
and observe it in ghidra

kali      125331  3.8  0.0  13780  7432 pts/0    Ss   12:11   0:00 /usr/bin/zsh
kali      125548  0.0  0.0   2516  1280 pts/0    S+   12:12   0:00 ./biobundle
kali      125573  0.0  0.0  10976  4352 pts/10   R+   12:12   0:00 ps aux

┌──(kali㉿kali)-[~/Desktop/HTB-University/rev_biobundle]
└─$ ls -lha /proc/125548/fd
total 0
dr-x------ 2 kali kali  4 Dec  8 12:12 .
dr-xr-xr-x 9 kali kali  0 Dec  8 12:12 ..
lrwx------ 1 kali kali 64 Dec  8 12:13 0 -> /dev/pts/0
lrwx------ 1 kali kali 64 Dec  8 12:13 1 -> /dev/pts/0
lrwx------ 1 kali kali 64 Dec  8 12:13 2 -> /dev/pts/0
lrwx------ 1 kali kali 64 Dec  8 12:12 3 -> '/memfd::^) (deleted)'

cat /proc/125548/fd/3 > extracted.elf

https://gchq.github.io/CyberChef/#recipe=From_Hex('Auto')Reverse('Character')&input=CgoKMHg3ZDcyMzMKMHg2YzMwMzA2MzVmNzQ3NTYyCjB4NWYzNTYyMzE2YzVmNjMzMQoweDc0MzQ3NDczN2I0MjU0NDg
HTB{st4t1c_l1b5_but_c00l3r}
----
Breakpoint 1, 0x0000555555555187 in main ()
(gdb) print (char[43])arr
$1 = "\234\226\275\257\223Ô`\242\321\302Ϝ\243\246h\224\301\327\254\226\223\223\237Ҕ\247֏\240\243\241\243V\236\000\000\000\000\000"

\234\226\275\257\223Ô`\242\321\302Ϝ\243\246h\224\301\327\254\226\223\223\237Ҕ\247֏\240\243\241\243V\236

234 226 275 257 223 303 224 140 242 321 302 317 234 243 246 150 224 301 327 254 226 223 223 237 322 224 247 326 217 240 243 241 243 126 236
