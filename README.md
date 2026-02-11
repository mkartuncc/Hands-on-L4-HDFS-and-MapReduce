# Input: Research paper abstract

The primary objective of this paper was to incorporate the reinforcement learning technique in variable speed limit (VSL) control strategies to reduce system travel time at freeway bottlenecks. 
A Q-learning (QL)-based VSL control strategy was proposed. 
The controller included two components: a QL-based offline agent and an online VSL controller. 
The VSL controller was trained to learn the optimal speed limits for various traffic states to achieve a long-term goal of system optimization. 
The control effects of the VSL were evaluated using a modified cell transmission model for a freeway recurrent bottleneck. 
A new parameter was introduced in the cell transmission model to account for the overspeed of drivers in unsaturated traffic conditions. 
Two scenarios that considered both stable and fluctuating traffic demands were evaluated. 
The effects of the proposed strategy were compared with those of the feedback-based VSL strategy. 
The results showed that the proposed QL-based VSL strategy outperformed the feedback-based VSL strategy. 
More specifically, the proposed VSL control strategy reduced the system travel time by 49.34% in the stable demand scenario and 21.84% in the fluctuating demand scenario.

# Output: the counts of each word in the abstract

the	13

VSL	8

The	6

strategy	4

control	4

was	4

traffic	3

for	3

and	3

were	3

proposed	3

system	3

freeway	2

time	2

strategy.	2

travel	2

transmission	2

model	2

feedback-based	2

QL-based	2

controller	2

demand	2

stable	2

fluctuating	2

speed	2

cell	2

that	2

effects	2

parameter	1

limit	1

with	1

online	1

optimal	1

learning	1

Two	1

reduce	1

strategies	1

showed	1

technique	1

controller.	1

scenario.	1

long-term	1

agent	1

included	1

reinforcement	1

scenario	1

results	1

incorporate	1

compared	1

specifically,	1

Q-learning	1

paper	1

two	1

goal	1

components:	1

demands	1

evaluated	1

scenarios	1

(VSL)	1

variable	1

various	1

learn	1

overspeed	1

(QL)-based	1

outperformed	1

account	1

unsaturated	1

21.84%	1

both	1

bottlenecks.	1

recurrent	1

trained	1

More	1

achieve	1

bottleneck.	1

offline	1

objective	1

considered	1

this	1

modified	1

conditions.	1

proposed.	1

those	1

reduced	1

49.34%	1

evaluated.	1

limits	1

optimization.	1

states	1

using	1

introduced	1

drivers	1

new	1

primary	1


# WordCount-Using-MapReduce-Hadoop

This repository is designed to test MapReduce jobs using a simple word count dataset. In this project we provide a input file and then we create a maaper and reducer logic to count the occurence of each word in the given input. There are sample input and Expected output for the sample input.

## Approach and implementation
1. Mapper Logic: We use StringTokenizer to create tokens from the input file and loop it using while loop to map all the words in the input file with key value pairs. In this mapper, it will not count characters that are smaller than 3.

2. Reducer Logic: Using the output of Mapper logic we increase a variable sum value as we encounter same words and retun them. this way we will get a list of words and the number of times it occured in the input file as output.

## Setup and Execution

### 1. **Start the Hadoop Cluster**

Run the following command to start the Hadoop cluster:

```bash
docker compose up -d
```

### 2. **Build the Code**

Build the code using Maven:

```bash
mvn clean package
```

### 4. **Copy JAR to Docker Container**

Copy the JAR file to the Hadoop ResourceManager container:

```bash
docker cp target/WordCountUsingHadoop-0.0.1-SNAPSHOT.jar resourcemanager:/opt/hadoop-3.2.1/share/hadoop/mapreduce/
```

### 5. **Move Dataset to Docker Container**

Copy the dataset to the Hadoop ResourceManager container:

```bash
docker cp shared-folder/input/data/input.txt resourcemanager:/opt/hadoop-3.2.1/share/hadoop/mapreduce/
```

### 6. **Connect to Docker Container**

Access the Hadoop ResourceManager container:

```bash
docker exec -it resourcemanager /bin/bash
```

Navigate to the Hadoop directory:

```bash
cd /opt/hadoop-3.2.1/share/hadoop/mapreduce/
```

### 7. **Set Up HDFS**

Create a folder in HDFS for the input dataset:

```bash
hadoop fs -mkdir -p /input/data
```

Copy the input dataset to the HDFS folder:

```bash
hadoop fs -put ./input.txt /input/data
```

### 8. **Execute the MapReduce Job**

Run your MapReduce job using the following command: Here I got an error saying output already exists so I changed it to output1 instead as destination folder

```bash
hadoop jar /opt/hadoop-3.2.1/share/hadoop/mapreduce/WordCountUsingHadoop-0.0.1-SNAPSHOT.jar com.example.controller.Controller /input/data/input.txt /output1
```

### 9. **View the Output**

To view the output of your MapReduce job, use:

```bash
hadoop fs -cat /output1/*
```

### 10. **Copy Output from HDFS to Local OS**

To copy the output from HDFS to your local machine:

1. Use the following command to copy from HDFS:
    ```bash
    hdfs dfs -get /output1 /opt/hadoop-3.2.1/share/hadoop/mapreduce/
    ```

2. use Docker to copy from the container to your local machine:
   ```bash
   exit 
   ```
    ```bash
    docker cp resourcemanager:/opt/hadoop-3.2.1/share/hadoop/mapreduce/output1/ shared-folder/output/
    ```
3. Commit and push to your repo so that we can able to see your output


## Sample Input: 
 ```bash
   Hello world
   Hello Hadoop
   Hadoop is powerful
   Hadoop is used for big data
   ```

## Expected output: 
 ```bash
Hadoop 3
Hello 2
used 1
for 1
big 1
data 1
powerful 1
world 1
   ```
