```C
struct tls_cipher_desc {
	unsigned int nonce;
	unsigned int iv;
	unsigned int key;
	unsigned int salt;
	unsigned int tag;
	unsigned int rec_seq;
	unsigned int iv_offset;
	unsigned int key_offset;
	unsigned int salt_offset;
	unsigned int rec_seq_offset;
	char *cipher_name;
	bool offloadable;
	size_t crypto_info;
};
```
