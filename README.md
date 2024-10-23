# Exp-13 : Implement Message Authentication Code (MAC)

## AIM:
To implement the Message Authentication Code (MAC) algorithm in C for ensuring the integrity and authenticity of a message.

## DESIGN STEPS:
### Step 1:
Select a secret key K for the MAC algorithm.

### Step 2:
Take the input message M from the user.

### Step 3:
Combine the message M with the secret key K.

### Step 4:
Generate a MAC by hashing the combined data (using a simple hash function like XOR or a more secure function like SHA).

### Step 5:
Verify the MAC by recomputing it using the same method and comparing it with the transmitted MAC.

# PROGRAM:
```
NAME:VESLIN ANISH A
REGISTER NO:212223240175
#include <stdio.h>
#include <string.h>

// Simple XOR-based hash function for generating MAC
unsigned int simpleHash(char *data, int length) {
    unsigned int hash = 0;
    for (int i = 0; i < length; i++) {
        hash ^= data[i];  // XOR each byte to create a hash
    }
    return hash;
}

// Function to generate MAC
unsigned int generateMAC(char *message, char *key) {
    char combined[256];  // Combined message and key
    strcpy(combined, key);  // Start with the key
    strcat(combined, message);  // Append the message
    
    // Generate a hash of the combined key + message
    return simpleHash(combined, strlen(combined));
}

int main() {
    char message[128];
    char key[128];
    
    // Input the secret key
    printf("Enter the secret key: ");
    fgets(key, sizeof(key), stdin);
    key[strcspn(key, "\n")] = 0;  
    
    // Input the message
    printf("Enter the message: ");
    fgets(message, sizeof(message), stdin);
    message[strcspn(message, "\n")] = 0; 
    
    // Generate MAC for the given message
    unsigned int mac = generateMAC(message, key);
    
    // Print the generated MAC
    printf("Generated MAC: %u\n", mac);
    
    // For verification, re-enter the message and key to check
    char verify_message[128];
    char verify_key[128];
    
    printf("\n--- Verification ---\n");
    printf("Enter the message for verification: ");
    fgets(verify_message, sizeof(verify_message), stdin);
    verify_message[strcspn(verify_message, "\n")] = 0;  
    
    printf("Enter the secret key for verification: ");
    fgets(verify_key, sizeof(verify_key), stdin);
    verify_key[strcspn(verify_key, "\n")] = 0;  
    
    // Generate MAC for the verification message
    unsigned int verify_mac = generateMAC(verify_message, verify_key);
    
    // Compare the two MACs
    if (mac == verify_mac) {
        printf("Verification successful! MACs match.\n");
    } else {
        printf("Verification failed! MACs do not match.\n");
    }
    
    return 0;
}


```
# OUTPUT:
![Screenshot 2024-10-23 231540](https://github.com/user-attachments/assets/0eac829d-efb4-4069-b00b-6aee7cfd2bad) 

# RESULT:
Thus, the Message Authentication Code (MAC) algorithm has been successfully implemented in C.
