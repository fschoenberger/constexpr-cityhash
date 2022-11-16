# constexprhash
Header-only `constexpr` and `consteval` implementations of common non-cryptographic hash functions.

## Google's cityhash

Right now, this library only includes [Google's Cityhash](https://github.com/google/cityhash). If you study the code, 
you can quickly see that it is virtually the same compared to Google's.

The code is written for C++23 because it uses `std::byteswap`. 

This is first and foremost a personal library, and some stuff in there is really quick-and-dirty.

### Future Work
- [ ] Convert to module instead of header
- [ ] Add consteval overloads
- [ ] Clean up visibility and make only the right functions visible to outside callers
- [ ] Clean up tests
