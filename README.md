# DeepWebHarvester

Is an advanced Python-based crawler designed to anonymously navigate and extract valuable intelligence from the dark web’s ".onion" sites. By leveraging Tor’s anonymity network, the tool ensures secure, privacy-respecting access while implementing robust features such as automatic retries, rate-limiting to prevent detection, and periodic Tor circuit renewal to evade tracking. Built with an ethical OSINT mindset and a hacker vibe, DeepWebHarvester systematically handles website pages, extracts relevant links, and safely saves the data in structured formats for analysis. It is an essential tool for cybersecurity professionals and researchers seeking proactive threat intelligence from the darkest corners of the internet.
 



# key features of DeepWebHarvester tool

- **Anonymous Crawling via Tor**: Routes all traffic through the Tor network using the SOCKS5 proxy protocol for true anonymity on .onion sites.
  
- **Automated Link Discovery**: Starts from seed .onion URLs and recursively extracts valid hidden service links to expand crawling reach.
  
- **Robust Retry Mechanisms**: Retries failed network requests with exponential backoff, improving reliability on unstable dark web servers.
  
- **Rate Limiting**: Includes delays between requests to reduce the risk of IP bans and detection by dark web sites.
  
- **Automatic Tor Circuit Renewal**: Periodically changes the Tor identity/IP to maintain stealth and avoid being blocked.
  
- **Blacklist Filtering**: Skips crawling pages like login or registration that might require authentication or cause errors.
  
- **Data Extraction**: Parses page titles and text content safely and systematically.
  
- **Result Export**: Saves collected intelligence in structured JSON and CSV formats, ready for analysis or integration.
  
- **Ethical OSINT Focus**: Designed specifically for legal and ethical intelligence gathering with a hacker-inspired approach.


# Importance in Cybersecurity and OSINT

The DeepWebHarvester serves as a specialized tool for navigating and indexing hidden services on encrypted networks like Tor. Unlike conventional web crawlers, this tools delve into non-indexed, anonymous web spaces to extract valuable security-related data. Its importance spans several domains:


- **Threat Intelligence**: Organizations employ dark web crawlers to monitor emerging cyber threats, such as stolen credentials, leaked databases, malware discussions, and planned attacks circulating on dark web marketplaces and forums. Early detection enables faster incident response and risk mitigation.
  
- **Data Breach Detection**: Cybersecurity teams can identify when company data or customer information is sold or distributed in hidden channels, helping limit damage and notifying affected parties promptly.
  
- **Law Enforcement & Investigations**: These tools facilitate investigations by tracing illegal activities, uncovering criminal networks, and gathering intelligence from covert sources inaccessible via surface web.
  
- **Corporate Security**: Businesses use dark web data to assess vulnerabilities, monitor for brand abuse, and detect phishing campaigns specific to their organizations.
  
- **Academic Research & OSINT**: Researchers analyze dark web trends, criminal behaviors, and underground technological advancements for comprehensive threat landscapes.
  
- **Proactive Defense**: By aggregating dark web data continuously, organizations build enriched threat intelligence databases, enhancing predictive analytics and improving security postures against evolving risks.

  
**In essence, DeepWebHarvester empower cybersecurity professionals and OSINT practitioners with actionable insights from the most obscure and high-risk areas of the internet, offering a critical advantage in an increasingly hostile cyber environment**.


- - - 

**Below is a simple, step-by-step guide to set up and use the robust Python darkweb scraper tool on Kali Linux, covering everything from saving the script, installing dependencies, configuring Tor, to running the scraper**.


# 1. Save the Script ( Manual Installation )

- **Open a terminal**.
  
Use nano (or your preferred text editor) to create the Python script file:

    nano deepwebharvester.py

- Follow the link below to copy the tool script and paste it into nano:
  
https://gist.github.com/techenthusiast167/76ef6f0e1e3af74045f4d85bc1a7c60e
  
- **Save and exit nano**:
  
- Press **Ctrl+O**, hit Enter to save.
- Press **Ctrl+X** to exit nano.


- - - 


# 2. Install Required Dependencies

- **Make sure your system is updated**:

      sudo apt update
      sudo apt upgrade -y


- **Install Python3 and pip if not already installed**:

      sudo apt install -y python3 python3-pip


- **Create and activate a Python virtual environment to avoid conflicts**:

      virtualenv my_temp_venv
      source my_temp_venv/bin/activate


- **Install the necessary Python packages**:
  
      pip install requests pysocks stem beautifulsoup4 lxml


- - - 


# 3. Install and Configure Tor

- **Install the Tor service if you haven't**:

      sudo apt install -y tor


- **Enable Tor ControlPort in Tor's config so your script can renew identity**:
  
- **Generate a hashed control password (replace YourStrongPassword123 with a secure password)**:

      tor --hash-password YourStrongPassword123


- **The output will be something like**:
  
      16:AB12CD34EF56...


- **Edit Tor config file**:
  
      sudo nano /etc/tor/torrc


- **Add or uncomment these lines, replacing with your hashed password**:

      ControlPort 9051
      HashedControlPassword 16:AB12CD34EF56...


