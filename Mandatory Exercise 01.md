
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