# EPUB Provenance Repository

**Thornevald Publishing**  
Digital provenance and file integrity verification for DRM-free ebooks

---

## What This Is

This repository serves as a public ledger of file integrity hashes and GPG signatures for ebooks published by Thornevald Publishing. It exists to prove that the file you're reading is exactly the file we published—unaltered, unmodified, and authentic.

## Why This Matters

In a world where digital files can be silently modified, injected with tracking code, or corrupted in transit, provenance matters. This repository provides cryptographic proof that:

1. **The file came from us** - GPG signatures verify the publisher
2. **The file hasn't been altered** - SHA-512 hashes verify integrity
3. **The record is permanent** - Git history preserves the timeline

Think of it as a public notary for digital books.

## Structure

```
epub-provenance/
└── releases/
    └── YYYY-MM-DD/
        ├── book-title-v1.0-abc123.sha512
        └── book-title-v2.0-abc123.epub.asc
```

Each release date contains:
- **`.sha512` files** - SHA-512 hash of the EPUB file
- **`.epub.asc` files** - GPG detached signatures (when available)

## How to Verify a File

### 1. Verify SHA-512 Hash

Every EPUB published by Thornevald Publishing contains a provenance page with:
- The SHA-512 hash embedded in the file
- A QR code linking to this repository
- Instructions for verification

**On macOS/Linux:**
```bash
# Calculate hash of your EPUB
shasum -a 512 your-book.epub

# Compare with published hash
cat releases/2026-01-29/your-book-v1.0-abc123.sha512
```

**On Windows (PowerShell):**
```powershell
Get-FileHash -Algorithm SHA512 your-book.epub
```

The hashes should match exactly.

### 2. Verify GPG Signature (Optional)

If you want cryptographic proof the file came from Thornevald Publishing:

```bash
# Import our public key (first time only)
gpg --recv-keys [OUR_KEY_ID]

# Verify signature
gpg --verify releases/2026-01-29/your-book-v1.0-abc123.epub.asc your-book.epub
```

A valid signature proves:
- The file was signed by Thornevald Publishing
- The file hasn't been modified since signing

## What the Hash Proves

A matching SHA-512 hash proves:  
- The file is byte-for-byte identical to what we published  
- No tracking code has been injected  
- No content has been altered or censored  
- The file hasn't been corrupted in transit or storage

A non-matching hash means:  
- The file has been modified (possibly maliciously)  
- The file may be corrupted  
- You should re-download from a trusted source

## DRM-Free Means Trust-Based

Our ebooks are DRM-free. We don't lock them down, we don't track you, and we don't require accounts. But DRM-free only works if you can trust the source.

This repository is how we earn that trust.

## For Readers

### Quick Verification

1. Open the EPUB in your reader  
2. Go to the **Provenance** page (last page of the book)  
3. Tap the QR code or copy the hash  
4. Compare with the hash in this repository  

If they match: you have an authentic, unmodified file.  
If they don't: something's wrong. Contact us.

### Why Should You Care?

Most readers won't verify every file. That's fine. But the fact that verification is *possible* keeps everyone honest:

- Distributors can't inject tracking code
- Platforms can't silently censor content
- Bad actors can't impersonate us
- You can prove what we actually published

It's trust, but verifiable.

## For Distributors & Platforms

If you're hosting or distributing our ebooks:

1. **Don't modify the files** - Any change breaks the hash
2. **Preserve metadata** - ISBN, publisher, dates must remain intact
3. **Keep provenance intact** - Don't remove the provenance page
4. **Link back here** - Readers should be able to verify

We chose DRM-free *because* we trust readers and distributors to do the right thing. This repository is the safety net.

## For Developers & Archivists

### Hash Format

SHA-512 files use the standard format:
```
<hash>  <filename>
```

Example:
```
a1b2c3d4e5f6...  book-title-v1.0-abc123.epub
```

Compatible with:
- `shasum -c` (macOS/Linux)
- `sha512sum -c` (Linux)
- Standard checksum tools

### Git as Provenance

The Git history itself provides additional provenance:
- **Commit timestamps** - When the file was published
- **Commit messages** - Publication notes
- **Immutable history** - Can't be rewritten without detection

Clone this repo to preserve a complete provenance archive.

## Contact

**Publisher:** Thornevald Publishing  
**Location:** Matakana, New Zealand  
**Website:** [www.thornevald.com](https://www.thornevald.com)  
**Email:** ahoy@thornevald.com

## Philosophy

We believe:

- Readers deserve to know their files are authentic
- Publishers should be accountable for what they publish
- DRM is not the answer to trust problems
- Transparency beats control every time

This repository is our commitment to those beliefs.

---

## Technical Notes

### Why SHA-512?

- Industry standard for file integrity
- Collision-resistant (practically impossible to forge)
- Widely supported across platforms
- Fast enough for large files

### Why Git?

- Immutable history
- Distributed (anyone can clone and preserve)
- Timestamped (commit dates prove publication timeline)
- Transparent (all changes are public)

### Why Not Blockchain?

Because Git does everything we need without the complexity, energy waste, or hype. Blockchain is a solution looking for a problem. Git is a proven tool that already solves ours.

## License

The *hashes and signatures* in this repository are public domain (CC0).  
The *ebooks themselves* are copyrighted works - see each book's license page.

This repository exists to verify authenticity, not to distribute the files themselves.

---

**Last Updated:** 2026-01-29  
**Repository:** [Thornevald Publishing](https://github.com/thornevald-publishing/epub-provenance)
