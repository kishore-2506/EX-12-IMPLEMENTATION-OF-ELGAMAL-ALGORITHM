
## AIM:

To implement the ElGamal encryption and decryption algorithm using C for secure communication.


## ALGORITHM:
1.	Choose a large prime number p and a primitive root g of p.
2.	Select a private key x such that 1 < x < p.
3.	Compute the public key y = g^x mod p.
4.	To encrypt a message M:
a.	Choose a random integer k such that 1 < k < p.
b.	Compute C1 = g^k mod p.
c.	Compute C2 = (M * y^k) mod p.
d.	The ciphertext is the pair (C1, C2).
5.	To decrypt the ciphertext (C1, C2):
a.	Compute s = C1^(p-1-x) mod p.
b.	Compute the original message M = (C2 * s) mod p.
6.	Display the decrypted message.


## PROGRAM:
```
#include <stdio.h>
#include <math.h>

long long int modExp(long long int base, long long int exp, long long int mod) {
    long long int result = 1;
    base = base % mod;
    while (exp > 0) {
        if (exp % 2 == 1)
            result = (result * base) % mod;
        exp = exp / 2;
        base = (base * base) % mod;
    }
    return result;
}

int main() {
    long long int p, g, x, y, k, M, C1, C2, s, decrypted;

    printf("Enter a large prime number (p): ");
    scanf("%lld", &p);

    printf("Enter a primitive root of p (g): ");
    scanf("%lld", &g);

    printf("Enter private key (x): ");
    scanf("%lld", &x);

    y = modExp(g, x, p);
    printf("Public key (y) = %lld\n", y);

    printf("Enter message (M) < p: ");
    scanf("%lld", &M);

    printf("Enter random integer (k): ");
    scanf("%lld", &k);

    C1 = modExp(g, k, p);
    C2 = (M * modExp(y, k, p)) % p;

    printf("\n--- Encryption ---\n");
    printf("Ciphertext: (C1, C2) = (%lld, %lld)\n", C1, C2);

    s = modExp(C1, p - 1 - x, p);
    decrypted = (C2 * s) % p;

    printf("\n--- Decryption ---\n");
    printf("Decrypted message (M) = %lld\n", decrypted);

    return 0;
}
```


## OUTPUT:

<img width="642" height="497" alt="EXP 12" src="https://github.com/user-attachments/assets/cdef3767-d939-4f5a-bcd2-fd29903c8c05" />

## RESULT:

The program is executed successfully.
