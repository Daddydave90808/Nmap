# Nmap
# This Python script allows you to perform an enumeration on multiple hosts, and the intensity of each Nmap scan

import subprocess
import os

def run_nmap(host, discovery_level):
    output_folder = "nmap_reports"
    os.makedirs(output_folder, exist_ok=True)
    output_file = os.path.join(output_folder, f"{host}_report.txt")

    nmap_command = f"nmap -{discovery_level} -oN {output_file} {host}"
    subprocess.run(nmap_command, shell=True)

def main():
    hosts = []
    max_hosts = 10

    print("Enter up to 10 hosts (one per line, empty line to finish):")
    for _ in range(max_hosts):
        host = input("Host (or press Enter to finish): ")
        if not host:
            break
        hosts.append(host)

    for host in hosts:
        print(f"Select discovery level for {host}:")
        print("1. Basic Scan (-sP)")
        print("2. Quick Scan (-sV)")
        print("3. Full Scan (-p-)")
        choice = input("Enter choice (1, 2, or 3): ")

        if choice == "1":
            run_nmap(host, "sP")
        elif choice == "2":
            run_nmap(host, "sV")
        elif choice == "3":
            run_nmap(host, "p-")
        else:
            print("Invalid choice. Skipping host.")

    print("Nmap scans completed. Reports are stored in the 'nmap_reports' folder.")

if __name__ == "__main__":
    main()
