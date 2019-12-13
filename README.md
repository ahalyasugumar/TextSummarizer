# TextSummarizer
Summarization of Text

Source Repository:  

1. https://github.com/dmmiller612/bert-extractive-summarizer 

2. https://github.com/atulkum/pointer_summarizer    

  

Preprocessed Dataset for training downloaded from:  

 https://github.com/abisee/cnn-dailymail  

Note --- We have not included the pre-processed datasets within the Google Drive as it is 4GB in size and owing to the huge size, it was difficult to upload it to the drive. Before running, please download the pre-processed dataset and place it in the data directory directly with naming convention as train_* 

Prerequisites: 

For the Extractive Summarizer: 

numpy==1.16.3 

torch==1.0.1 

spacy==2.1.3 

transformers==2.2.0 

Cython==0.29.10 

tqdm==4.32.2 

neuralcoref==4.0 

argparse 

scikit-learn 

bert-extractive-summarizer==0.2.2 

For the Abstractive Summarizer: 

Setup pyrouge to get the rouge score 

Download corpus from extractive summarizer and extract in specified directory 

 

Files Created: 

 1. run.ipnb – A run file is created that runs the bert extractive summary model and feeds the summarized output to the pointer generator abstractive summary model. Further,  

Files Modified:  

For Extractive Summarizer:  

Added code to extract the output posted to the RESTful API and write it to a text file so that it can be passed to the Abstractive Summarizer for processing. Further, since the input to the Abstractive Summarizer needs to be processed to be in the bin format, code to convert the text output from the BERT Extractive Summarizer was written using the make_file function. 

For Abstractive Summarizer: 

Model.py & train.py: Modified the architecture by adding an additional LSTM layers and experimented with non-Bidirectional LSTMs and Linear Layers. 

 

Config.py: Experimented with hyper parameters such as hidden_dim, max_iterations, learning rate etc. and analyzed the performance. 

 

Commands: 

[1] To execute the Summarizer: 

For Extractive Summarizer,  

make docker-service-build 

make docker-service-run 

For the Abstractive Summarizer, 

 

!python run_summarization.py --mode=decode --  data_path='/content/drive/My Drive/NLP/Project/prof/pointer-generator-master/data/finished_files/chunked/test_001*' --vocab_path='/content/drive/My Drive/NLP/Project/prof/pointer-generator-master/data/finished_files/vocab' --log_root='/content/drive/My Drive/NLP/Project/prof/pointer-generator-master' --exp_name=pretrained_model_tf1.2.1 --max_enc_steps=400 --max_dec_steps=120 --coverage=1 --single_pass=1 

 

[2] To compute the ROGUE Score: Code included in the implementation of Abstractive Summariser 

 

#Sample Output 

Passage: 

( cnn ) a man charged with planning the deadly 2008 mumbai terror attacks in india has been released on bail in pakistan after years of detention , prompting sharp criticism from india . zaki-ur-rehman lakhvi , a top leader of the terrorist group lashkar-e-taiba , was released early friday from a jail in the pakistani city of rawalpindi , according to yahya mujahid , spokesman for jamaat-ud-dawa , a group with which lakhvi is affiliated . lakhvi was charged in pakistan in 2009 , accused of masterminding the november 2008 terror attacks that left more than 160 people dead in mumbai , india 's most populous city . lakhvi still faces trial in the case . but an anti-terrorism court granted lakhvi bail last year , a decision the pakistani government said it would challenge . that challenge lasted until thursday , when the lahore high court ordered his release , cnn affiliate and pakistani outlet geo news reported . lakhvi posted bail totaling 2 million pakistani rupees ( more than $ 19,000 ) , according to geo news . india , pakistan 's neighbor and rival , condemned lakhvi 's bail release on friday . the country contacted pakistan 's foreign secretary to underline `` that this has reinforced the perception that pakistan has a dual policy on dealing with terrorists , and those who have carried out attacks or are posing a threat to india are being dealt with differently , '' said syed akbaruddin , a spokesman for india 's ministry of external affairs . the accusation that pakistan might treat india differently highlights long-running tensions between the two nuclear-armed neighbors , which have fought three wars against each other since their partition at the end of british colonial rule . pakistan 's foreign office responded friday by saying , `` it would not be proper to cast aspersions on pakistan 's commitment to countering terrorism at a time when pakistan has entered a critical stage of defeating the menace of terrorism . '' the foreign office also blamed what it said was india 's delay in cooperating in the case , saying it `` weakened the prosecution . '' in the mumbai attacks , heavily armed men stormed landmark buildings around mumbai , including luxury hotels , the city 's historic victoria terminus train station and a jewish cultural center . india executed the last surviving gunman from the attacks in 2012 . other suspects were all killed during the series of attacks , which went on for three days . more about the mumbai attacks . cnn 's harmeet singh contributed to this report . 

Output of Extractive Summarizer: 

Output of Abstractive Summarizer: 

zaki-ur-rehman lakhvi , a top leader of the terrorist group lashkar-e-taiba , was released early friday from a jail in the pakistani city of rawalpindi . 

lakhvi was charged in pakistan in 2009 , accused of masterminding the november 2008 terror attacks that left more than 160 people dead in mumbai , india 's most populous city . 

ROGUE Score for the Model: 

 

Baseline 

Rouge 1 

Rouge 2 

F - Score 

Precision 

Recall 

F - Score 

Precision 

Recall 

0.304714 

0.3299 

0.2831 

0.109784 

0.1372 

0.0915 


