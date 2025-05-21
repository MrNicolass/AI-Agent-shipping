<p align="center">
    <img loading="lazy" src="https://files.engaged.com.br/5db0810e95b4f900077e887e/account/5db0810e95b4f900077e887e/xMCS8NFKTMqwhefy8WLd_catolica-horizontal.png" width="300">
</p>

# Agent Shipping

This project simulates an urban delivery system on a 4x4 grid using two intelligent agents that make decisions based on simple heuristics and natural language. The goal is to demonstrate how Artificial Intelligence techniques can be applied to real-world scenarios, it was built in the software engineering degree of Católica University in Jaraguá do Sul, Brazil.

## 1. Objective

Create a simulation where two autonomous agents named "Ana" and "Beto" (A and B on the map) move on a 4x4 grid, trying to reach their destinations while avoiding collisions (in most cases) and always respecting the boundaries of the environment. The movement is guided by an LLM model (Gemma2-9b-it via Groq API), which analyzes the options and chooses the next move.

## 2. Artificial Intelligence Used

- **LLM Models (Language Model):** Each agent is controlled by the same LLM model but uses separate "chats", receiving movement options and deciding its next step while avoiding collisions;
- **Asynchronous Coordination:** The two agents act alternately in turns, orchestrated by a proxy agent without human intervention.

## 3. Project Structure

```
Agent-shipping/
├── main.py
├── .env
├── requirements.txt
├── README.md
```

## 4. Technologies Used

- Python 3.10+;
- [AutoGen](https://github.com/microsoft/autogen) (Interactive AI agents);
- Groq API with Gemma2-9b-it model;
- `dotenv` library for reading environment variables.

## Modelos LLM Suportados

You can change the model used by editing the `"model"` field in the `AIagentsShipping.py` file on `llm_config`. Examples of models supported by Groq:

- `gemma2-9b-it`
- `llama-3.1-8b-instant`
- `llama-3.3-70b-versatile`

Just remember to check if the model answers with text! Check the [Groq documentation](https://console.groq.com/docs/models) for the full list.

## 5. Customizing the Simulation

You can change the grid size, initial positions, and agent goals by editing the following lines in `AIagentsShipping.py`:

```python
world = World(width=4, height=4)
ag1 = Agent("Ana", [3, 0], [0, 3])
ag2 = Agent("Beto", [0, 3], [3, 0])
```

**Remember:** The first array (second parameter) for each agent represents its starting position, and the second array is its goal position.

## 6. How to Run the Project

1. Clone the repository;

2. **Create and activate a virtual environment (optional):**
    ```bash
    python -m venv venv
    venv\Scripts\activate
    ```

3. **Install the dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

4. **Set up the API Key:**
    - Create a `.env` file in the project root.
    - Add your Groq key:
      ```
      GROQ_API_KEY=your_groq_key
      ```

5. **Run the simulation:**
    ```bash
    python main.py
    ```

## 7. Submission Guidelines and Report

### 7.1. Code Commentary and Thought Process

Here is a summary of the thought process and the functionality of each component:

- **Environment Variable Loading:**  
  Uses `dotenv` to load the Groq API key from a `.env` file, ensuring security and flexibility.
 
- **LLM Model Configuration:**  
    The `llm_config` dictionary specifies which LLM model will be used (default: `gemma2-9b-it`) and sets parameters such as `temperature` (controls randomness in responses) and `max_tokens` (limits the length of generated outputs). Adjusting these parameters allows you to fine-tune the agents' behavior and response style.

- **World Class:**  
  Represents the 4x4 environment where agents move. It includes methods to add agents, update their positions, and display the grid in the console.

- **Agent Class:**  
  Each agent has a name, position, and goal. The `move_with_action` method executes the movement according to the LLM's response, ensuring the agent does not leave the grid boundaries.

- **LLM Agent Creation:**  
  Two agents (`DeliveryAgentAna` and `DeliveryAgentBeto`) are instantiated using AutoGen, each with specific instructions to decide the next move.

- **User Proxy:**  
  The `UserProxyAgent` automates communication between the code and the LLM agents, with no human intervention required.

- **Main Loop:**  
  While both agents have not reached their goals, the code alternates between them, requesting the next move from the LLM and updating the world state.

### 7.2. Methods, Findings, and Conclusions

#### Methods

- **LLM-based Simulation:**  
  Each agent makes movement decisions based on prompts sent to the language model, considering its position, goal, and the other agent's position.
- **Collision and Boundary Avoidance:**  
  System instructions ensure agents do not collide or leave the grid.
- **Real-time Visualization:**  
  The grid is updated and displayed at each move, allowing step-by-step tracking of the simulation.

#### Findings

- Using LLMs for decision-making in simple environments is feasible and allows simulating autonomous agent behavior;
- Turn alternation and explicit communication of agent states are sufficient to avoid collisions in most cases;
- The system is easily customizable for different grid sizes, initial positions, and goals.

#### Conclusions

- The project demonstrates, in a didactic way, how intelligent agents can be orchestrated by language models to solve navigation and delivery tasks;
- The code is modular, well-commented, and can be expanded to more complex scenarios, such as multiple agents or obstacles in the grid;
- Integration with the Groq API and the use of AutoGen make the system flexible for testing different LLM models.

### 7.3. How the Code Works

- **Initialization:** Loads configurations and prepares the environment;
- **Execution:** Alternates between agents, requesting decisions from the LLM and updating the world state;
- **Completion:** Displays a success message when deliveries are completed.

---

**Summary:**  
The code implements a clear and efficient simulation of autonomous agents in a grid, using LLMs for decision-making. The project is easily adaptable and serves as a foundation for studies in distributed AI and multi-agent coordination.