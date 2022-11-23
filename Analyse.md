
Petite analyse des sentiments (négatif, positif, neutre) des tweets de différents média d'informations à l'aide d'une IA.

@BFMTV

@afpfr

@brutofficiel

@CerfiaFR

<br><br>
Je lis de temps en temps dans les réponses de tweet de média des phrases du style "Notre monde va de plus en plus mal".
Bon pour confirmer ces propos, il faudrait plus qu'un thread, mais là, on va s'intéresser aux news envoyées au public.

<br><br>
Alors quand on regarde les médias généralistes, on a souvent l'impression de voir plus de news négatives que de news positives.
Et j'ai voulu vérifier cette impression avec une Intelligence artificielle qui est allée détecter le sentiment des tweets et donc de l'information.


<br><br>
<br><br>
IA:
Pour cette analyse, j'ai utilisé un modèle de deep learning pré-entraîné, appelé BERT crée par Google qui permet de résoudre des problèmes de NLP (Natural Language processing)
NLP est un sous-domaine du Machine learning qui a pour objectif de donner à des programmes informatiques la capacité de comprendre et de traiter le langage humain.

<br><br>
Voici des petits exemple des résultats de l'IA sur des tweets, ce n'est pas parfait, il peut y avoir des erreurs, mais dans l'ensemble, c'est exploitable.

exemples aux hasard :
<br><br>
![alt text](https://github.com/Kyytox/feelings-twitter-ia/blob/master/Graph/tweets_negatifs.png)
![alt text](https://github.com/Kyytox/feelings-twitter-ia/blob/master/Graph/tweets_neutres.png)
![alt text](https://github.com/Kyytox/feelings-twitter-ia/blob/master/Graph/tweets_positifs.png)

<br><br>
Data:
j'ai pu récupérer un certain nombre de tweets des différents média, en tout, j'ai 14 000 tweets (l'API Twitter limite la récupérations, aux 3200 derniers d'un compte)
Dans ces tweets, il n'y a pas de retweets ni les réponses aux tweets
<br><br>


Analyse:
Voici une représentation du :
Pourcentage de tweets négatifs, neutres, positifs pour chaque média
<br><br>
![alt text](https://github.com/Kyytox/feelings-twitter-ia/blob/master/Graph/Pie_graph_pourcent_sent_of_tweets.png)

<br><br>
Voici une représentation du :
Nombre de tweets négatifs, neutres, positifs pour chaque média
<br><br>
![alt text](https://github.com/Kyytox/feelings-twitter-ia/blob/master/Graph/Bar_graph_number_tweets_by_sent.png)

<br><br>
On peut voir une domination des news négatives (60 % ou plus) par rapport aux neutre et positifs sauf pour @brutofficiel qui arrive a 50% Mais si on prend seulement les positifs ou neutre les tweets négatifs l'emportent largement

<br><br>
Ensuite, j'ai voulu regarder les mots les plus utilisé dans les tweets pour chaque média. 
Voilà ce que ça donne
<br><br>
![alt text](https://github.com/Kyytox/feelings-twitter-ia/blob/master/Graph/Wordcloud_graph_frequent_words.png)

<br><br>
Pour finir, j'ai récupéré 1148 tweets de chaque sentiment, pour regarder leur nombre d'interactions.
![alt text](https://github.com/Kyytox/feelings-twitter-ia/blob/master/Graph/Circle_graph_nb_interactions.png)

Dans ce dernier graph on voit que les tweets détecter comme négatifs ont presque 2x plus d'interactions que les autres pris séparément.

<br><br>
Bilan: 
Si on prend séparément les sentiments, il y a une nette domination des news négatives. 
Si on considère que les tweets neutre et positifs appartiennent à sentiments similaires alors il y a toujours, mais une plus petite domination des négatifs sauf pour @brutofficiel

<br><br>
Mais là où c'est intéressant, c'est le nombre d'interactions, qui est 2x plus grand pour les négatifs que pour le reste. 
Donc si on part du principe qu'un média est là pour fournir de l'info, mais aussi attirer plus de gens (pour les finances et la crédibilité)

<br><br>
Ils ont tout intérêt à tweeter des news négatives puisque qu'il y aura bien + d'interactions sur ces derniers.

<br><br>
Donc on blâme qui, les médias qui balance + de news négatives que de positives ou neutre ou l'humain qui a tendance à toujours + réagir quand il s'agit d'une bad news, sachant que l'interactions fait perdurer un média ?

<br><br>
Voilà. 

<br><br>
Merci d'avoir lu 

<br><br>
Je compte continuer à récupérer des tweets pour pourquoi pas, refaire une analyse dans 6/8 ou 10 mois avec bien plus de données.
