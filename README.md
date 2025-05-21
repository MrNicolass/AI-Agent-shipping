<p align="center">
    <img loading="lazy" src="https://files.engaged.com.br/5db0810e95b4f900077e887e/account/5db0810e95b4f900077e887e/xMCS8NFKTMqwhefy8WLd_catolica-horizontal.png" width="300">
</p>

# Agent Shipping

This project simulates an urban delivery system on a 4x4 grid using two intelligent agents that make decisions based on simple heuristics and natural language. The goal is to demonstrate how Artificial Intelligence techniques can be applied to real-world scenarios.

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

That's it! Now just follow the simulation in your console and enjoy!