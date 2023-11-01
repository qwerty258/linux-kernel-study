# Global alg list

```C
crypto_alg_list
```

like C++ `struct crypto_larval` is child class of `struct crypto_alg`

```C
struct crypto_alg {
	struct list_head cra_list;
	struct list_head cra_users;

	u32 cra_flags;
	unsigned int cra_blocksize;
	unsigned int cra_ctxsize;
	unsigned int cra_alignmask;

	int cra_priority;
	refcount_t cra_refcnt;

	char cra_name[CRYPTO_MAX_ALG_NAME];
	char cra_driver_name[CRYPTO_MAX_ALG_NAME];

	const struct crypto_type *cra_type;

	union {
		struct cipher_alg cipher;
		struct compress_alg compress;
	} cra_u;

	int (*cra_init)(struct crypto_tfm *tfm);
	void (*cra_exit)(struct crypto_tfm *tfm);
	void (*cra_destroy)(struct crypto_alg *alg);
	
	struct module *cra_module;
} CRYPTO_MINALIGN_ATTR;


struct crypto_larval {
	struct crypto_alg alg;
	struct crypto_alg *adult;
	struct completion completion;
	u32 mask;
	bool test_started;
};
```
