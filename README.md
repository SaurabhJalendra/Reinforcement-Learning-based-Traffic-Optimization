# Reinforcement Learning-based Traffic Optimization

This project implements an intelligent traffic flow optimization system using Deep Reinforcement Learning (DRL) techniques. The system adaptively controls vehicle speed and lane changes to enhance traffic efficiency, reduce congestion, and improve road safety.

## Project Overview

The project develops and compares two Reinforcement Learning approaches:
- Deep Q-Network (DQN)
- Actor-Critic Network

Both agents learn to optimize traffic flow by making real-time decisions about vehicle speed and lane changes based on the surrounding traffic conditions.

## Features

- Real-time vehicle control optimization
- Multi-agent reinforcement learning
- Adaptive speed regulation
- Intelligent lane change decisions
- Safety-aware decision making
- High-frequency state updates (10 Hz)

## State Space

The environment state consists of 8 key features:

| Feature | Description | Unit |
|---------|-------------|------|
| Vehicle Speed | Current velocity | m/s |
| Vehicle Acceleration | Rate of speed change | m/s² |
| Lane Position | Current lane identifier | - |
| Space Headway | Distance to preceding vehicle | m |
| Time Headway | Time gap to preceding vehicle | s |
| Vehicle Class | Type of vehicle | - |
| Global X | X-coordinate in global frame | m |
| Global Y | Y-coordinate in global frame | m |

## Action Space

The agent can perform 5 distinct actions:

| Action | Description | Conditions | Change |
|--------|-------------|------------|---------|
| 0 | Maintain speed | No conditions | 0 m/s |
| 1 | Increase speed | Space_Headway ≥ 15m | +2 m/s |
| 2 | Decrease speed | Space_Headway < 10m | -2 m/s |
| 3 | Change left | Left lane exists & unoccupied | Lane shift |
| 4 | Change right | Right lane exists & unoccupied | Lane shift |

## Safety Parameters

- **Safe Following Distance**: Minimum 15 meters from preceding vehicle
- **Collision Risk Zone**: Less than 5 meters gap
- **Target Speed**: 27 m/s (approximately 60 mph)

## Reward Function

The reward function balances optimal speed maintenance with collision avoidance:

R = (10 - |V_t - V_optimal|) - P_collision

Where:
- V_t = Current vehicle speed (m/s)
- V_optimal = 27 m/s (target speed)
- P_collision = Penalty factor
  - 20 if Space_Headway < 5m (high collision risk)
  - 0 otherwise

## Implementation Details

### Dependencies
- TensorFlow/Keras for DRL implementation
- NumPy for numerical computations
- Pandas for data handling
- Matplotlib for visualization

### Dataset
- High-frequency trajectory data (10 Hz)
- Each frame represents 0.1-second interval
- Rich vehicle state information

## Getting Started

1. Clone the repository:
```bash
git clone https://github.com/yourusername/Reinforcement-Learning-based-Traffic-Optimization.git
```

2. Install required dependencies:
```bash
pip install tensorflow numpy pandas matplotlib
```

3. Run the Jupyter notebook:
```bash
jupyter notebook "Traffic_Flow_Optimization final.ipynb"
```

## Results

The project demonstrates:
- Improved traffic flow efficiency
- Reduced congestion through intelligent speed control
- Enhanced safety through collision avoidance
- Adaptive behavior in various traffic conditions

## Documentation

Detailed documentation is available in:
- `Traffic_Flow_Optimization final.ipynb` - Main implementation notebook
- `Group_111-TrafficOptimization.pdf` - Project documentation

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- Dataset provided by [Dataset Source]
- Based on research in Deep Reinforcement Learning for traffic optimization
- Inspired by modern traffic management systems