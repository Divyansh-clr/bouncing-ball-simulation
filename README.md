# bouncing-ball-simulation
A Python-based multi-planet physics simulation tool that models projectile motion, gravity, and air drag across different celestial bodies with fully customizable user inputs
# Celestial Body Physics Simulator

A Python-based command-line tool that simulates the motion of an object dropped from a custom height under the influence of gravity and air resistance across various planets and moons in our solar system.

## Features
- **Multi-Planet Support:** Choose from Mercury, Venus, Earth, Mars, Jupiter, Saturn, Uranus, Neptune, Pluto, and moons like Moon, Titan, and Europa.
- **Full Customization:** Users can choose to use default planetary physics or input custom gravity ($g$) and air resistance ($K$) values.
- **Dynamic Parameters:** Easily adjust initial drop height, simulation steps, and object mass.
- **Data Visualization:** Generates clean, real-time height-over-time graphs using `matplotlib`.
- **Robust Error Handling:** Validates user inputs to prevent crashes.

## Tech Stack
- **Language:** Python
- **Libraries:** Matplotlib

## How to Run
1. Make sure you have Python and `matplotlib` installed:
   ```bash
   pip install matplotlib



import matplotlib.pyplot as plt
planet_data = {
    "mercury": {"g": -3.7, "K": 0.0},     
    "venus": {"g": -8.87, "K": 0.5},   
    "earth": {"g": -9.8, "K": 0.1},    
    "mars": {"g": -3.72, "K": 0.02},   
    "moon": {"g": -1.62, "K": 0.0},     
    "titan": {"g": -1.35, "K": 0.3},    
    "europa": {"g": -1.31, "K": 0.0},
    "jupiter": {"g": -24.79, "K": 0.5},   
    "saturn": {"g": -10.44, "K": 0.4},    
    "uranus": {"g": -8.69, "K": 0.3},     
    "neptune": {"g": -11.15, "K": 0.3},   
    "pluto": {"g": -0.62, "K": 0.01}    
}

def run_simulation(g, K,initial_height,total_steps,mass):
    Y = initial_height
    V = 0.0
    dt = 0.1
    M = mass
    y_history = []
    
    for i in range(total_steps):
        F_gravity = M * g
        F_drag = -K * V * abs(V)
        
        F = F_gravity + F_drag
        A = F / M
        
        V = V + A * dt
        Y = Y + V * dt
        
        if Y <= 0:
            V = -V * 0.8
            Y = 0
            
        y_history.append(Y)
        
    plt.plot(y_history)
    plt.title("Ball's Height Over Time")
    plt.xlabel("Time")
    plt.ylabel("Height")
    plt.show()

def p(x):
  print(x)

p("Available data")
p("All planets of the solar system")
p("-------------------------------------")
p("other options")
p("moon")  
p("Titan")
p("Europa")
p("Pluto")
user_input = input("Enter any planet or moon's name").strip().lower()

if user_input in planet_data:
    g_val = planet_data[user_input]["g"]
    k_val = planet_data[user_input]["K"]

    choice = input("do you want to set your garvity and air resistance? (Yes/No):").strip().lower()
    H_Choice = input("do you want to set your initial hight? (Yes/No):").strip().lower()
    S_Choice = input("do you want to set your steps? (Yes/No):").strip().lower()
    M_Choice = input("do you want to set your mass? (Yes/No):").strip().lower()

    if choice == "yes":
        g_val = float(input("Enter gravity value:"))
        k_val = float(input("Enter air resistance value:"))
    if H_Choice == "yes":
        Height = float(input("Enter initial height:"))
    else:
      Height = 20.0

    if S_Choice == "yes":
       steps = int(input("Enter total steps:"))
    else:
      steps = 100

    if M_Choice == "yes":
      mass = float(input("Enter mass:"))

    else:  
      mass = 2.0

    print(f"(Gravity: {g_val}, Air Resistance: {k_val})")
    run_simulation(g_val, k_val,Height,steps,mass)

elif user_input.isdigit(): 
      print("Invalid input: Name cannot be purely numeric.")    

else:
    print("Invalid input. Please enter a valid planet or moon name.")
