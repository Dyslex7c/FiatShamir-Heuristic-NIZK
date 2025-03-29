# FiatShamir-Heuristic-NIZK

We can develop a Non-Interactive Zero-Knowledge Proof using Fiat-Shamir heuristic and ECC. Let's say Bob is the prover and Alice is the verifier. Bob knows x (assume it to be a private key). Both of them agree upon the values of G and H (points on the elliptic curve) Bob computes xG and xH and sends it to Alice. Bob then selects v and calculates c as the hash of xG, xH, vG, and vH. Bob calculates `r = v-xc` and sends it over to Alice alongside vG and vH. Alice computes c and checks the following:

```
vG == rG + c(xG)
vH == rH + c(xH)
```

If both satisfy, it has been thus proved that Bob knows x

Proof: vG = rG + c(xG) = (v-cx)G + c(xG) = vG (Similarly for vH)

## Prerequisites

Install go and download the following dependencies:
```
go get go.dedis.ch/kyber/v3/group/edwards2551
go get go.dedis.ch/kyber/v3/util/random
```

## Run the program

```
go build
./fiat-shamir-heuristic-nizk TrzQAtbgoxJIW6
Bob and Alice agree:
 G:     73ef257a9be315b3bf73426cd69478fa4d16ffd2cc419c7844976168fb10ba5e
 H:     6e9d02f64820145ecb06129a0331ffa989dc430b0f0c02dfa855dbb49fd52b33

Bob's Password: TrzQAtbgoxJIW6
Bob's Secret(x):7e2a11ad0909032d7d664b371df36f956f4fec311d3e3a5f2ce785b0037ef608

Bob sends these values:
 xG:    037e64abbcd7dc6964dabe2afc1766afea95b27b95ce2e74382d66934e297094
 xH:    5652aacd3e0863ae9db49df60a36dbfdde46d8cab3490bd34611e62908061693

Bob selects v = 23364489c6ec4c5a0a69e77932e5c5d76b20dcf865155719a3c4e1f21dc7760f

Alice computes c = H(xG||xH||vG||vH)):  561120a0979b5a0f57f89a996a471204445a2d1bcf1a61761d47b48fd5d00706

Bob sends these values:
 r:     f1398e1c7ebd7e78d9f4fe76f6ecd972a1c661e7c023c4902ca50a0123e5cc0c
 vG:    9740111802dfd0c57f8c1ed6a4cbacb708d1466cf3aa2444028fe72656920951
 vH:    915045995f0f2c9e21b217a5a89e9691dd300a9285ba56ea40b61ff28c5dabbf

Correct proof%
```

Ref: Buchanan, William J (2025). Fiat–Shamir with Go and ECC (Non-interactive ZKP). Asecuritysite.com. https://asecuritysite.com/encryption/go_fiat2