# Profanity2使用教程

先clone到本地

`git clone https://github.com/1inch/profanity2`

然进目录后`make`一下，生成 ./profanity.x64文件

准备好后进行下面四步：

1. 首先用openssl生成一对本地公私钥，后续靓号通过对此账户偏移得到

   ```
   openssl ecparam -genkey -name secp256k1 -text -noout -outform DER | xxd -p -c 1000 | sed 's/41534e31204f49443a20736563703235366b310a30740201010420/Private Key: /' | sed 's/a00706052b8104000aa144034200/\'$'\nPublic Key: /'
   ```

   此时得到公钥A，私钥A

   ```
   Private Key: ed6742c82bb51c021dab68f5201dea8a07889c1425c25074a3b33e61b8163b4a
   Public Key: 04b49c2a742c69e71f567bab93bd21e40935538a5bdf9142003eeb66fcad86018a99ad4d2e090ebcccba4670fc6b6dcda2281822dcf1f4b2e56b032de0cd9ae9c7
   ```

   

2. 然后选择自己的靓号，并输入公钥A，去掉开头的04，开始计算偏移量，以找到目标靓号

   ```
   ./profanity2.x64 --matching 12345XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX -z b49c2a742c69e71f567bab93bd21e40935538a5bdf9142003eeb66fcad86018a99ad4d2e090ebcccba4670fc6b6dcda2281822dcf1f4b2e56b032de0cd9ae9c7(去掉开头04的公钥A)
   ```

   

3. 此时得到偏移量和靓号地址

   ```
    Time:    14s Score:  3 Private: 0x0000759cb1683740ead41729c9e441c9ea2e576218f0e4e1b60e4dab610fc88b Address: 0x12345eee5a7e4b7070d748ce15baebc82d135ce6
   Total: 86.507 MH/s - GPU0: 86.507 MH/s
   ```

   

4. 把偏移量加到最开始的私钥上，得到靓号的私钥

   

   ```
   (echo 'ibase=16;obase=10' && (echo '(ed6742c82bb51c021dab68f5201dea8a07889c1425c25074a3b33e61b8163b4a + 0000759cb1683740ead41729c9e441c9ea2e576218f0e4e1b60e4dab610fc88b) % FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFEFFFFFC2F' | tr '[:lower:]' '[:upper:]')) | bc
   
   
   ```

   

   解释一下个部分代表是什么？

   ```
   (echo 'ibase=16;obase=10' && (echo '(ed6742c82bb51c021dab68f5201dea8a07889c1425c25074a3b33e61b8163b4a（私钥A） + 0000759cb1683740ead41729c9e441c9ea2e576218f0e4e1b60e4dab610fc88b（偏移量）) % FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFEFFFFFC2F' | tr '[:lower:]' '[:upper:]')) | bc 
   ED67B864DD1D5343087F801EEA022C53F1B6F3763EB3355659C18C0D192603D5 （靓号私钥）
   ```

   