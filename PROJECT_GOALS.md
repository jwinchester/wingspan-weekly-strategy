# Wingspan Weekly Strategy Optimizer

## Project Overview
The goal of this project is to develop an intelligent Python-based assistant for optimizing gameplay in *Wingspan*’s weekly challenges. Using the **Wingspan card dataset**, **game rules**, and **OpenAI API for text analysis**, this tool will calculate optimal strategies to maximize player scores against the Automa AI. The solution will simulate games, track and predict gameplay elements, and analyze card effects to help develop informed strategies.

---

## Project Requirements and Objectives

### 1. **Primary Data Sources**
   - **Wingspan Dataset**:
     - Source: [Wingspan data on GitHub by coolbutuseless](https://github.com/coolbutuseless/wingspan)
     - Description: This dataset includes comprehensive stats for bird cards and bonus cards, which are crucial for determining scoring potential, play costs, and interaction effects.
     - Data Handling: Load this dataset with `pandas` for easy manipulation and develop helper functions to access specific card attributes.
   - **Wingspan Rules**:
     - Source: [Official Wingspan Rules](https://stonemaiergames.com/games/wingspan/)
     - Description: The rules document includes essential gameplay mechanics, scoring details, Automa behavior, and card interaction guidance.
     - Integration: Functions will reference rule-based interactions to simulate scoring, end-of-round objectives, and card effects accurately.

### 2. **Project Structure and Setup**
   - **Folder Structure**:
     ```
     WingspanWeekly/
     ├── data/             # Store Wingspan dataset and rule documentation
     ├── src/              # Source code for core game logic, analysis, and simulation
     ├── tests/            # Unit and integration tests
     ├── [main.py](http://_vscodecontentref_/#%7B%22uri%22%3A%7B%22%24mid%22%3A1%2C%22fsPath%22%3A%22%2Fhome%2Fuser%2FDocuments%2FProjects%2FWingspanWeekly%2Fmain.py%22%2C%22path%22%3A%22%2Fhome%2Fuser%2FDocuments%2FProjects%2FWingspanWeekly%2Fmain.py%22%2C%22scheme%22%3A%22file%22%7D%7D)           # Entry point for running the program
     └── [requirements.txt](http://_vscodecontentref_/#%7B%22uri%22%3A%7B%22%24mid%22%3A1%2C%22fsPath%22%3A%22%2Fhome%2Fuser%2FDocuments%2FProjects%2FWingspanWeekly%2Frequirements.txt%22%2C%22path%22%3A%22%2Fhome%2Fuser%2FDocuments%2FProjects%2FWingspanWeekly%2Frequirements.txt%22%2C%22scheme%22%3A%22file%22%7D%7D)  # Project dependencies
     ```
   - **Dependencies**:
     - Key libraries: `pandas` (data manipulation), `pytest` (testing), and `openai` (API for text analysis).
     - Install dependencies by running `pip install -r requirements.txt`.

### 3. **Coding Standards and Documentation**

   #### Docstrings and Comments
   - **Docstring Structure**:
     - Include a concise, structured docstring for each function, class, and module.
     - Each docstring should include:
       - **Summary**: One-line function or class purpose.
       - **Parameters**: List of each parameter with its type and purpose.
       - **Returns**: Return type and purpose.
       - **Raises**: Exceptions raised and when.
     - Example:
       ```python
       def calculate_score(bird_data: pd.DataFrame, bonus_data: pd.DataFrame) -> int:
           """
           Calculates the total score based on bird and bonus card data.

           Parameters:
               bird_data (pd.DataFrame): DataFrame with bird card details.
               bonus_data (pd.DataFrame): DataFrame with bonus card details.

           Returns:
               int: Total score from birds and bonuses.

           Raises:
               ValueError: If data is missing or improperly formatted.
           """
       ```
   - **Comments**:
     - Add comments to clarify complex code sections or strategic design decisions.
     - Include inline comments only when necessary for readability, focusing on *why* a particular approach is used.

   #### Error Handling
   - Use `try-except` blocks to handle predictable errors (e.g., [`FileNotFoundError`](command:_github.copilot.openSymbolFromReferences?%5B%22%22%2C%5B%7B%22uri%22%3A%7B%22scheme%22%3A%22file%22%2C%22authority%22%3A%22%22%2C%22path%22%3A%22%2Fhome%2Fuser%2FDocuments%2FProjects%2FWingspanWeekly%2Ftests%2FPROJECT_GOALS.md%22%2C%22query%22%3A%22%22%2C%22fragment%22%3A%22%22%7D%2C%22pos%22%3A%7B%22line%22%3A65%2C%22character%22%3A66%7D%7D%5D%2C%22f7ee7377-6413-4d87-b77d-1ad35a345d82%22%5D "Go to definition") for data loading, [`KeyError`](command:_github.copilot.openSymbolFromReferences?%5B%22%22%2C%5B%7B%22uri%22%3A%7B%22scheme%22%3A%22file%22%2C%22authority%22%3A%22%22%2C%22path%22%3A%22%2Fhome%2Fuser%2FDocuments%2FProjects%2FWingspanWeekly%2Ftests%2FPROJECT_GOALS.md%22%2C%22query%22%3A%22%22%2C%22fragment%22%3A%22%22%7D%2C%22pos%22%3A%7B%22line%22%3A65%2C%22character%22%3A104%7D%7D%5D%2C%22f7ee7377-6413-4d87-b77d-1ad35a345d82%22%5D "Go to definition") for missing data entries).
   - Implement logging to track issues during API calls or data processing.
   - Use [`finally`](command:_github.copilot.openSymbolFromReferences?%5B%22%22%2C%5B%7B%22uri%22%3A%7B%22scheme%22%3A%22file%22%2C%22authority%22%3A%22%22%2C%22path%22%3A%22%2Fhome%2Fuser%2FDocuments%2FProjects%2FWingspanWeekly%2Ftests%2FPROJECT_GOALS.md%22%2C%22query%22%3A%22%22%2C%22fragment%22%3A%22%22%7D%2C%22pos%22%3A%7B%22line%22%3A67%2C%22character%22%3A10%7D%7D%5D%2C%22f7ee7377-6413-4d87-b77d-1ad35a345d82%22%5D "Go to definition") clauses where applicable (e.g., closing file streams).

### 4. **Core Functionalities and Simulation Goals**

   #### Game Simulation and Prediction
   - **Deck Tracking**:
     - Track both *Bird deck* and *Bonus card deck* states in real-time, updating as cards are drawn.
     - Use the fixed nature of decks to predict card availability, helping refine play strategies as unknown cards become known.
   - **Automa Actions**:
     - Implement predictive models to anticipate Automa actions based on round goals and card draw history.
     - Functions should simulate Automa scoring methods and calculate competitive moves.
   - **Dice Roll Analysis**:
     - Develop tests to determine if dice rolls are consistent or random per game session. If consistent, optimize for predictable sequences; otherwise, apply probabilistic adjustments.

   #### Strategy Optimization
   - **Scoring and Outcome Calculations**:
     - Develop scoring functions that factor in bird abilities, bonus cards, and end-of-round goals.
     - Integrate helper functions for maximizing points by evaluating all possible moves and prioritizing high-scoring options.
   - **Dynamic Strategy Updates**:
     - Build adaptive tracking of known and unknown cards to adjust strategies dynamically, incorporating real-time game data.

   #### OpenAI API Integration
   - **Purpose**:
     - Use OpenAI API to analyze card text and rules to understand complex card effects and gameplay interactions. This will help ensure accurate application of card powers and scoring mechanics.
   - **Key API Use Cases**:
     - **Text Analysis for Card Effects**:
       - Prompt the API to interpret and summarize complex or ambiguous card texts, improving function accuracy for card interactions.
       - Example prompt for Copilot or OpenAI: *"Explain how the bonus for 'omnivore expert' applies to a game round in Wingspan."*
     - **Rule Interpretation**:
       - Automate parsing of complex rule interactions, especially for bonus points or multi-card effects, ensuring all scenarios are covered.

---

## Testing Framework

   #### Unit Testing with [`pytest`](command:_github.copilot.openSymbolFromReferences?%5B%22%22%2C%5B%7B%22uri%22%3A%7B%22scheme%22%3A%22file%22%2C%22authority%22%3A%22%22%2C%22path%22%3A%22%2Fhome%2Fuser%2FDocuments%2FProjects%2FWingspanWeekly%2Ftests%2FPROJECT_GOALS.md%22%2C%22query%22%3A%22%22%2C%22fragment%22%3A%22%22%7D%2C%22pos%22%3A%7B%22line%22%3A30%2C%22character%22%3A53%7D%7D%5D%2C%22f7ee7377-6413-4d87-b77d-1ad35a345d82%22%5D "Go to definition")
   - Write unit tests for all key functions, verifying each aspect of game setup, scoring, deck tracking, and card interactions.
   - **Examples of Unit Tests**:
     - Testing `load_data()` function for correct data handling and exceptions.
     - Validating `calculate_score()` to ensure accurate point calculations based on data.
   - **OpenAI API Test Cases**:
     - Mock API calls to test responses for card effect interpretations and rule applications.

   #### Integration Testing
   - Ensure functions work together seamlessly by testing game simulation, Automa predictions, and scoring calculations in real-game scenarios.
   - **Example Integration Tests**:
     - Simulate a full game round to verify the accuracy of point tracking, card effects, and Automa scoring.

---

## Expected Outcomes

1. **Functional Wingspan Strategy Assistant**:
   - A Python-based tool capable of accurately loading data, tracking deck states, predicting Automa moves, and suggesting optimal plays for each round.

2. **Reliable and Maintainable Codebase**:
   - Code following best practices in docstring documentation, error handling, and commenting, ensuring easy maintenance and extensibility.

3. **Enhanced Game Insights**:
   - A tool that not only provides scoring predictions but also interprets complex card and rule interactions through OpenAI API integration, giving users a clear understanding of optimal game strategies.
