Valet+ for Linux depends on specific PHP versions and extensions from the "ppa:ondrej/php" repository. However, this PPA only supports LTS versions of Ubuntu. If the PHP PPA is not correctly configured for the "noble" version, Valet+ will not be able to install or run correctly. By manually forcing the PPA to use the "noble" codename, you ensure that:

- PHP packages are correctly available for Ubuntu 25.04 and 25.10.
- Valet+ can install and configure PHP without errors.
- Your development environment remains stable and compatible.

### ✅ How to Force a PPA to Use "noble" on Ubuntu

1. **Update the package index**:
   ```bash
   sudo apt-get update
   ```
   
2. **Install dependencies**:
   ```bash
   sudo apt-get install libicu74
   ```
   ```bash
   sudo apt-get install libzip4t64
   ```

2. **Add the PPA normally**:
   ```bash
   sudo add-apt-repository ppa:ondrej/php
   ```

3. **Find the `.list` file that was created**:
   ```bash
   FILE=$(find /etc/apt/sources.list.d -name '*ondrej-php*.list')
   ```

4. **Rename the file to reflect "noble"**:
   ```bash
   sudo mv "$FILE" "${FILE/questing/noble}"
   sudo mv "$FILE" "${FILE/plucky/noble}"
   FILE="${FILE/questing/noble}"
   FILE="${FILE/plucky/noble}"
   ```

5. **Replace the release name inside the file**:
   ```bash
   sudo sed -i 's/questing/noble/g' "$FILE"
   sudo sed -i 's/plucky/noble/g' "$FILE"
   ```

6. **Update your package list**:
   ```bash
   sudo apt update
   ```

---

Now you can use the "Valet plus" commands to install the necessary PHP versions for your projects:

```bash
valet use 8.5
valet use 8.4
valet use 7.4
```
