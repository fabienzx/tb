# Analyse OWASP-ZAP

- [Installation](#installation)
- [Scan](#scan)
- [Results](#results)
- [Overall configuration](#overall-configuration)


## Installation

OWASP ZAP (Zed Attack Proxy) is an open-source web application security testing tool. It is developed by the OWASP (Open Web Application Security Project), a global community dedicated to improving software security.

In order to get the OWASP-ZAP software you can either download it from their website or get their package with :

```bash
sudo apt-get install zaproxy
```

Once the installation is completed (may take several minutes) you can proceed to the application by inputing :

```bash
zaproxy
```

## Scan

A lot of possible add-on will be proposed upon entering the application.
<br>
If you wish to install additional scans/add-ons, a marketplace is available.
<br>

As for the scan, when you get on the front page of the app, you will have to select one of three option (we will select the 1st one *"Run a scan/attack"*.
<br>
You can then select the url you wish to scan, in our case localhost:8080 (thingsboard web app)
<br>
When you click *"Start the scan"*, your computer may experience some slowness.
<br>

After some minutes, you will have access to different alerts on the bottom left of ZAP.
<br>
This is where you will be able to see what has been detected, the severity of that said alert as well as the confidence of the scan.
<br>

Once that's done, you can decide to export the data (navigator), ultimately creating a html file (as well as some css) that can be access through a web browser.
<br>
That page is in fact the summary of the report that has been made thanks to the app.

## Results


