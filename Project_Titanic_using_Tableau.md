Titanic - Isolating the True Families using Visualization in Tableau[¶](#Titanic---Isolating-the-True-Families-using-Visualization-in-Tableau) {#Titanic---Isolating-the-True-Families-using-Visualization-in-Tableau}
==============================================================================================================================================

### Links[¶](#Links) {#Links}

-   [Titanic.TrueFamilies.1.0](https://public.tableau.com/profile/daniel1932#!/vizhome/Titanic_TheSurvived_1_0/IsolatingTrueFamilyMembers?publish=yes),
    the first version
-   [Titanic.TrueFamilies.2.0](https://public.tableau.com/profile/daniel1932#!/vizhome/Titanic_TrueFamilies_2_0/SampleSimilarityCalculation?publish=yes),
    the final version

### Summary[¶](#Summary) {#Summary}

For example, a passenger 'Andersson, Miss. Erna Alexandra' looks like a
member of 'Andersson' family. However, true 7 members of 'Andersson'
family have the same ticket '347082', the same fare '31.275',
accordingly 'Andersson, Miss. Erna Alexandra' is not the family member -
her ticket(3101281) and fare(7.925) are different and it is the same for
'Andersson, Mr. August Edvard ("Wennerstrom")' who turned out to be no
Andersson's. So, how could we segregate the true family?\
 Here I used Tableau visualization to detect passengers who have more
similarities than others based on many clues like 'Name', 'Ticket',
'Fare', 'FamilySize', 'Pclass', 'Cabin', 'Embarked'. Strong candidates
for true family were discovered - total 188 families and 370 total
members. Mostly they stayed in 1st class cabin and their survival rate
was 0.52, which is much higher than passengers traveled alone (0.28) and
even survival rate in total(0.38)

### Design[¶](#Design) {#Design}

For the visualization I was aiming, which is not for understanding the
data, but to harvest proper targets, I prepared 'SimilarityScore' data
first by calculating the similarities among the passengers using
features like 'Name', 'Ticket', 'Fare', 'FamilySize', 'Pclass', 'Cabin',
'Embarked' which can imply 'being a member of a family'. The pairing of
each 900 passengers generated about 25000 rows after filtering zero
similarity rows, and the data was exported as a csv file for Tableau
visualization.\
 In my Tableau story,

-   1st story point is an example to explain 'SimilarityScore'
    -   To have a top hovering view on many passenger pairs being
        compared, to meet the purpose of this visualization, I converted
        'PassengerId' from Dimension to Measure to contain their
        horizontal location within the screen width to easily detect
        strongly similar members. Then, each row(a GroupName) will have
        at least two PassengerId on the same horizon.
    -   Mark considerations
        -   Main features like 'Ticket', 'Name', which are most-weighted
            features to discern a family - were expressed through mark
            color and shape. Eventually, the marks that stand out from
            the rest in human eyes, strongly indicate 'family'
        -   I had many thought on the shape and color. The final choice
            is rectangle because circle and others can generate a little
            confusion when comparing two mark
        -   Other information like original name, family size, cabin,
            fare are added to Tooltip, to provide convenience when
            detecting and verifying a family members
-   2nd and 3rd are expanded chart of 1st story point for the actual
    detection of the families. Eventually at the 3rd point, true
    families are listed.
    -   A feedback enlightened me to have consistent mark style among
        the similar charts. I unified the shape and color in the final
        version.
    -   At the first version, true family lists are absent. Later at the
        final version, I included that to let the viewer look more
        closely into the result.
-   4th point might be trivial and ruining the flow of the main topic
    according to a feedback, however I think showing the distribution of
    the similarity data that I prepared, would provide more reliability
    and overall understanding of the raw data.
-   5th point reveals the conclusion. As I expected the isolated
    families have much higher survival rate and I chose bar chart for
    clear delivery of the finding

### Feedback[¶](#Feedback) {#Feedback}

Not much feedback so far through
[https://discussions.udacity.com/t/feedback-needed-for-the-project-titanic/411674](https://discussions.udacity.com/t/feedback-needed-for-the-project-titanic/411674)\
 My family and friends shared following feedbacks

#### Feedback. "You better make the mark a rectangle"[¶](#Feedback.-"You-better-make-the-mark-a-rectangle") {#Feedback.-"You-better-make-the-mark-a-rectangle"}

At the 1st version, at the 1st story point, I exemplified the graph
using differenct mark shape and color - circle and blue. This feedback
says it is inconsistent and the viewer might be confused by the
different shape and color in later worksheet. I strongly agreed and
reflected the idea to the final version.

#### Feedback. "Why do you need histogram?"[¶](#Feedback.-"Why-do-you-need-histogram?") {#Feedback.-"Why-do-you-need-histogram?"}

It makes sense in that the flow of the topic is just at the front of the
conclusion and the histogram ruins the smooth transition. However, the
histogram of 'SimilarityScore' is meant for how many there are the weak
similarities and provides a little of understanding and reliability on
the data.

#### Feedback. "What is 0 and 1 in your bar chart?"[¶](#Feedback.-"What-is-0-and-1-in-your-bar-chart?") {#Feedback.-"What-is-0-and-1-in-your-bar-chart?"}

At the 1st version, the bar chart has its column values - 0/1, which
would be unkind. I accepted. 'Calculated Field' was created as
'InGroup\_str' to have values either 'Family' or 'No Family'

#### Feedback. "Your bar chart is meaninglessly colorful"[¶](#Feedback.-"Your-bar-chart-is-meaninglessly-colorful") {#Feedback.-"Your-bar-chart-is-meaninglessly-colorful"}

The essence of the bar chart is big different survival rate. So, I
visually differentiated the survival rate but the color choise was bad -
yellow and red, which just looks like a meaningless cosmetics for the
bar. Later, I picked a same color hue.

#### Feedback. "You would be better try 'clustering' such as 'k-means clustering' to segregate family as more mathematical and objective method[¶](#Feedback.-"You-would-be-better-try-'clustering'-such-as-'k-means-clustering'-to-segregate-family-as-more-mathematical-and-objective-method) {#Feedback.-"You-would-be-better-try-'clustering'-such-as-'k-means-clustering'-to-segregate-family-as-more-mathematical-and-objective-method}

It was an objection on my method of clustering the passengers. I heard
of 'k-means clustering' at the machine learning class, but my experience
to apply that well is limited for now. I strongly hope to use the
library later, hoping a more objective and mathematically beautiful way
of clustering each families.

-   scikit-learn 'k-means clustering' :
    [http://scikit-learn.org/stable/auto\_examples/cluster/plot\_cluster\_iris.html](http://scikit-learn.org/stable/auto_examples/cluster/plot_cluster_iris.html)

#### Feedback. "What if the name has slight typos, is that ignorable?"[¶](#Feedback.--"What-if-the-name-has-slight-typos,-is-that-ignorable?") {#Feedback.--"What-if-the-name-has-slight-typos,-is-that-ignorable?"}

It was also a questioning on data preparation not visualization. I admit
that 'Andersson' and 'Anderson' might be the same and Ticket '33345' and
'3345' might be result of human mistake. Maybe I will have to invest
more time on the comparison logics. I agree.

### Resources[¶](#Resources) {#Resources}

-   References to general knowledge on passengers, ticket and cabin on
    Titanic
    -   [Titanic passenger data and its
        description](https://www.kaggle.com/c/titanic/data)
    -   Titanic Passenger names
        -   [Passenger
            name](http://titanic.wikia.com/wiki/List_of_Titanic%27s_passengers_and_crew)
        -   [Passenger name and
            cabin](https://www.encyclopedia-titanica.org/cabins.html)
-   [Titanic general information](http://www.encyclopedia-titanica.org/)
    -   324 1st class passengers, 201 survived. 277 2nd class
        passengers, 118 survived. 708 3rd class passengers, 181
        survived. 885 crew members, 212 survived. 13 postmen/musicians,
        none survived. Grand total: 2,207 on board, 712 survivors.
    -   [Titanic sailing route : S → C →
        Q](https://discovernorthernireland.com/things-to-do/attractions/titanic/titanic-sailing-route-map/)
-   In fact, there is another my analysis using Tableau - It is
    discovered from Tableau visualization that 'Ticket' starts with '1'
    such as 17759, 113806 is highly referring to 1st ticket
    class(Pclass) and likewise 'Ticket' starts with '2' or '3' means 2nd
    and 3rd ticket class for each.
    -   [My Tableau link on Titanic Ticket naming
        convention](https://public.tableau.com/profile/daniel1932#!/vizhome/Titanic_TheSurvived_Ticket-Cabin_Naming_Pattern_1_0/Fare_v_Ticket_log)
    -   [Titanic Ticket naming
        discussion](https://www.encyclopedia-titanica.org/community/threads/ticket-numbering-system.20348/)
    -   [Titanic Cabin
        naming](https://www.encyclopedia-titanica.org/cabins.html)
-   [Hide/Show Python code cell in Jupyter
    Notebook](https://stackoverflow.com/questions/27934885/how-to-hide-code-from-cells-in-ipython-notebook-visualized-with-nbviewer)
    - I composed this document on Jupyter, to include Python codes. For
    the better readability, the link introduced me a technique to hide
    the codes.

In [1]:

    from IPython.display import HTML
    HTML('''<script>
    code_show=true; 
    function code_toggle() {
     if (code_show){
     $('div.input').hide();
     } else {
     $('div.input').show();
     }
     code_show = !code_show
    } 
    $( document ).ready(code_toggle);
    </script>
    <li>To show/hide the raw python code in Supplement section, click <a href="javascript:code_toggle()">here</a>.  
    The raw code for this IPython notebook is by default hidden for easier reading.</li>''')  

Out[1]:

To show/hide the raw python code in Supplement section, click
[here](javascript:code_toggle()). The raw code for this IPython notebook
is by default hidden for easier reading.

### Supplement. Data Preparation Steps for the Visualization in Tableau[¶](#Supplement.-Data-Preparation-Steps-for-the-Visualization-in-Tableau) {#Supplement.-Data-Preparation-Steps-for-the-Visualization-in-Tableau}

To extract families, the first step is to wrangle the data in order to
tokenize features that can be then easily compared among passengers. For
example, the name 'Fortune, Mr. Charles Alexander' is tokenized as
[Alexander, Charles, Fortune] and the 'Fortune' family has 'Fortune'
token in common, and their Ticket ('19950'), Cabin('C23 C25 C27'),
Fare(263) are identical and they all embarked at 'S' and have the same
family size(6) record.\
 After extracting that elements, full cross-check among the passengers
is executed and the common elements list is saved in another table
(**dfSM**) for each pair of passengers taking a row to describe the
similarity. The number of common elements, or similarity score indicates
possibly the same family or group.

-   **df** will be accumulating clues to track family/group members.
    Every elements will be tokenized, listed and finally compared
    between every two passengers pair.

    -   Clues for similarity
        -   Ticket similarity - '**Ticket**' will be used.
        -   Name similarity - 'Name' values will be tokenized to
            '**Name\_**' column and alphabetized in the order.
        -   Fare similarity - '**Fare**' and '**Pclass**' will be used.
        -   Location similarity - '**Cabin**' and '**Embarked**' will be
            used.
        -   Family or group size - new '**FamilySize**' column will
            contain 'SibSp'+'Parch'+1(1 for self).
    -   **df** will be exported as 'titanic-data\_w.csv' for reference
        and another visualization
-   **dfSM**, a new table will list the similarity for the pairs of two
    passengers if any similarity exists.

    -   Different weight on similarity of each column will be imposed
        for the final similarity score. For example, the ticket and
        family name are strong indicators of being the same family, but
        similarity in first name or cabin is weak. Following order will
        be referenced.
        -   Name, Ticket : high
        -   Fare, FamilySize, Pclass : middle
            -   The FamilySize similarity check will allow ±2 deviation,
                because counting mistake is strongly suspected. For
                example the Andersson family has 7 passengers and
                identically FamilySize equals 7 (SibSp+Parch+1).
                However, Rice family (Ticket 382652) has 5 family
                members and FamilySize value is 6.
            -   Ticket =1601 has 7 members (seemingly all male
                passengers at similar ages) but their FamilySize is 0.
                However, when we have a glance on the other data, they
                are definitely a group tralveled together though not a
                family. So, let's just recognize the FamilySize is not
                precise.
        -   Cabin, Embarked : low
    -   **dfSM** will be exported as '**titanic-data\_similarity.csv**'
        for visualization in Tableau

Additionally, I will explore the possibility of any 'Ticket', 'Cabin'
naming pattern through Tableau visualization, using additional data
which were prepared as new columns in **df** DataFrame ( exported as
'titanic-data\_w.csv')

-   Ticket naming convention : new 'Ticket\_' column will be created to
    see any numeric pattern
-   Cabin naming convention : new 'Cabin\_' column will be created to
    investigate to see the same numeric pattern exists

#### Detail.1. Data preparation to calculate similarity among passengers[¶](#Detail.1.-Data-preparation-to-calculate-similarity-among-passengers) {#Detail.1.-Data-preparation-to-calculate-similarity-among-passengers}

In [2]:

    import pandas as pd
    import numpy as np

    %matplotlib inline
    import matplotlib.pyplot as plt
    from IPython.display import display

    pd.set_option('display.max_columns', None)  
    pd.set_option('display.max_colwidth', -1) 

    df = pd.read_csv('titanic-data.csv')
    # print(df.shape)
    # display(df.columns)
    # display(df.sample(5))

In [3]:

    """ data wrangling to prepare similarity clues  """
    # Name_ : new column, a list of break-down 'Name' to name tokens
    import nltk
    from nltk.corpus import stopwords
    import re
    def NameTokenizer(name) :
        """
        print(NameTokenizer('Louch, Mrs. Charles Miss. Alexander (Dr. Alice Adelaide Slow)'))
        RESULT :  ['Louch', 'Charles', 'Alexander', 'Alice', 'AdelaiSlow']
        """
        nameori =  name
        name = re.sub('(?:Mr|Mrs|Ms|Miss|Dr)\.*\s', '', name)
        name = re.sub('(?: Jr| de |II)', '', name)
        name = re.sub('[^a-zA-Z0-9\s]', '', name)
        words = nltk.word_tokenize(name)
        words = [word for word in words if len(word) > 1]   # remove (  ) , ; and so on 
        words = [word for word in words if not word.isnumeric()]   
        stopWords = set(stopwords.words('english'))
        wordsFiltered = []
        for w in words:
            if w not in stopWords: wordsFiltered.append(w)
        wordsFiltered.sort()
        return wordsFiltered
    # tokenize the name
    df['Name_'] = df['Name'].apply(NameTokenizer)

    # FamilySize : new column for convenience, of accessing family size (siblings/husbands/wives + children and parents and oneself)
    df['FamilySize'] = df['SibSp'] + df['Parch'] + 1

#### Detail.2. Cross-check among the passengers to calculate 'SimilarityScore'[¶](#Detail.2.-Cross-check-among-the-passengers-to-calculate-'SimilarityScore') {#Detail.2.-Cross-check-among-the-passengers-to-calculate-'SimilarityScore'}

In [4]:

    """ dfSM : new table to save SimilarityScore """
    dfSM = pd.DataFrame( columns = ['PassengerId', 'Similarity', 'SimilarityScore', 'SimilarityScore_Name', 'SimilarityScore_Ticket', 'GroupName'] )
    dfSM[['PassengerId', 'SimilarityScore', 'SimilarityScore_Name', 'SimilarityScore_Ticket']] = dfSM[['PassengerId','SimilarityScore', 'SimilarityScore_Name', 'SimilarityScore_Ticket']].astype(int)
    listClues = ['Name', 'Ticket', 'Fare', 'FamilySize', 'Pclass', 'Cabin', 'Embarked'] 
    def GetElementsInCommon (xrow, yrow) : 
        retlist = [[], [], [], [], [], [], []]
        if xrow['PassengerId'] == yrow['PassengerId'] : return retlist
        ntlist = list(set(xrow['Name_']).intersection(yrow['Name_']))  
        ntlist.sort()
        retlist[0] = ntlist
        for i in range(1, len(listClues)) : 
            colnm = listClues[i]
            if xrow[colnm] == yrow[colnm] : retlist[i].append(xrow[colnm])
        # allow room for FamilySize value 
        if len(retlist[3]) == 0 & np.abs(xrow['FamilySize'] - yrow['FamilySize']) <= 2  : retlist[3].append(max(xrow['FamilySize'], yrow['FamilySize']))
        return retlist
    def GetSimilarityScore (xrow) : 
        sml = xrow['Similarity']
        retscore =  len(sml[0])*3 +  len(sml[1])*10 +  len(sml[2])*2 +  len(sml[3])*2 +  len(sml[4])*2 +  len(sml[5])*1  +  len(sml[6])*1   
        return retscore
    def GetUniqueGroupName(xrow)  :
        sml = xrow['Similarity']
        return '_'.join( '_'.join(str(e) for e in clist) for clist in sml)

    # this full cross check takes about 10 minutes 
    for i, row in df.iterrows() : 
        df['Similarity'] = df.apply(lambda x: GetElementsInCommon(x, row), axis=1)
        df['SimilarityScore'] = df.apply(lambda x : GetSimilarityScore(x), axis=1)
        df['SimilarityScore_Name'] = df.apply(lambda x : len(x['Similarity'][0]) * 1, axis=1)
        df['SimilarityScore_Ticket'] = df.apply(lambda x : len(x['Similarity'][1]) * 1, axis=1)
        df['GroupName'] = df.apply(lambda x : GetUniqueGroupName(x), axis=1)   
        # append to new dataframe only if SimilarityScore bigger than 8? where average Name similarity  reaches 1
        dfSM = dfSM.append(df.loc[df['SimilarityScore'] > 0, ['PassengerId', 'Similarity', 'SimilarityScore', 'SimilarityScore_Name', 'SimilarityScore_Ticket', 'GroupName']]) 

    # some tidying up
    df.drop(['Similarity', 'SimilarityScore', 'SimilarityScore_Name', 'SimilarityScore_Ticket', 'GroupName'], axis=1, inplace=True)
    dfSM = dfSM.drop_duplicates(['PassengerId','GroupName']).reset_index(drop=True)

    # left join to get FamilySize. Originally tried in Tableau but there seems to be a bug which omits some rows
    dfSM = pd.merge(dfSM, df[['PassengerId','FamilySize','Survived']], on='PassengerId', how='left')

    # export for Tableau
    dfSM.to_csv('titanic-data_similarity.csv')  

#### Detail.3. New columns for Ticket/Cabin naming convention analysis[¶](#Detail.3.-New-columns-for-Ticket/Cabin-naming-convention-analysis) {#Detail.3.-New-columns-for-Ticket/Cabin-naming-convention-analysis}

In [5]:

    """ Data-wrangling for the another analysis - Ticket, Cabin naming pattern analysis """
    # Ticket_ : new column to extract only numeric part from 'Ticket'  
    df['Ticket_'] = df['Ticket'].str.replace( r'\D.*\s+' ,'')
    df['Ticket_'] = df['Ticket_'].str.replace( r'LINE' , '0')

    # Cabin_ : new column to extract only numeric and representative part from 'Cabin' 
    df['Cabin_'] = df['Cabin'].str.replace( r'\D\s\D*' ,'')
    df['Cabin_'] = df['Cabin_'].str.replace( r'\s.*' ,'')
    df['Cabin_'] = df['Cabin_'].str.replace( r'\D' ,'')

    # export for Tabeau 
    df.to_csv('titanic-data_w.csv')