- **Save and exit (Ctrl+O, Enter, Ctrl+X)**.

  
- **Restart the Tor service**:
  
      sudo systemctl restart tor


- **Confirm Tor is running**:
  
      systemctl status tor@default.service


*You should see Active: active (running) status*.

**Or list all instance services**:

    systemctl list-units | grep tor@

- If Tor is running, these should show active (running) with a valid main PID.
- - - 


# 4. Update the Python Script Settings

- **Open the script for editing if needed**:

      nano deepwebHarvester.py


- Replace the placeholder TOR_CONTROL_PASSWORD = **"your_password_here"** with your plain text ControlPort password you set earlier, e.g.,
  
**TOR_CONTROL_PASSWORD = "YourStrongPassword123"**


- Add your target **.onion URLs** inside the **onion_start_urls** list in the script.
  
- **Save and exit**.


- - - 


# 5. Run the Scraper

- **With Tor service running and the script ready**:

      python3 deepwebharvester.py


- *You will see logs showing crawling progress, retries if any failures occur, and when scraping completes*.


- - - 

# 6. Check Results

The scraper saves results to:

    JSON & CSV 

To see the data scraped and save in JSON and CSV, you can use the command **open**. For example:

    open deepwebharvester_results.json

- This will open up the content of the data scraped and saved in json for you - same procedure with CSV.

- - - 

# Notes:

- The script automatically routes all requests through Tor's SOCKS5 proxy at 127.0.0.1:9050.

- It renews Tor circuits periodically for anonymity.
  
- It respects delays between requests to avoid hammering hidden services.
  
- Use Tor Browser for browsing .onion sites manually; no need to configure Firefox unless you want to proxy Firefox traffic through Tor.
  
- Keep system time accurate (sudo timedatectl set-ntp true) for Tor to work correctly.



- - - 
- - - 

# Additional Help (1)


**You can check if Tor is activated and running on your system by using the following commands in the terminal**:


1. **Check Tor service status**:
   
- Run this command to see if the Tor service is active and running:

       sudo systemctl status tor

- **Look for the line that says**:

      Active: active (running)

*If you see this, Tor is running correctly*.


# 2. Check if Tor is listening on the default SOCKS port (9050):

 
    ss -aln | grep 9050


*If you see output showing a listening socket on port 9050, this means Tor is ready to accept proxy connections*.



# 3. Test Tor connectivity with curl:

You can test if requests are going through Tor by using curl with the Tor SOCKS proxy:

    curl --socks5-hostname 127.0.0.1:9050 https://check.torproject.org/


*If successful, this will return a webpage message indicating you are using Tor — output page will say*: 

“Congratulations. This browser is configured to use Tor.”


# 4. If Tor is not running, start it:

    sudo systemctl start tor


# 5. If problems occur, check detailed logs:

    journalctl -xeu tor



# Summary:

**To confirm Tor is running properly**:

- **sudo systemctl status tor** → should show active (running)
  
- **ss -aln | grep 9050** → port 9050 listening
  
- **Curl test** → confirms Tor network is used
  
- If it's not running, you can start it with:
  
- **sudo systemctl start tor**



- - -


# Additionally HELP (2)


**If your Tor service status shows**:


*Active: active (exited) since date; minute > ago
...
Main PID: 1111651 (code=exited, status=0/SUCCESS)
...
Finished tor.service - Anonymizing overlay network for TCP (multi-instance-master)*.


# This means:

- The tor service unit is not running the Tor daemon actively.

- Instead, it started and immediately exited successfully because the service's ExecStart is likely set to /bin/true or a similar no-op command.
  
- So despite the "active (exited)" state, Tor is effectively not running as a persistent background process.



**For Tor to be properly active, the service’s ExecStart must run the actual Tor binary (e.g., /usr/bin/tor -f /etc/tor/torrc), and the status should be Active: active (running)**.


# What to do next:

1. Check your **Tor systemd service file** with:
  
         systemctl cat tor.service



2. If you see **/bin/true as the ExecStart command**, you must fix or replace it.


3. To fix it, you can:

- Reinstall Tor (which may restore the correct service file):

      sudo apt purge tor
      sudo apt install tor


4. Reload systemd and restart tor:

       sudo systemctl daemon-reload
       sudo systemctl enable tor
       sudo systemctl start tor
       sudo systemctl status tor


*After this, you should see Tor running properly*.


# Summary

- Tor is properly running when systemctl status tor shows active (running) (not active (exited)).
  
- Tor listens on port 9050 for SOCKS5 proxy.
  
- Curl test confirms Tor connection.
Log checks help identify startup or runtime issues.

- - - 



# Disclaimer

This tool is intended for legitimate cybersecurity and Open Source Intelligence (OSINT) purposes only. Unauthorized or illegal usage to access or disrupt dark web content is prohibited and may be punishable under applicable laws. Users must comply with all legal and ethical standards when deploying this tool. The creators shall not be held responsible for any misuse.


- If you need additional help, have questions, or want to collaborate, please don’t hesitate to reach out to me via my LinkedIn:

http://linkedin.com/in/tech-enthusiast-669279263

**Creator: Tech Enthusiast**
