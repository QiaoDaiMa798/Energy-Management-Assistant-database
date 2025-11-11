# Energy-Management-Assistant-database  
Store the experimental and practical application data in the research of the energy management assistant  


# Documentation for Weaving Domain Datasets and Knowledge Graph Resources  


## Project Overview  
This project open-sources datasets and knowledge graph construction resources in the weaving domain (textile machinery and processes), including energy consumption prediction model fine-tuning datasets, process parameter analysis model fine-tuning datasets, domain entity sets (NER), and entity relationship sets (RE). All these resources are collected from actual weaving production scenarios and can be used for tasks such as fine-tuning vertical large models in the weaving domain, knowledge graph construction, and intelligent prediction and analysis, providing data support for research related to intelligent textile manufacturing.  


## Dataset Details  


### 1. Vertical Large Model Fine-Tuning Datasets for Energy Consumption  
Including `energy_consumption_train.json` (training set) and `energy_consumption_valid.json` (validation set), which are used to train and validate energy consumption prediction models in the weaving process.  

#### Data Structure  
- **Input Field (`input`)**: In dictionary format, containing key parameters of the weaving process:  
  - `run_minute`: Running time (minutes)  
  - `stop_minute`: Downtime (minutes)  
  - `product_meter`: Output (meters)  
  - `efficiency`: Efficiency (%)  
  - `rpm`: Rotational speed (revolutions per minute)  
  - `weft_t`: Weft stop time (seconds)  
  - `warp_t`: Warp stop time (seconds)  
  - `weft_c`: Number of weft stops  
  - `warp_c`: Number of warp stops  
  - `energy_consumption`: Energy consumption (kWh, used as the target value for the model)  

- **Output Field (`output`)**: In string format, specifying the specific energy consumption value of the current shift.  

#### Example (Training Set)  
```json  
{
  "instruction": "This shift lasts for 8 hours, with a total of 78 looms participating in production. The specific production details are as follows: 190 spray C/T32/2*32/2*100*53*63\"2/1 anti-static grid 0.8*0.8HZW, 1........."
  "input": "dict: {run_minute:1951992,stop_minute:286266,product_meter:34884,efficiency:86.99,rpm:420,weft_t:104328,warp_t:101424,weft_c:1764,warp_c:599,energy_consumption:1067}",  
  "output": "The specific energy consumption of this shift is 1067kWh."  
}  
```  

#### Usage  
- Used for fine-tuning energy consumption prediction models to achieve accurate energy consumption prediction based on weaving process parameters.  
- Supports research on energy consumption optimization and energy efficiency evaluation of weaving equipment.  


### 2. Vertical Large Model Fine-Tuning Datasets for Processes  
Including `craft_list_train.json` (training set) and `craft_list_valid.json` (validation set), which are used to train and validate models for correlating weaving process parameters with processing status.  

#### Data Structure  
- **Instruction Field (`instruction`)**: In string format, describing the standard processing technology of fabrics, including:  
  - Fabric specifications (e.g., "340 denier C/T (50/50) 40*40*140*100*120\" 1-inch satin strip fabric")  
  - Process parameters (warp/weft density, shrinkage rate, tension, loom speed, etc.).  

- **Input Field (`input`)**: In dictionary format, containing actual processing parameters:  
  - Basic process parameters (`warp_density`, `weft_density`, `warp_shrink`, etc.)  
  - Production status parameters (`run_minute`, `stop_minute`, `product_meter`, `efficiency`, etc.)  
  - Fault parameters (number of weft stops `weft_c`, number of warp stops `warp_c`, etc.).  

- **Output Field (`output`)**: In string format, describing the actual processing status, including running time, output, efficiency, downtime, and evaluation of processing complexity and stability.  

#### Example (Training Set)  
```json  
{  
  "instruction": "The standard processing technology for the 340-inch denier C/T (50/50) 40*40*140*100*120\" 1-inch satin strip fabric follows. The warp density is 551 threads per 10cm...",  
  "input": "dict: {warp_density:551,weft_density:394,nominal_layout:305,warp_number:16788,...rpm:434,weft_t:0,warp_t:4,weft_c:51,warp_c:4}",  
  "output": "The fabric with an imperial specification of 340 denier C/T (50/50) 40*40*140*100*120\" 1-inch satin strip fabric has the following actual processing status: running time of 20414s... Its processing complexity is high and production stability is poor."  
}  
```  

