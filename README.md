# 🚩 Guided Path: Solving PicoCTF Corrupt Key

Follow this structured path to understand, execute, and complete the challenge.

---

## 🗺️ Step 1: Analyze the Vulnerability (The Theory)
* **The Problem:** We have the RSA modulus $N$ and a partial leak of the prime factor $p$ (`_p_high`). However, a small 7-bit segment inside the prefix is uncertain, and the lower bits are entirely missing.
* **The Vulnerability:** Since we know more than half of $p$'s total bit length, the key is vulnerable to a **Partial-Key Exposure Attack**.
* **The Math:** We use **Coppersmith's Method**. By building a polynomial $f(x) \equiv 0 \pmod p$, we can use the **LLL (Lenstra–Lenstra–Lovász)** lattice reduction algorithm to find the small integer root $x$, which represents our missing lower bits.

---

## 🛠️ Step 2: Set Up the Environments
To solve this, you need two different programming environments:

### Environment A: SageMath (For Math & Lattice Reduction)
1. Open the web-based [SageMathCell](https://sagemath.org).
2. This environment natively handles the complex polynomial rings and matrix mathematics required by Coppersmith's method.

### Environment B: Python 3 (For Local Decryption)
1. Create a local folder on your computer.
2. Place your encrypted flag file (`msg.enc`) inside this folder.
3. Install the required cryptographic library by running this command in your terminal:
   ```bash
   pip install pycryptodome tqdm
   ```

---

## 🧬 Step 3: Recover Prime $p$ in SageMath
Because 7 bits of our known prefix are uncertain, our script uses a hybrid brute-force and lattice approach.

1. Copy the full SageMath script (containing `small_roots`, `recover`, and `solve`) into **SageMathCell**.
2. Click **Evaluate**.
3. **How it executes:** 
   * `tqdm` loops through all $2^7 = 128$ possible bit variations for the uncertain segment.
   * For each guess, `recover()` constructs the polynomial $f(x) = p_{\text{high}} \cdot 2^{k} + x$.
   * `small_roots()` builds an LLL matrix to find the root.
4. **Output:** The script will successfully print out the complete, large integer value of **$p$**. Copy this number.

---

## 🔓 Step 4: Extract the Flag with Python
Now that the hard math is done, you can decrypt the message using standard RSA math.

1. Create a file named `decrypt.py` in your local project folder.
2. Paste the standard RSA Python decryption code into it.
3. Replace the `p = ...` variable with the exact long integer output you copied from SageMath in Step 3.
4. Run the script in your terminal:
   ```bash
   python decrypt.py
   ```
5. **Result:** The script reads `msg.enc`, derives $q$ and the private key $d$, reverses the encryption, and prints your flag to the screen!
# Picoctf-Corruptkey
The guided solution for PicoCTF (Corrupt-Key)
1 : First Run the sage math code in online compiler cocalc:)
2: GET The Extracted Values. 
3:And then run the second script i gave you to get the Flag. 
4: Dont Just copy , Learn the Code and Demonstarted Attsck Using Some AI tools.
