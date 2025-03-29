# How to Setup Splunk & Upload Testing Data  

## Access Splunk Web  
- Open your browser and go to `http://127.0.0.1:8000/`  
- Log in with your Splunk credentials  

## 1. Install Splunk Add-ons  
Install the following add-ons to ensure correct source typing and log parsing:  
- **Splunk Add-on for Cisco WSA** (for Cisco IronPort logs)  
- **Splunk Add-on for Unix and Linux** (for Linux authentication logs)  

**Steps:**  
1. Navigate to `Apps` → `Find More Apps`  
2. Search for and install the required add-ons via Splunkbase  

> ✅These add-ons enable automatic field extractions, making searches more efficient.  

## 2. Prepare Data  
Extract `zip` file from Splunk that contains:  
- **Web logs** (`access.log`, `secure.log`) for `www1`, `www2`, `www3`  
- **Cisco IronPort logs** (`cisco_ironport_web.log`)  
- **Additional data** (`MOCK_DATA.csv`, used later)  

> ✅These logs simulate real-world security events, providing a hands-on experience.  

## 3. Upload Data to Splunk  
Go to **`Settings` → `Add Data` → `Upload`**, then follow these steps:  

### Web Server Logs (`www1`, `www2`, `www3`)  
1. **Upload `access.log`**  
   - Source Type: `access_combined`  
   - Host: `web1` (or `web2`, `web3`)  
   - Index: `web`  

2. **Upload `secure.log`**  
   - Source Type: `linux_secure`  
   - Host: `web1` (or `web2`, `web3`)  
   - Index: `security`  

> ✅Correct source types ensure accurate parsing of Apache access logs and Linux authentication logs.  

### Cisco IronPort Log  
1. **Upload `cisco_ironport_web.log`**  
   - Source Type: `cisco:wsa:squid`  
   - Host: `cisco`  
   - Index: `cisco`  

> ✅Cisco WSA logs contain proxy traffic data, which is essential for network security monitoring.  

## 4. Validate Data in Splunk  
Use **Search & Reporting** to confirm ingestion:  
```splunk
index=* | stats count by index, sourcetype, source, host
```

![Full Splunk Setup](img/1.png)  
*Setting up Splunk with testing data*  

# Adding Local Monitor Data to Splunk  

## 1. Add Local Event Logs  
- Navigate to **Settings** → **Add Data** → **Monitor**  
- Select **Local Event Logs** (Collect event logs from this machine)  
- Choose important logs to monitor:  
  - ✅ Application Logs  
  - ✅ Security Logs  
  - ✅ System Logs  
- Click **Next**, set **host value** to your machine  
- Create a new index (e.g., `application_system_security`)  
- Click **Review** → **Submit**  

## 2. Add Local Windows Host Monitoring  
- Go to **Add Data** → **Monitor**  
- Select **Local Windows Host Monitoring**  
- Enter a **Collection Name** (e.g., `my_local_logs`)  
- Select all available monitoring options  
- Set interval to **30 seconds**  
- Assign a new index (e.g., `my_computer_logs`)  
- Click **Save & Review** → **Submit**  

## 3. Search the Added Data  
- Use the **Search & Reporting** app  
- Query logs by their respective indexes:  
  ```spl
  index="applicatioin_system_security" or index="my_computer_logs"	

    source="my_local_logs" host="myHost" index="my_computer_logs" sourcetype="WinHostMon"
  ```

![Adding Monitoring of my Local Machine](img/2.png)  
*Adding Monitoring of my Local Machine*  

![ ](img/3.png)  
* *  

![ ](img/4.png)  
* *  

![ ](img/5.png)  
* *  

![ ](img/6.png)  
* *  

![ ](img/7.png)  
* *  

![ ](img/8.png)  
* *  

![ ](img/9.png)  
* *  

![ ](img/10.png)  
* *  

![ ](img/11.png)  
* *  

![ ](img/12.png)  
* *  

![ ](img/13.png)  
* *  

![ ](img/14.png)  
* *  

![ ](img/15.png)  
* *  

![ ](img/16.png)  
* *  

![ ](img/17.png)  
* *  

![ ](img/18.png)  
* *  

![ ](img/19.png)  
* *  

![ ](img/20.png)  
* *  

![ ](img/21.png)  
* *  

![ ](img/22.png)  
* *  

![ ](img/23.png)  
* *  

![ ](img/24.png)  
* *  

![ ](img/25.png)  
* *  

![ ](img/26.png)  
* *  

![ ](img/27.png)  
* *  

![ ](img/28.png)  
* *  

![ ](img/29.png)  
* *  

![ ](img/30.png)  
* *  

![ ](img/31.png)  
* *  

![ ](img/32.png)  
* *  

![ ](img/33.png)  
* *  

![ ](img/34.png)  
* *  

![ ](img/35.png)  
* *  

![ ](img/36.png)  
* *  

![ ](img/37.png)  
* *  

![ ](img/38.png)  
* *  

![ ](img/39.png)  
* *  

![ ](img/40.png)  
* *  
