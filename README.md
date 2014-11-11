[Dan Garrette]: http://cs.utexas.edu/~dhg
[Jason Baldridge]: http://www.jasonbaldridge.com
[Jason Mielens]: http://jason.mielens.com/


# Low-Resource POS-Tagging: 2014

**Author:** Dan Garrette (dhg@cs.utexas.edu)



This is a rewritten version of the code used in the papers:

> [Learning a Part-of-Speech Tagger from Two Hours of Annotation](http://www.cs.utexas.edu/users/dhg/papers/garrette_baldridge_naacl2013.pdf)  
> [Dan Garrette] and [Jason Baldridge]  
> In Proceedings of NAACL 2013  

> [Real-World Semi-Supervised Learning of POS-Taggers for Low-Resource Languages](http://www.cs.utexas.edu/users/dhg/papers/garrette_mielens_baldridge_acl2013.pdf)  
> [Dan Garrette], [Jason Mielens], and [Jason Baldridge]  
> In Proceedings of ACL 2013  

This archive contains code, written in Scala, for training and tagging using the approach described in the papers.
You do not need to have Scala installed in order to run the software since Scala runs on the Java Virtual Machine (JVM).
Thus, if you have Java installed, you should be able to run the system as described below.

## Setting things up


### Getting the code

Clone the project:

    $ git clone https://github.com/dhgarrette/low-resource-pos-tagging-2014.git
    
    
The rest of these instructions assume starting from the `low-resource-pos-tagging-2014` directory.


### Compile the project

    $ ./compile


## Running the system

    $ target/start OPTIONS

Training data.  If `rawFile` is given, `toksupFile` or `typesupFile` (or both) must be given.

* `--rawFile`: Location of the unannotated training data.
* `--toksupFile`: Location of the token-supervision training data: annotated sentences.
* `--typesupFile`: Location of the type-supervision training data: annotated words (line breaks don't matter; whitespace is ignored).

Model serialization file.  Required if training data is not given.

* `--modelFile`: Location of the saved model file, either for saving after training, or for retrieving if no training data is given. 

Data to run the tagger on.

* `--inputFile`: Location of an unannotated file to tag.
* `--outputFile`: Output location of the result of tagging the `inputFile`.
* `--evalFile`: Location of an annotated file to evaluate on.

* `--tdCutoff`: Tag dictionary cutoff.  Default: none.
* `--numRawTokens`: Number of raw tokens (complete sentences up to this number of total tokens).  Default: infinite.
* `--labelPropIterations`: Number of iterations for the label propagation procedure. Default `200`
* `--emIterations`: Number of iterations for the HMM EM training procedure. Default `50`
* `--memmIterations`: Number of iterations for the MEMM training procedure. Default `100`
* `--memmCutoff`: Cutoff for number of feature occurrences.  Default `100`

For example:

    $ ./run --rawFile data/raw.txt --toksupFile data/toksup.txt --typesupFile data/typesup.txt --modelFile data/model.ser
    $ ./run --modelFile data/model.ser --inputFile data/input.txt --outputFile data/output.txt
    $ ./run --modelFile data/model.ser --evalFile data/eval.txt



Note: You should set the `JAVA_OPTS` environment variable to increase the available memory:

    export JAVA_OPTS="-Xmx4g"


