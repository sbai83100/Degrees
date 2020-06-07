# Degrees
Program that determines how many "degrees of separation" apart two actors are


## Background
According to the Six Degrees of Kevin Bacon game, anyone in the Hollywood film industry can be connected to Kevin Bacon within six steps, where each step consists of finding a film that two actors both starred in.

In this problem, we're interested in finding the shortest path between any two actors by choosing a sequence of movies that connected them. For example, the shortest path between Jennifer Lawrence and Tom Hanks is 2: Jennifer Lawrence is connected to Kevin Bacon by both starring in "X-Men: First Class," and Kevin Bacon is connected to Tom Hanks by both starring in "Apollo 13."

We can frame this as a search problem: our states are people. Our actions are movies, which take us from one actor to another (it's true that a movie could take us to multiple different actors though). Our initial state and goal state are defined by two people we're trying to connect. By using breadth-first search, we can find the shortest path from one actor to another.


## Specifications
There are two sets of CSV data files: one set in the large directory and one set in the small directory. Each contains files with the same names, and the same structure, but small is a much smaller dataset for ease of testing and experimentation.

Each dataset consists of three CSV files.

**people.csv** - each person has a unique id, corresponding with their id in IMDb's database, a name, and a birth year

**movies.csv** - each movie has a unique id, in addition to a title and the year in which the movie was released

**stars.csv** - establishes relationship between the people in people.csv and the movies in movies.csv, each row being a pair of a person_id value and movie_id value

At the top of **degrees.py**, several data structures are defined to store information from the CSV files. The **names** dictionary is a way to look up a person by their name: it maps names to a set of corresponding ids. The **people** dictionary maps each person's id to another dictionary with values for the person's **name**, **birth** year, and the set of all the **movies** they have starred in. And the **movies** dictionary maps each movie's id to another dictionary with values for that movie's **title**, release **year**, and the set of all the movie's **stars**. The **load_data** function loads data from the CSV files into these data structures.

The **main** function in this program first loads data into memory (the directory from which the data is loaded can be specified by a command-line argument). Then, the function prompts the user to type in two names. The **person_id_for_name** function retrieves the id for any person (and handles prmpting the user to clarify, in the event that multiple people have the same name). The function then calls the **shortest_path** function to compute the shortest path between the two people, and prints out the path.

The **shortest_path** function returns the shortest path from the person with id **source** to the person with the id **target**.
* Assuming there is a path from the **source** to the **target**, the function returns a list, where each list item is the next (movie_id, person_id) pair in the path from the source to the target. Each pair is a tuple of two **int**s.
* If there are multiple paths of minimum length from the source to the target, the function returns any one of them.
* If there is no possible path between two actors, the function returns **None**.
