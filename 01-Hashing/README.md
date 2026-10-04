# Practical 1: File Hashing with CertUtil (MD5 & SHA-1)

## Aim
To generate MD5 and SHA-1 hash values of files using the Windows `certutil` command, and to observe how hash values change when a file is modified or compressed.

## Tools & Environment
- **OS:** Windows (Command Prompt)
- **Utility:** `certutil` (built-in Windows tool)
- **Algorithms:** MD5 (128-bit), SHA-1 (160-bit)

## Command Syntax
```cmd
certutil -hashfile "<path_to_file>" <ALGORITHM>
```
Replace `<ALGORITHM>` with `MD5` or `SHA1`.

---

## Part A: Generate MD5 and SHA-1 Hashes of a File

**File used:** `adiya.txt`

```cmd
certutil -hashfile "C:\Users\student\Desktop\adiya.txt" MD5
certutil -hashfile "C:\Users\student\Desktop\adiya.txt" SHA1
```

| Algorithm | Hash Value |
|-----------|------------|
| MD5  | `c0eb9c69c7686606adbfc4318e8b40e2` |
| SHA-1 | `8a0a1d72aac8db471700260d48c59f3e5a85afc1` |

---

## Part B: Effect of Modifying a File

### 1. Hash before and after editing
The MD5 hash of `adiya.txt` was calculated, the file contents were changed, and the hash was calculated again.

```cmd
certutil -hashfile "C:\Users\student\Desktop\adiya.txt" MD5
```

| Stage | MD5 Hash |
|-------|----------|
| Hash 1 (original file) | `c0eb9c69c7686606adbfc4318e8b40e2` |
| Hash 2 (after modification) | `4ca0a6af4760e6a3edbd22637cc2146b` |

**Observation:** Even a small change to the file produces a completely different hash (the avalanche effect). This is why hashes are used to verify file integrity.

### 2. Comparing hashes of text files and their ZIP archives
Two text files (`DIYA.txt`, `JANVI.txt`) were created and compressed into ZIP files. Hashes of each original and its ZIP were compared.

#### File 1: DIYA

| File | MD5 | SHA-1 |
|------|-----|-------|
| `DIYA.txt` | `eb61eead90e3b899c6bcbe27ac581660` | `c65f99f8c5376adadddc46d5cbcf5762f9e55eb7` |
| `DIYA.zip` | `7ea081e47d17d42dafb7f15f47cc1e5d` | `b5e5e73c5671633c4bbddcd9e20d47a0a9f4c195` |

#### File 2: JANVI

| File | MD5 | SHA-1 |
|------|-----|-------|
| `JANVI.txt` | `a84af70122be5b965d035f3100288c10` | `d80b227e7d56f0d8bdafa8b745f555fb395ed4ac` |
| `JANVI.zip` | `56766b3b72bc6f0d010e75b436cd844e` | `4c13b19b071fdf34ee92d786f3f180017b1b0ada` |

**Observation:** In both cases the hash of the ZIP file differs from the hash of the original text file. Compression changes the binary content of the file (and adds archive headers and metadata), so the resulting hash is different.

---

## Conclusion
- `certutil -hashfile` can generate MD5 and SHA-1 hashes for any file on Windows.
- Hash values are unique to a file's exact contents: any change, however small, results in a different hash.
- A file and its compressed (ZIP) version have different hashes, since they are different byte sequences.
- MD5 produces a 32-character hex digest and SHA-1 a 40-character hex digest.
- Note: both MD5 and SHA-1 are considered cryptographically weak today (collisions are possible). They are fine for basic integrity checks, but SHA-256 or stronger is recommended for security purposes (`certutil -hashfile <file> SHA256`).

## Screenshots
Add your command prompt screenshots to a `screenshots/` folder and link them here, for example:

```markdown
![MD5 and SHA1 of adiya.txt](screenshots/part-a.png)
![Hash before and after modification](screenshots/part-b1.png)
![DIYA and JANVI hashes](screenshots/part-b2.png)
```
