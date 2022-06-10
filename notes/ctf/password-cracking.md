# Password cracking

## Hashcat
- https://hashcat.net/wiki/doku.php?id=hashcat

### Dictionary attack
- `hashcat -m 10 -a 0 hashes.txt rockyou.txt`
    - `-m 10` is salted MD5 (hash.salt format)
    - `-a 0` is dictionary attack mode

### Dictionary attack with rules
- `hashcat -m 10 -a 0 hashes.txt rockyou.txt -r nsa64.rule.txt`
    - `-r nsa64.rule.txt` - rules (such as append a number at the end)

### Brute-force with mask (`[a-z0-9]{8}`)
- `hashcat -m 10 -a 3 -1 ?l?d ?1?1?1?1?1?1?1?1 hashes.txt`
    - `-a 3` is brute-force attack mode
    - `-1 ?l?d`  defines custom charset
        - `-l` - small alphabets
        - `-d` - digits

## John the Ripper