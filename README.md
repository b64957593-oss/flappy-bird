🐦 Flappy Bird AI with NEAT

A Flappy Bird game where the birds learn to play by themselves. Instead of coding the rules, the project uses NEAT (NeuroEvolution of Augmenting Topologies) to evolve neural networks over many generations until a bird can fly through the pipes without crashing.

Built with Python, Pygame and NEAT-Python.

🧠 How It Works
A population of birds is created, each controlled by its own small neural network.
Every frame, the network looks at the game and decides: flap or don't flap.
Birds earn fitness for surviving and passing pipes. Crashed birds are removed.
The best networks are mixed and mutated to create the next generation.
This repeats until a bird reaches the target score.

Network inputs and output

Type	Value
Input	Bird's Y position
Input	Distance to the top of the next pipe opening
Input	Distance to the bottom of the next pipe opening
Output	Flap if the value is greater than 0.5 (tanh)
🛠 Installation

Requires Python 3.8+.

bash
git clone https://github.com/<your-username>/flappy-bird-neat.git
cd flappy-bird-neat
pip install pygame neat-python
▶️ Usage
bash
python main.py

A window opens and the birds start training. Watch the generation counter go up as they improve. Press Esc to quit.
