# Build

## Mbed TLS Library

Build the Mbed TLS lib for the desired platform. Instructions here: https://github.com/ARMmbed/mbedtls
Once built, run `cp cp mbedtls-2.7.0/library/libmbedtls.a ngrok-c/libpolarssl-linux.a` to copy Mbed TLS lib (formerly Polar SSL) into the `ngrok-c` build directory. The build script is looking for `libpolarssl-linux.a` in the root dir.

## ngrok-c

Instructions below are for Linux. For OSX, Windows, and others see: https://github.com/dosgo/ngrok-c

```
cd ngrok-c
./build.sh
```

This will produce an `ngrokc` executable in the `bin` directory.

# Usage

## Server (`ngrokd`)

Instructions are for self-hosted `ngrok`.

On the server side you can use the vanilla `ngrokd` built from source: https://github.com/inconshreveable/ngrok
Run the server without specifying any SSL certs, but do specify a password of your choice:

```
ngrokd -domain="yourdomain.com" -pass="password"
```

# Client (HTTP/HTTPS/WebSocket)

```
ngrokc -SER[Shost:yourdomain.com,Sport:4443,Password:password] -AddTun[Type:https,Lhost:127.0.0.1,Lport:80,Sdname:subdomain]
```

Replace `subdomain` with your permanent subdomain URL (or make something up, like "test"). Replace `yourdomain.com` with your domain. Replace the `https` with `http` if you don't need SSL.

Further instructions can be found here: https://github.com/dosgo/ngrok-c
This fork will be periodically updated with the original to stay parallel.

**NOTE ABOUT WEBSOCKETS**: The vanilla `ngrokd` has a problem with secure WebSockets, so I also have a fork here that fixes the problem: https://github.com/AtomicCactus/ngrok.git
