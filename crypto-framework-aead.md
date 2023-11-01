```C
struct crypto_aead *crypto_alloc_aead(const char *alg_name, u32 type, u32 mask);
    static inline void *crypto_alloc_tfm(const char *alg_name, const struct crypto_type *frontend, u32 type, u32 mask);
        void *crypto_alloc_tfm_node(const char *alg_name, const struct crypto_type *frontend, u32 type, u32 mask, int node);
```
