
# Comprehensive IP Address Lists

This repository is a central, auto-updating source for IP address lists. The goal is to provide accurate, up-to-date IP lists for countries and online game servers, suitable for use in firewalls, routing tools, security research, and other network applications.

## 📂 Folder Structure

This project contains the following data:

-   `ipv4-countries/`: Contains **IPv4** address lists, categorized by country.
    
-   `ipv6-countries/`: Contains **IPv6** address lists, categorized by country.
    
-   `game-servers/`: Contains IP address lists for online game servers.
    
    -   `steam/`: IP lists for servers of all games on the **Steam** platform.
        

## ⚙️ How It Works & Data Sources

This repository is automatically updated every **30 minutes** by a **GitHub Actions Workflow** to ensure the data is always fresh and accurate.

### 1. Country IP Blocks

-   **Source:** Data for this section is sourced from the reputable [herrbischoff/country-ip-blocks](https://github.com/herrbischoff/country-ip-blocks "null") repository.
    
-   **Format:** Files are in `.cidr` format and categorized by their two-letter country code (e.g., `US.cidr` for the United States).
    

### 2. Steam Game Servers

-   **Source:** The server list is dynamically fetched directly from the **Steam API**.
    
-   **Process:**
    
    1.  First, the complete list of all games on Steam is fetched via the `GetAppList` API.
        
    2.  Then, for each game, the list of active servers is queried using the `GetSDRConfig` API.
        
    3.  If active servers are found for a game, their IP addresses (both IPv4 and IPv6) are saved into a file named after the game (e.g., `Counter-Strike_2.cidr`).
        

## 💡 How to Use

You can use these lists in scripts, firewalls (like `iptables` or `pfSense`), or any other tool that requires traffic differentiation based on geolocation or a specific service.

For example, to block all IPs from a specific country using a Linux firewall:

```
# Example: Block all IPs from a hypothetical country (e.g., country code XX)
for ip in $(cat ipv4-countries/XX.cidr); do
  iptables -A INPUT -s "$ip" -j DROP
done

```

## 🤝 Contribution & Feedback

If you have suggestions or ideas to improve this project, please feel free to open a new [Issue](https://github.com/mo13ammad/CountryIP/issues "null").
