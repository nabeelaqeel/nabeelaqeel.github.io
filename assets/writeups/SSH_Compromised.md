# Challenge Name: SSH Compromised

**Category:** Incident Handling Challenge  
**Points:** 500

## Approach

1. **Unzip the file:**
    ```sh
    gunzip rawlog.tar.gz
    ```

2. **Extract the tar file:**
    ```sh
    tar -xvf rawlog.tar
    ```

3. **Analyze the `auth.log` file:**
    ```sh
    cat auth.log
    ```

4. **Observe repeated log messages from different IPs and ports:**
    ```
    Jul 27 05:02:32 vmprod-uat-01 sshd[153942]: Failed password for root from 149.102.244.68 port 8352 ssh
    Jul 27 05:02:33 vmprod-uat-01 sshd[153942]: Connection closed by authenticating user root 149.102.244.68 port 8352 [preauth]
    ```

5. **Check for successful login attempts:**
    If the intruder gained access, there should be logs for accepted passwords.

6. **Search for "Accepted password" in `auth.log`:**

    ```
    cat auth.log | grep "Accepted password"
    
    Jul 27 05:02:26 vmprod-uat-01 sshd[153863]: Accepted password for sysadmin from 149.102.244.68 port 7153 ssh
    ```

7. **Get the flag**

    flag : ihack24{149.102.244.68_sysadmin}