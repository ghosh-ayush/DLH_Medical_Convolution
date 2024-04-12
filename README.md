# Medical_Convolution_DLH
> Procedures on running the set of Jupyter Notebooks and models

1. Gain access to the MIMIC-III from PhysioNet.

2. Use the MIMIC-Extract Pipeline provided in https://github.com/MLforHealth/MIMIC_Extract to extract the data.

3. Start by moving all_hourly_data.h5 in the output file of MIMIC-Extract Pipeline to the data folder, and running "01-Extract-Timeseries-Features.ipynb" to extract first 24 hours timeseries features from MIMIC-Extract raw data.

4. Copy the ADMISSIONS.csv, NOTEEVENTS.csv, ICUSTAYS.csv files into data folder, and run "02-Select-SubClinicalNotes.ipynb" to select and save clinical notes.

5. Run "03-Prprocess-Clinical-Notes.ipnyb" to prepocessing clinical notes from step 4.

6. Use Med7, which is a transferable clinical natural language processing model for electronic health records, to extract medical entities by running "04-Apply-med7-on-Clinical-Notes.ipynb".

7. Download the Pre-trained Word2Vec & FastText embeddings from https://github.com/kexinhuang12345/clinicalBERT and move the embeddings into the "embedding" folder. 

8. Run "05-Represent-Entities-With-Different-Embeddings.ipynb" to convert medical entities extracted by Med7 into word representations using several approaches including Word2Vec, FastText, and combining both of them.

9. Run "06-Create-Timeseries-Data.ipynb" to prepare the timeseries data to fed through GRU model.

10. Train the timeseries baseline model (GRU) and evaluate its performance on predicting the 4 different clinical tasks (mortality (in-hospital & in-ICU) and Length-of-stay (>3 & >7) at ICU) by running "07-Timeseries-Baseline.ipynb". 

11. Run "08-Multimodal-Baseline.ipynb" to train multimodal baseline that uses the word representations obtained in step 8 and evaluate its perfromance on predicting the 4 different clinical tasks.

12. "09-Proposed-Model.ipynb" includes the proposed model from the original paper, which uses 1D convolutional layers as a feature extractor on medical entities obtained from step 8. Run "09-Proposed-Model.ipynb" to train the model and evaluates its performance on the 4 tasks.

13. Run "load_print_results.ipynb" to organize the result obtained from the previous steps and produce comparisons among different models as well as comparing the results the to those from the original paper. 
