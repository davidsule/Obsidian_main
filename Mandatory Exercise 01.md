
### Security & Privacy - David Süle

#### Q1
*The following message has been encrypted using Caesar’s cipher: byffixulehymmgsifxzlcyhx. Decrypt the message. Note, the spaces have been removed for better obfuscation. Your answer should have spaces removed as well.*

```
abcdefghijklmnopqrstuvwxyz
ghijklmnopqrstuvwxyzabcdef
```
hellodarknessmyoldfriend

#### Q2
*Each month, Alice sends Bob a message, encrypting the name of the city where they should meet using one-time pad.  Last month, Eve intercepted an encrypted message “221c15061c0d150c0017”, and she knows that Alice then met Bob in Copenhagen. The next intercepted message from Alice is 201f001b130b10190c18. In which city do Alice and Bob meet this month? Hint: the messages are encoded in hexadecimal, e.g. “Berlin” becomes “4265726c696e”. The answer should be decoded to ACSII, that is, it should be a readable text in English. Following tools can help: https://gchq.github.io/CyberChef/, https://xor.pw.*

`Copenhagen` ($m_1$) to hex: `43 6f 70 65 6e 68 61 67 65 6e`
`XOR` with $c_1$ will be $k$: `61 73 65 63 72 65 74 6b 65 79`
`XOR` $k$ with $c_2$ will be $m_2$: `Alexandria`

#### Q3
*ℋ is a hash function that defined as follows: given a number, it returns the sum of all its digits; for example, given 6885 as input, the function returns 6+8+8+5=27. Which properties of a cryptographic hash function are ensured?*

a - easy to compute

#### Q4
```python
import hashlib

def compute_hash(password, salt):
    return hashlib.sha256((password + salt).encode()).hexdigest()

def find_password(target_hash, salt):
    for i in range(1000000):
        password = str(i).zfill(6) # Pad with zeros
        if compute_hash(password, salt) == target_hash:
            return password
    
    return None


salt = "dzr0fv3hz4"
target_hash = "20048def4d4a3922a933a4f84b9cb838c70a8b80402ac45243ed586dd8643bca"

password = find_password(target_hash, salt)

if password:
    print(f"Found the password: {password}")
else:
    print("Password not found.")
```

Solution: `558519`

#### Q5
*$N = 39015351411159703781$, $e = 28236791284198039865$ is an RSA public key. Find a secret key $d$. Hint: $N$ is small enough to factor using online tools. Once you have the prime factors of $N$, you can compute $d$.*

