# Search for PbPb->ttbar with 2018 data

## Documentation
 
See details in the analysis twiki page https://twiki.cern.ch/twiki/bin/view/CMS/PbPbTTBar2018

## Running the analysis

The selection/plot filling is implemented in bin/runTTto2Lselection.cc.
It uses directly as inputs the HiForest contents.
The executable can be compiled with `scram b`.
To run on a single file for testing one  can give the command
```
runTTto2Lselection --in /eos/cms/store/group/phys_top/PbPbTTbar_2018/SkimElectrons_PromptRecov1/Chunk_1_ext0.root --out test.root
```

To loop over all the available forest trees better to use condor and then merge the outputs.
Jobs finalize in approx. 40min if queues are empty.
```
dir=/eos/cms/store/cmst3/group/top/PbPb
a=(`ls ${dir}`)
out=`pwd`/plots/Chunks
for tag in ${a[@]}; do    
    extraOpts="true true"
    if [[ $tag == *"Skim"* ]]; then
       extraOpts=""
    fi
    python scripts/launchAnalysis.py ${dir}/${tag} $out $tag $extraOpts;
done   
```

Merge the outputs (hadds all the chunks according to the tag defined)
```
python scripts/mergeOutputs.py plots
```

Plot the results
```
FIXME
```