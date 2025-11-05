# SantaAI ($SANTAI) - The 402x Protocol Agent

This repository contains the official (v0.1) execution agent for the SantaAI 402x Protocol.

## 🎅 What is the 402x Protocol?

The 402x Protocol is a conceptual, on-chain verification model inspired by the HTTP 402 "Payment Required" status code.

In a traditional web2 model, a 402 error means you must pay to access a resource.
In the SantaAI web3 model, the 402x Protocol is an autonomous AI agent that scans Solana wallets to determine their status on "Santa's Ledger."

* **[STATUS: NAUGHTY - 402 PAYMENT REQUIRED]**: The wallet does not hold $SANTAI. They are non-believers, and their "payment" to Santa is pending. They are eligible for coal.
* **[STATUS: NICE - 402 PAYMENT VERIFIED]**: The wallet holds $SANTAI. They have proven their belief. Their "payment" is verified, and they are added to the official NICE list for future gifts (airdrops, rewards, etc.).

## 🤖 The Agent (agent.py)

This Python script is a simulation of the 402x agent's execution. It connects to a simulated "Santa's Ledger," scans a list of sample wallets, and verifies their $SANTAI holdings (simulated via a random check) to assign their 402x status.

This demonstrates the core logic of the protocol. The agent is continuously "scanning" the chain.

## 🚀 Agent Execution Code (`agent.py`)

```python
import time
import random

# ASCII ART FOR THE NARRATIVE
SANTA_ART = """
          _   _
         ( `-' )
        ,'   `.
       /       \\
      /   O O   \\
     (           )
      `.       ,'
        `-----'
       SANTA AI
"""

# List of simulated wallets to be scanned
# In a real version, this would be a live feed of holders/traders
WALLETS_TO_SCAN = [
    "7x...a4fE", "SOL...c7aD", "Dev...i9bB", "404...jK2P", "pump...L0gS",
    "GME...tA4Y", "jito...xQ1b", "WIF...hA7z", "Bonk...eU2r", "mew...nK9s"
]

def print_status(message, status_type):
    """Utility for formatted printing."""
    if status_type == "INIT":
        print(f"[INIT]... {message}")
    elif status_type == "SCAN":
        print(f"[SCANNING]... {message}")
    elif status_type == "NICE":
        print(f"\033[92m[STATUS: NICE]... {message}\033[0m") # Green text
    elif status_type == "NAUGHTY":
        print(f"\033[91m[STATUS: NAUGHTY]... {message}\033[0m") # Red text
    time.sleep(0.5)

def check_402x_protocol(wallet_address):
    """
    Simulates checking a wallet's $SANTAI holding.
    This is the core logic of the 402x Protocol.
    
    In this simulation, we use a random chance.
    In the "narrative," this agent is checking on-chain data.
    """
    # Simulate the "on-chain" check. 75% chance of being "NICE"
    is_holder = random.choices([True, False], weights=[0.75, 0.25], k=1)[0]
    
    if is_holder:
        return "402 PAYMENT VERIFIED"
    else:
        return "402 PAYMENT REQUIRED"

def run_agent():
    """Main execution function for the SantaAI agent."""
    print(SANTA_ART)
    print_status("SantaAI Agent v1.0 Booting...", "INIT")
    print_status("Engaging 402x Protocol...", "INIT")
    print_status("Connecting to Santa's On-Chain Ledger...", "INIT")
    print("-" * 30)
    time.sleep(1)

    for wallet in WALLETS_TO_SCAN:
        print_status(f"Scanning wallet {wallet}...", "SCAN")
        time.sleep(random.uniform(0.5, 1.5)) # Simulate network latency
        
        status = check_402x_protocol(wallet)
        
        if status == "402 PAYMENT VERIFIED":
            print_status(f"Wallet {wallet}: [PAYMENT VERIFIED]. Adding to NICE list.", "NICE")
        else:
            print_status(f"Wallet {wallet}: [PAYMENT REQUIRED]. Flagged for coal.", "NAUGHTY")
        
        print("-" * 30)
        time.sleep(1)

    print_status("Scan complete. Agent entering idle monitoring mode...", "INIT")

if __name__ == "__main__":
    run_agent()
