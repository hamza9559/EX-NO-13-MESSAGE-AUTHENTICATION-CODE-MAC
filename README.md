# EX-NO-13-MESSAGE-AUTHENTICATION-CODE-MAC

## AIM:
To implement MESSAGE AUTHENTICATION CODE(MAC)

## ALGORITHM:

1. Message Authentication Code (MAC) is a cryptographic technique used to verify the integrity and authenticity of a message by using a secret key.

2. Initialization:
   - Choose a cryptographic hash function \( H \) (e.g., SHA-256) and a secret key \( K \).
   - The message \( M \) to be authenticated is input along with the secret key \( K \).

3. MAC Generation:
   - Compute the MAC by applying the hash function to the combination of the message \( M \) and the secret key \( K \): 
     \[
     \text{MAC}(M, K) = H(K || M)
     \]
     where \( || \) denotes concatenation of \( K \) and \( M \).

4. Verification:
   - The recipient, who knows the secret key \( K \), computes the MAC using the received message \( M \) and the same hash function.
   - The recipient compares the computed MAC with the received MAC. If they match, the message is authentic and unchanged.

5. Security: The security of the MAC relies on the secret key \( K \) and the strength of the hash function \( H \), ensuring that an attacker cannot forge a valid MAC without knowledge of the key.

## Program:
```c
#include <stdio.h>
#include <string.h>

// A simple hash-like function (not secure, just for demonstration)
// Computes sum of ASCII values mod 256
unsigned char simple_hash(const char *data) {
    unsigned int sum = 0;
    for (int i = 0; data[i] != '\0'; i++) {
        sum += (unsigned char)data[i];
    }
    return (unsigned char)(sum % 256);
}

// Function to compute MAC = hash(key || message)
unsigned char compute_mac(const char *key, const char *message) {
    char combined[512];
    // concatenate key and message
    strcpy(combined, key);
    strcat(combined, message);

    return simple_hash(combined);
}

int main() {
    char key[100], message[400];
    unsigned char mac, received_mac;

    printf("Enter secret key: ");
    fgets(key, sizeof(key), stdin);
    key[strcspn(key, "\n")] = '\0';  // Remove newline

    printf("Enter message: ");
    fgets(message, sizeof(message), stdin);
    message[strcspn(message, "\n")] = '\0';  // Remove newline

    // Generate MAC for the message
    mac = compute_mac(key, message);
    printf("Generated MAC: %02X\n", mac);

    // Simulate verification by recomputing MAC
    printf("Enter received MAC (hex): ");
    scanf("%2hhx", &received_mac);

    if (received_mac == compute_mac(key, message)) {
        printf("Message is authentic and unchanged.\n");
    } else {
        printf("Message authentication failed.\n");
    }

    return 0;
}

```
## Output:
![image](https://github.com/user-attachments/assets/20301ad7-9258-40c2-bb69-605b427f9f2c)


## Result:
The program is executed successfully.
