# Azure-SIEM
<h1>Azure Security Information and Event Management (SIEM)</h1>

<h2>Overview</h2>

<p>This project was designed to visualize the scope of cyber threats lurking on the public internet. By deploying a deliberately vulnerable "honeypot" virtual machine in Microsoft Azure, I attracted real-world attackers and captured their failed login attempts. The collected data was then enriched with geolocation information and visualized on a global heat map—revealing just how relentless and widespread malicious activity truly is.</p>

<h2>Objective</h2>

<p>Demonstrate the volume and geographic distribution of brute-force attacks targeting internet-exposed systems, while gaining hands-on experience with Azure's security and monitoring ecosystem.</p>

<h2>Architecture</h2>

| Component | Purpose |
|-----------|---------|
| Azure Virtual Machine | Windows 10 Pro honeypot (`flytrap1`) with all defenses disabled |
| Windows Event Viewer | Captures failed RDP login attempts (Event ID 4625) |
| IP Geolocation API | Enriches attacker IPs with latitude, longitude, country, and region |
| Azure Log Analytics Workspace | Ingests and stores custom log data |
| Microsoft Sentinel | SIEM platform for querying, analyzing, and visualizing attack data |

<h2>Implementation Steps</h2>

<h3>1. Deploying the Honeypot</h3>
<p>Provisioned a Windows 10 Pro virtual machine in Azure named <code>flytrap1</code>. Intentionally disabled all firewall rules and built-in security features to make the VM an attractive target for attackers scanning the internet for vulnerable endpoints.</p>

<h3>2. Capturing Attack Data</h3>
<p>Monitored the <strong>Windows Event Viewer Security logs</strong> for Event ID 4625 (failed login attempts). Each event captured critical information including:</p>
<ul>
  <li>Attempted usernames</li>
  <li>Source IP addresses</li>
  <li>Timestamps</li>
</ul>

<h3>3. Enriching Data with Geolocation</h3>
<p>Leveraged an <strong>IP Geolocation API</strong> to transform raw IP addresses into actionable intelligence. For each attacker IP, the API returned:</p>
<ul>
  <li>Latitude & Longitude</li>
  <li>Country</li>
  <li>State/Province</li>
  <li>City</li>
</ul>

<h3>4. Configuring Azure Log Analytics</h3>
<p>Created a <strong>Log Analytics Workspace</strong> in Azure to ingest the custom log data. Trained the workspace by feeding it sample data from simulated failed logins. Defined <strong>custom fields</strong> to parse and extract the geolocation attributes, enhancing the platform's ability to structure incoming attack data.</p>

<h3>5. Building the SIEM in Microsoft Sentinel</h3>
<p>Connected Microsoft Sentinel to the Log Analytics Workspace. Wrote a <strong>custom query</strong> to filter the log data, ensuring completeness by omitting entries with missing fields. The cleaned dataset was then visualized using Sentinel's mapping capabilities.</p>

<h3>6. Visualizing Global Threats</h3>
<p>Configured a <strong>heat map</strong> that plots attacker locations on a world map. Each point represents a source of malicious login attempts, with the size/intensity indicating the volume of attacks from that region.</p>

<h2>Results</h2>

<p align="center">
  <img src="https://i.imgur.com/blCUwG3.jpeg" alt="Global Attack Heat Map" width="800"/>
</p>
<p align="center"><em>Heat map showing geographic distribution of failed RDP login attempts against the honeypot</em></p>

<h2> Tools & Technologies</h2>

<img src="https://img.shields.io/badge/Microsoft%20Azure-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white" />
<img src="https://img.shields.io/badge/Microsoft%20Sentinel-0078D4?style=for-the-badge&logo=microsoft&logoColor=white" />
<img src="https://img.shields.io/badge/Log%20Analytics-0078D4?style=for-the-badge&logo=microsoft&logoColor=white" />
<img src="https://img.shields.io/badge/Windows%2010%20Pro-0078D6?style=for-the-badge&logo=windows&logoColor=white" />
<img src="https://img.shields.io/badge/IP%20Geolocation%20API-orange?style=for-the-badge" />
<img src="https://img.shields.io/badge/KQL-5C2D91?style=for-the-badge&logo=microsoft&logoColor=white" />

<h2> Key Takeaways</h2>

<ul>
  <li><strong>Threat Landscape Awareness:</strong> The internet is constantly being scanned by bots and attackers probing for vulnerable systems</li>
  <li><strong>SIEM Fundamentals:</strong> Gained practical experience configuring log ingestion, custom fields, and security analytics in Azure</li>
  <li><strong>Data Enrichment:</strong> Learned to enhance raw log data with third-party APIs for deeper insights</li>
  <li><strong>Visualization:</strong> Transformed abstract security data into actionable, visual intelligence</li>
</ul>

<h2> Conclusion</h2>

<p>This project reinforced a critical truth: <strong>the internet is swarming with threats vying for access to any connected endpoint.</strong> The honeypot was under attack within minutes of deployment, with attempts originating from across the globe. This underscores the importance of:</p>

<ul>
  <li>Keeping systems patched and up to date</li>
  <li>Enabling built-in security features and firewalls</li>
  <li>Implementing strong access controls and authentication</li>
  <li>Following security best practices for online activity</li>
</ul>

<p>Protecting proprietary information requires vigilance—because someone, somewhere, is always looking for a way in.</p>