#### Usage  
- Used for fine-tuning process analysis models to predict processing status (efficiency, stability, etc.) from process parameters.  
- Supports research on weaving process optimization and production stability evaluation.  


### 3. Weaving Knowledge Graph Entity Set (`NER.json`)  
Defines core entity categories and instances in the weaving domain knowledge graph, providing a foundation for constructing knowledge graph nodes.  

#### Entity Categories and Examples  
- **Weaving Machine Models**: e.g., "Toyota JAIS-150T-T Air-Jet Loom", "SGC761A Circular Loom".  
- **Process Parameters**: e.g., "Main Nozzle Pressure Fluctuation Range ±0.02MPa", "Loom Rotational Speed", "Warp Tension Set to 12-15N".  
- **Energy Consumption Parameters**: e.g., "Air Compressor Energy Consumption Ratio", "Main Nozzle Energy Consumption Ratio 18%-22%", "Air Consumption of Single Auxiliary Nozzle per Hour 8-12m³".  
- **Transmission Components**: e.g., "Transmission Pulley", "Transmission Chain Drive Mechanism", "Transmission Ball Bearing".  
- **Air Supply System Components**: e.g., "Air Supply System Main Weft Insertion Nozzle", "Compressed Air Source".  

#### Usage  
- Serves as the "node" foundation of the knowledge graph for building a weaving domain entity library.  
- Supports natural language processing tasks such as entity recognition and entity linking.  


### 4. Weaving Knowledge Graph Entity Relationship Set (`RE.json`)  
Defines core relationships between entities in the weaving domain, providing a foundation for constructing edges in the knowledge graph.  

#### Relationship Categories and Examples  
- **Process Parameters**: e.g., "Diamond Metal Mesh Weaving Machine Flat Plate Rotating Speed 600r/min" and "Process parameters: humidity 85%, temperature 40℃".  
- **Environmental Conditions**: e.g., "Diamond Metal Mesh Weaving Machine Spindle" and "High temperature and high humidity (humidity 90%, temperature 50℃) + severe vibration environment".  
- **Fault Frequency**: e.g., "Diamond Metal Mesh Weaving Machine Flat Plate" and "Air flow diffusion fault frequency ≤0.8 times/day".  
- **Contain**: e.g., "air-jet loom air system" and "contains heald frame, heald lever, pattern mechanism".  
- **Reduce/Improve**: e.g., "lightweight heald frame" and "reduce unit energy consumption of dobby machine by 10%"; "wavelet neural network" and "improve bearing diagnosis accuracy to 100%".  
- **Energy Consumption Composition Ratio**: e.g., "total energy consumption of dobby machine" and "inertia energy consumption of opening mechanism accounts for 40%".  

#### Usage  
- Serves as the "edge" foundation of the knowledge graph for constructing semantic associations between entities.  
- Supports tasks such as relationship extraction and knowledge reasoning, facilitating applications like weaving domain knowledge question-answering and intelligent diagnosis.  


## Data Sources  
All datasets are derived from actual production and experimental data of weaving equipment (e.g., air-jet looms, rapier looms), structured and organized for academic research to ensure data authenticity and domain specificity.  


## Usage Recommendations  
1. **Model Fine-Tuning**:  
   - Energy consumption datasets can be used to train regression models for predicting energy consumption in the weaving process.  
   - Process datasets can be used to train sequence generation or classification models for evaluating processing complexity and stability.  

2. **Knowledge Graph Construction**:  
   - Combine NER entities and RE relationships to build a weaving domain knowledge graph using graph databases (e.g., Neo4j).  
   - Can be extended to scenarios such as intelligent retrieval and fault diagnosis reasoning.  

3. **Data Expansion**:  
   - Datasets can be combined with real-time sensor data from weaving equipment to improve model generalization ability.  
   - The knowledge graph can be extended to more textile domain concepts through entity linking technology.  


## Notes  
- Equipment parameters and process indicators in the data are experimental values under specific scenarios; adjustments should be made based on specific application scenarios when in use.  
- Entity and relationship definitions are based on core knowledge in the weaving domain and can be further expanded according to research needs.
