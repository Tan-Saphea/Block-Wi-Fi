# Block Wi-Fi on Windows (វិធីសាស្រ្តបិទ Wi-Fi លើ Windows)

ឯកសារណែនាំស្តីពីរបៀបកំណត់មិនឱ្យកុំព្យូទ័រ Windows 10 ឬ Windows 11 អាចភ្ជាប់បណ្តាញ Wi-Fi បាន ទោះបីជាអ្នកប្រើប្រាស់ស្គាល់ Password ក៏ដោយ។

---

## វិធីទី 1: បិទ Wi-Fi Adapter (ងាយស្រួល)

វិធីនេះធ្វើឱ្យកុំព្យូទ័រមិនអាចភ្ជាប់ Wi-Fi បាន រហូតដល់មានអ្នកបើក Adapter ឡើងវិញ។

### ជំហានអនុវត្ត:
1. ចុច `Win + R` ដើម្បីបើកផ្ទាំង Run
2. វាយបញ្ចូលពាក្យ `ncpa.cpl` រួចចុច **Enter**
3. ស្វែងរក **Wi-Fi** Adapter
4. ចុច Mouse ស្តាំ (Right-click) លើ **Wi-Fi**
5. ជ្រើសរើសយក **Disable**

> **ចំណាំ:** អ្នកប្រើប្រាស់ដែលមានសិទ្ធិជា Administrator អាចបើក (Enable) វាឡើងវិញបានយ៉ាងងាយស្រួល ដូច្នេះវិធីនេះមិនមែនជាការការពារដាច់ខាតឡើយ។

---

## វិធីទី 2: Block Wi-Fi ទាំងអស់ដោយ CMD (ណែនាំ)

វិធីនេះអាចរារាំងការភ្ជាប់ Wi-Fi បានយ៉ាងមានប្រសិទ្ធភាព ទោះបីជាស្គាល់ Password ក៏ដោយ។

### ជំហានអនុវត្ត:
1. បើក **Command Prompt** ដោយជ្រើសរើស **Run as administrator**
2. វាយ Command ខាងក្រោមដើម្បីទប់ស្កាត់ការភ្ជាប់ Wi-Fi ប្រភេទ Infrastructure ទាំងអស់:
   ```cmd
   netsh wlan add filter permission=denyall networktype=infrastructure
   ```
3. ផ្តាច់ Wi-Fi ដែលកំពុងភ្ជាប់បច្ចុប្បន្ន:
   ```cmd
   netsh wlan disconnect
   ```
4. ពិនិត្យបញ្ជី Filter ដែលបានកំណត់:
   ```cmd
   netsh wlan show filters
   ```

### របៀបបើកឱ្យភ្ជាប់ Wi-Fi វិញ (Restore Wi-Fi):
នៅពេលអ្នកចង់អនុញ្ញាតឱ្យកុំព្យូទ័រភ្ជាប់ Wi-Fi វិញ សូមបើក Command Prompt (Run as administrator) រួចវាយ:
```cmd
netsh wlan delete filter permission=denyall networktype=infrastructure
```

---

## វិធីទី 3: ការពារមិនឱ្យអ្នកផ្សេងបើក Wi-Fi វិញ

ប្រសិនបើកុំព្យូទ័រនេះមានអ្នកផ្សេងប្រើប្រាស់រួមគ្នា អ្នកគួរអនុវត្តបន្ថែមដូចខាងក្រោម:
1. បង្កើត Windows Administrator Account ដែលមាន Password ការពារត្រឹមត្រូវ។
2. ប្តូរ Account របស់អ្នកប្រើប្រាស់ផ្សេងឱ្យទៅជា **Standard User**។
3. អនុវត្តការបិទ Wi-Fi Adapter តាមវិធីទី 1 ឬ Block តាមរយៈ CMD តាមវិធីទី 2។
4. កុំចែករំលែក Administrator Password ទៅកាន់អ្នកប្រើប្រាស់ផ្សេង។

វិធីនេះនឹងធានាថាអ្នកប្រើប្រាស់ធម្មតាមិនអាចចូលទៅ Enable Adapter ឬកែសម្រួលការកំណត់របស់ Network ឡើងវិញបានឡើយ។

---

## English Guide

### Method 1: Disable Wi-Fi Adapter
1. Press `Win + R`, type `ncpa.cpl`, and press **Enter**.
2. Locate the **Wi-Fi** adapter.
3. Right-click on it and select **Disable**.
*Note: Users with Administrator access can easily re-enable it.*

### Method 2: Block All Wi-Fi Networks via Command Prompt (Recommended)
1. Open **Command Prompt** as Administrator (**Run as administrator**).
2. Block all infrastructure Wi-Fi networks:
   ```cmd
   netsh wlan add filter permission=denyall networktype=infrastructure
   ```
3. Disconnect any currently connected Wi-Fi:
   ```cmd
   netsh wlan disconnect
   ```
4. Verify the active filter:
   ```cmd
   netsh wlan show filters
   ```

#### To Unblock / Restore Wi-Fi:
Run Command Prompt as Administrator and execute:
```cmd
netsh wlan delete filter permission=denyall networktype=infrastructure
```

### Method 3: Restrict User Privileges
1. Set up a secure password on your Administrator account.
2. Change other user accounts to **Standard User**.
3. Do not share the Administrator credentials. Standard users will not have permission to modify network filters or adapter states.
