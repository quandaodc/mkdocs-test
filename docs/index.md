# Generative Service
There are 3 tasks in this service, the note of each task is presented as follow:

## Automatically generate table description

In the **auto_description** task, aside from the dataset name, this task also require the dataset sample called *row_data*. The type of the row_data is string instead of a DataFrame, there are two reasons for this:

- This task is in the adding data feature on the app side. It means that the provided data has not been saved in our database. Hence, it is hard for ML components to load it if we use DataFrame as an input.
- A string can be used directly in this task's pipeline. Hence, there is no further preprocess needed.

The row_data is defined by the dataset transformation. Transform the data frame into a string defined by:

- row_i (i = 1,2,…,5): the order of row
- |: separating values in 1 row
- [SEP]: separating each row

Example: the row_data of a dataset with 10 columns is:

    row_1: |1xLMexpeeTKQ20SwGMaGSK|Wild Child|48|['austin americana', 'austindie', 'folk-pop', 'indie folk', 'stomp and holler']|156767|austin americana|austindie|folk-pop|indie folk|stomp and holler|
    [SEP]row_2: |3dkbV4qihUeMsqN4vBGg93|Al Green|63|['classic soul', 'funk', 'memphis soul', 'soul', 'soul blues', 'southern soul']|1897910|classic soul|funk|memphis soul|soul|soul blues|
    [SEP]row_3: |6K4qT7qjaR6q5SqwQ1oA3o|Yami Bolo|33|['deep ragga', 'lovers rock', 'modern reggae', 'reggae', 'roots reggae']|22221|deep ragga|lovers rock|modern reggae|reggae|roots reggae|
    [SEP]row_4: |2D9Oe8R9UhbMvFAsMJpXj0|Kölsch|51|['danish electronic', 'danish techno', 'deep euro house', 'melodic techno', 'minimal techno']|226006|danish electronic|danish techno|deep euro house|melodic techno|minimal techno|
    [SEP]row_5: |1Ih0fEQQsy9EeAJbYEeQRa|Avantasia|52|['fantasy metal', 'german metal', 'german power metal', 'gothic symphonic metal', 'metal', 'opera metal', 'power metal', 'speed metal', 'symphonic metal']|434195|fantasy metal|german metal|german power metal|gothic symphonic metal|metal|[SEP]


## Automatically suggest the column names of the data

In this task, there is one point that we need to note, the column_data. It is a dictionary/JSON which is transformed from the original dataset

Example: the column_data of the dataset having 8 columns

    {'column_1': ['1993-06-02', '2000-09-03', '1993-05-16', '2003-03-29', '1984-10-17'],
    'column_2': ['Norway', 'Hungary', 'Kuwait', 'France', 'Netherlands'],
    'column_3': ['England', 'Italy', 'Macau', 'Malta', 'Hungary'],
    'column_4': ['Norway', 'Italy', 'Kuwait', 'France', 'Netherlands'],
    'column_5': ['Lars Bohinen', 'Filippo Inzaghi', 'Ali Marwi', 'Thierry Henry', 'Wim Kieft'],
    'column_6': [48.0, 35.0, 11.0, 38.0, 19.0],
    'column_7': [False, False, False, False, False],
    'column_8': [False, False, False, False, False]}

## Define the relationship between a pair of column

In this task, there is also one point that we need to note, the sample_data. It is a dictionary/JSON which is transformed from the original dataset. Note the the keys now are the actual name of columns

Example: the column_data of the dataset having 8 columns

    {'date': ['1993-06-02', '2000-09-03', '1993-05-16', '2003-03-29', '1984-10-17'],
    'home_team': ['Denmark', 'Argentina', 'Spain', 'Poland', 'Mexico'],
    'away_team': ['Greece', 'Bulgaria', 'Bulgaria', 'Moldova', 'Panama'],
    'team': ['Denmark', 'Argentina', 'Spain', 'Poland', 'Panama'],
    'scorer': ['Lars Bohinen', 'Filippo Inzaghi', 'Ali Marwi', 'Thierry Henry', 'Wim Kieft'],
    'minute': [55.0, 4.0, 90.0, 81.0, 48.0],
    'own_goal': [False, False, False, False, False],
    'penalty': [False, False, False, False, False]}
