🐦 Flappy Bird AI: Learning to Fly with NEAT

A Flappy Bird clone where the birds teach themselves to play. Instead of hand-coding the rules, this project uses NEAT (NeuroEvolution of Augmenting Topologies) to evolve neural networks that learn when to flap, generation after generation.

Built with Python, Pygame and NEAT-Python.

📖 Table of Contents
How It Works
Features
Installation
Usage
Project Structure
Configuration
What to Expect
Troubleshooting
Ideas to Extend
Contributing
License
Acknowledgements
🧠 How It Works

NEAT is a genetic algorithm that evolves both the weights and the structure of a neural network. It starts with tiny, simple networks and only adds neurons and connections when they actually improve performance.

text
  Bird Y position ────────────┐
                              │
  Distance to top pipe ───────┼──▶  [ evolving network ]  ──▶  JUMP?
                              │                                (output > 0.5 → flap)
  Distance to bottom pipe ────┘
The training loop
Spawn a population. Every bird is controlled by its own neural network (a genome).
Play. Each frame, a bird feeds what it "sees" into its network. If the output passes the threshold, it flaps.
Score fitness. Birds earn points for surviving and passing pipes, and are removed when they crash.
Select and evolve. The best genomes are kept, crossed over and mutated to form the next generation.
Repeat until a bird reaches the fitness threshold or the generation limit.
Network inputs and output
Type	Value	Meaning
Input	Bird's Y position	How high or low the bird currently is
Input	Distance to top pipe opening	Vertical gap to the top of the next gap
Input	Distance to bottom pipe opening	Vertical gap to the bottom of the next gap
Output	Jump signal (tanh)	The bird flaps if the output is above 0.5
Fitness function
Event	Fitness change
Staying alive (per frame)	+0.1
Passing a pipe	+5
Hitting a pipe, floor or ceiling	-1 (genome removed)

These are the default values. Change them in the game code to see how the birds' behavior changes.

✨ Features
🎮 Flappy Bird clone built with Pygame
🧬 Evolves a whole population of birds with NEAT-Python
📈 Live on-screen stats: generation number, birds alive, score
⚙️ Everything tunable from one file: config-feedforward.txt
💾 Saves the best genome so you can replay the winner later
🛠 Installation
Prerequisites
Python 3.8 or newer
pip
Setup
bash
# 1. Clone the repository
git clone https://github.com/<your-username>/flappy-bird-neat.git
cd flappy-bird-neat

# 2. (Optional) Create a virtual environment
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

requirements.txt

text
pygame
neat-python
▶️ Usage
Train the AI
bash
python main.py

A window opens and the first generation starts flying (and crashing). Watch the generation counter go up as the birds get better.

Replay the best bird

(if your project saves the winning genome)

bash
python play_best.py
Controls
Key	Action
Esc	Quit the game
Space	Flap (manual play mode only)
📁 Project Structure
text
flappy-bird-neat/
├── imgs/                     # Bird, pipe, base and background sprites
├── main.py                   # Game loop + NEAT training
├── config-feedforward.txt    # NEAT configuration
├── requirements.txt          # Python dependencies
└── README.md
⚙️ Configuration

NEAT's behavior is controlled by config-feedforward.txt. The most useful settings:

ini
[NEAT]
fitness_criterion      = max
fitness_threshold      = 100    # Stop when a bird reaches this fitness
pop_size               = 50     # Birds per generation
reset_on_extinction    = False

[DefaultGenome]
num_inputs             = 3
num_hidden             = 0      # Start simple; NEAT adds nodes as needed
num_outputs            = 1
activation_default     = tanh
activation_mutate_rate = 0.0
Parameter	Effect
pop_size	Bigger populations explore more but run slower
fitness_threshold	Higher values train longer for a stronger bird
num_hidden	Starting hidden nodes (0 lets NEAT grow the topology)
activation_default	Activation function used by every neuron
📊 What to Expect

Typical training with the default settings:

Generation	What you'll usually see
1 to 3	Most birds crash into the first pipe or the floor
4 to 10	A few birds learn to time their flaps and clear pipes
10+	A winning genome appears and can fly almost indefinitely

Results vary from run to run because NEAT starts from random networks.

🩺 Troubleshooting
Problem	Fix
ModuleNotFoundError: neat	Install with pip install neat-python (not pip install neat)
Images or sprites not loading	Run the game from the project folder so relative paths work
Birds never improve	Increase pop_size or reward passing pipes more
Game runs too fast or too slow	Adjust the FPS value in the clock.tick() call
All species extinct error	Set reset_on_extinction = True in the config file
💡 Ideas to Extend
Add more inputs, such as bird velocity or horizontal distance to the next pipe
Make the game harder with faster pipes or a smaller gap
Visualize the winning network with graphviz
Use a NEAT checkpointer to pause and resume long training runs
Plot best and average fitness per generation with matplotlib
🤝 Contributing

Contributions are welcome!

Fork the repository
Create a feature branch: git checkout -b feature/your-idea
Commit your changes: git commit -m "Add your idea"
Push the branch: git push origin feature/your-idea
Open a Pull Request
📄 License

Distributed under the MIT License. See LICENSE for more information.

🙏 Acknowledgements
NEAT-Python for the NEAT implementation
Pygame for the game framework
Evolving Neural Networks through Augmenting Topologies by Kenneth O. Stanley and Risto Miikkulainen (2002), the original NEAT paper
Dong Nguyen, creator of the original Flappy Bird

Made with ❤️ and a lot of crashed birds 🐦
