# Alg Type

```C
struct af_alg_type {
	void *(*bind)(const char *name, u32 type, u32 mask);
	void (*release)(void *private);
	int (*setkey)(void *private, const u8 *key, unsigned int keylen);
	int (*setentropy)(void *private, sockptr_t entropy, unsigned int len);
	int (*accept)(void *private, struct sock *sk);
	int (*accept_nokey)(void *private, struct sock *sk);
	int (*setauthsize)(void *private, unsigned int authsize);

	struct proto_ops *ops;
	struct proto_ops *ops_nokey;
	struct module *owner;
	char name[14];
};

struct alg_type_list {
	const struct af_alg_type *type;
	struct list_head list;
};

static LIST_HEAD(alg_types);
static DECLARE_RWSEM(alg_types_sem);
```

# Registered types

```C
static const struct af_alg_type algif_type_aead = {
	.bind		=	aead_bind,
	.release	=	aead_release,
	.setkey		=	aead_setkey,
	.setauthsize	=	aead_setauthsize,
	.accept		=	aead_accept_parent,
	.accept_nokey	=	aead_accept_parent_nokey,
	.ops		=	&algif_aead_ops,
	.ops_nokey	=	&algif_aead_ops_nokey,
	.name		=	"aead",
	.owner		=	THIS_MODULE
};

static const struct af_alg_type algif_type_hash = {
	.bind		=	hash_bind,
	.release	=	hash_release,
	.setkey		=	hash_setkey,
	.accept		=	hash_accept_parent,
	.accept_nokey	=	hash_accept_parent_nokey,
	.ops		=	&algif_hash_ops,
	.ops_nokey	=	&algif_hash_ops_nokey,
	.name		=	"hash",
	.owner		=	THIS_MODULE
};

static const struct af_alg_type algif_type_rng = {
	.bind		=	rng_bind,
	.release	=	rng_release,
	.accept		=	rng_accept_parent,
	.setkey		=	rng_setkey,
#ifdef CONFIG_CRYPTO_USER_API_RNG_CAVP
	.setentropy	=	rng_setentropy,
#endif
	.ops		=	&algif_rng_ops,
	.name		=	"rng",
	.owner		=	THIS_MODULE
};

static const struct af_alg_type algif_type_skcipher = {
	.bind		=	skcipher_bind,
	.release	=	skcipher_release,
	.setkey		=	skcipher_setkey,
	.accept		=	skcipher_accept_parent,
	.accept_nokey	=	skcipher_accept_parent_nokey,
	.ops		=	&algif_skcipher_ops,
	.ops_nokey	=	&algif_skcipher_ops_nokey,
	.name		=	"skcipher",
	.owner		=	THIS_MODULE
};
```

**alg compression missing**
