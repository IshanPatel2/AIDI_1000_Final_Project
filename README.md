# AIDI_1000_Final_Project

Research Paper Link: https://arxiv.org/pdf/1904.08067v5.pdf
Research Paper Github Link: https://github.com/kk7nc/Text_Classification/tree/master
Dataset Link: https://github.com/kk7nc/Text_Classification/blob/master/Data/Download_Glove.py

# Project Goal:
Text feature extraction and pre-processing for classification algorithms are very significant. In this section, we start to talk about text cleaning since most of documents contain a lot of noise. In this part, we discuss two primary methods of text feature extractions- word embedding and weighted word.
1)Text Cleaning and Pre-processing
2)Tokenization
3)Stop words
4)Capitalization

# Steps to run our code:
1) Step:1 Data Loading
   from __future__ import print_function

import os, sys, tarfile
import numpy as np
import zipfile

if sys.version_info >= (3, 0, 0):
    import urllib.request as urllib  # ugly but works
else:
    import urllib

print(sys.version_info)

# image shape


# path to the directory with the data
DATA_DIR = '.\Glove'

# url of the binary data



# path to the binary train file with image data


def download_and_extract(data='Wikipedia'):
    """
    Download and extract the GloVe
    :return: None
    """

    if data=='Wikipedia':
        DATA_URL = 'http://nlp.stanford.edu/data/glove.6B.zip'
    elif data=='Common_Crawl_840B':
        DATA_URL = 'http://nlp.stanford.edu/data/wordvecs/glove.840B.300d.zip'
    elif data=='Common_Crawl_42B':
        DATA_URL = 'http://nlp.stanford.edu/data/wordvecs/glove.42B.300d.zip'
    elif data=='Twitter':
        DATA_URL = 'http://nlp.stanford.edu/data/wordvecs/glove.twitter.27B.zip'
    else:
        print("prameter should be Twitter, Common_Crawl_42B, Common_Crawl_840B, or Wikipedia")
        exit(0)


    dest_directory = DATA_DIR
    if not os.path.exists(dest_directory):
        os.makedirs(dest_directory)
    filename = DATA_URL.split('/')[-1]
    filepath = os.path.join(dest_directory, filename)
    print(filepath)

    path = os.path.abspath(dest_directory)
    if not os.path.exists(filepath):
        def _progress(count, block_size, total_size):
            sys.stdout.write('\rDownloading %s %.2f%%' % (filename,
                                                          float(count * block_size) / float(total_size) * 100.0))
            sys.stdout.flush()

        filepath, _ = urllib.urlretrieve(DATA_URL, filepath)#, reporthook=_progress)


        zip_ref = zipfile.ZipFile(filepath, 'r')
        zip_ref.extractall(DATA_DIR)
        zip_ref.close()
    return path


from __future__ import print_function

import os, sys, tarfile
import numpy as np

if sys.version_info >= (3, 0, 0):
    import urllib.request as urllib
else:
    import urllib

print(sys.version_info)

# image shape


# path to the directory with the data
DATA_DIR = '.\data_WOS'

# url of the binary data
DATA_URL = 'http://kowsari.net/WebOfScience.tar.gz'


# path to the binary train file with image data


def download_and_extract():
    """
    Download and extract the WOS datasets
    :return: None
    """
    dest_directory = DATA_DIR
    if not os.path.exists(dest_directory):
        os.makedirs(dest_directory)
    filename = DATA_URL.split('/')[-1]
    filepath = os.path.join(dest_directory, filename)


    path = os.path.abspath(dest_directory)
    if not os.path.exists(filepath):
        def _progress(count, block_size, total_size):
            sys.stdout.write('\rDownloading %s %.2f%%' % (filename,
                                                          float(count * block_size) / float(total_size) * 100.0))
            sys.stdout.flush()

        filepath, _ = urllib.urlretrieve(DATA_URL, filepath, reporthook=_progress)

        print('Downloaded', filename)

        tarfile.open(filepath, 'r').extractall(dest_directory)
    return path


