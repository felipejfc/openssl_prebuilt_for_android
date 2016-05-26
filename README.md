# Openssl 1.0.2h prebuilt for android (aermeabi, armeabi_v7)

## Usage

Just link it statically using your Android.mk file:
```
LOCAL_STATIC_LIBRARIES += ssl_static
LOCAL_STATIC_LIBRARIES += crypto_static
```
## Troubleshooting

If you get a complaint from NDK about bsd_signal not being defined, you can solve it by putting this code into any of your .c or .cpp files:

**.c :**
 ```
//Dirty hack for making it possible to link openssl statically against libpomelo2 on android
//Be warned that I don't know the implications of doing that
typedef void (*sighandler_t)(int);
sighandler_t __unused bsd_signal(int __unused signum, sighandler_t __unused handler);
sighandler_t __unused bsd_signal(int __unused signum, sighandler_t __unused handler) {
  return 0;
}
```
**.cpp :** 
```
//Dirty hack for making it possible to link openssl statically against libpomelo2 on android
//Be warned that I don't know the implications of doing that
extern "C" {
  typedef void (*sighandler_t)(int);
  sighandler_t __unused bsd_signal(int __unused signum, sighandler_t __unused handler);
}

sighandler_t __unused bsd_signal(int __unused signum, sighandler_t __unused handler) {
  return 0;
}
```
Be aware that this is a dirty hack and that I do not know it's implications.
