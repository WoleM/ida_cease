### ida_cease
Long story short, wanted to reverse how the endurance matches champions are selected at the towers of MK,
found an idb for sega rom which was created with a 20 year blacklisted license by Rico Baumgart with ID 48-325F-7034-FF.
Even with an active PRO license u are unable to open a blacklisted created idb.

To achieve opening a blacklisted database we patch the code thats always past the MD5s and looks like this:
```assembly
mov     rdx, rbx
lea     rcx, [rsp+0A8h+var_88]
call    MD5Update
lea     rdx, [rsp+0A8h+var_88]
lea     rcx, [rsp+0A8h+var_28]
call    MD5Final
mov     rdx, [rsp+0A8h+var_20]
lea     rax, qword_10315B00
mov     r8, [rsp+0A8h+var_28]
xor     ecx, ecx
cmp     rdx, [rax+8]
```
for pre7 ida with its custom extension modules:\
pattern:E8 ? ? ? ? B0 01 5E C3		<--	 74 ? ? ? ? B0 01 5E C3\
patch: 0003549F: EB 74

for post7:\
48 3B 50 08 EB 00 	    <--		48 3B 50 08 74 2A\
EB 00 48 83 C3 10 	    <--		74 3A 48 83 C3 10 \
001D94FB: EB 74\
001D94FC: 00 2A\
001D962B: EB 74\
001D962C: 00 3A

representation:	patched		<--	original

This repo contains no copyright material and the content is secured by the CJEU 91/250 A5(1)
