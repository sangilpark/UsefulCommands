# UsefulCommands
#### Settting CMS environment ####
====
  source /cvmfs/cms.cern.ch/cmsset_default.sh
  source /cvmfs/cms.cern.ch/crab3/crab.sh
  setenv SCRAM_ARCH slc6_amd64_gcc493
  source /d2/scratch/khakim/root_SL5/root/bin/thisroot.sh

#### Screen command ####
====
screen -S sessionname #create session
screen -R sessionname #go into session
screen -list          #screen list
Ctrl-a,d # detach

#### KNU Boson pT ####
git clone git@github.com:d4space/TerraNova.git
git clone git@github.com:d4space/WZRunII.git

#### KNU Higgs WW ####
git clone git@github.com:d4space/HWWSE.git

#### MIT W/Z ####
git clone https://github.com/cmedlock/CSA14.git WZ/CSA14
git clone https://github.com/jaylawhorn/MitEwk13TeV.git
git clone https://github.com/jaylawhorn/BaconProd.git
git clone https://github.com/jaylawhorn/BaconAna.git

#### MET Scan ####
https://github.com/cms-met/MetScanning.git

#### Sangil Useful Reference code, etc ####
git clone git@github.com:sangilpark/Miscellaneous.git

#### XROOTD commands ####
xrdcp root://xrootd.unl.edu////store/mc/Spring14miniaod/WplusToMuNu_CT10_13TeV-powheg-pythia8/MINIAODSIM/PU20bx25_POSTLS170_V5-v1/00000/AED9D7C6-4409-E411-AC3E-A5BCA2C588C1.root .
xrdcp root://xrootd-cms.infn.it//store/data/Run2015A/SingleMu/AOD/PromptReco-v1/000/246/865/00000/F042A080-140B-E511-8B1C-02163E0134B0.root .
root -l root://xrootd-cms.infn.it//store/group/phys_higgs/cmshww/amassiro/RunII/2016/Jun07/MC/v2/LatinoTrees/latino_ZZ__part0.root
root://eosuser.cern.ch//eos/user/j/jlauwers/HWW2015/21Jun2016_Run2016B_PromptReco/l2loose__hadd__EpTCorr__l2tight/latino_Run2016B_PromptReco_DoubleEG.root
xrdfs root://eoscms.cern.ch stat /store/data/Run2015D/SingleMuon/MINIAOD/PromptReco-v4/000/258/159/00000/6CA1C627-246C-E511-8A6A-02163E014147.root

#### batch job submit ####
qsub -q cms -l walltime=500:00:00,cput=500:00:00 job_desc_$isec.sh -N WpMu_dyn13_$isec
create-batch --jobName testjob1 --fileList fileList.txt --maxFiles 1 --cfg USER_CONF.py

#### Storage Element ####
gfal-ls -Hl 'srm://cluster142.knu.ac.kr:8443/srm/managerv2?SFN=/pnfs/knu.ac.kr/data/cms/store/user/spak/'
gfal-copy 'srm://cluster142.knu.ac.kr:8443/srm/managerv2?SFN=/pnfs/knu.ac.kr/data/cms/store/user/spak/ForUnfBiasNtuple/WJetsToLNu_S7/wAcceptance_62_2_Xhi.root' file:///d1/scratch/sangilpark/Wpt/CMSSW_5_2_6/src/KoSMP/WAnalyzer/AodToNtuple/S8/MuNeu/WJetsToLNu_S7/ntuples/
gfal-copy file:///`pwd`/UsefulCommand 'srm://cluster142.knu.ac.kr:8443/srm/managerv2?SFN=/pnfs/knu.ac.kr/data/cms/store/user/spak/'

#### dcap protocol ####
'dcap://cluster142.knu.ac.kr//pnfs/knu.ac.kr/data/cms/store/mc/RunIISpring15DR74/WJetsToLNu_TuneCUETP8M1_13TeV-amcatnloFXFX-pythia8/MINIAODSIM/Asympt50ns_MCRUN2_74_V9A-v1/50000/166EBB38-39FE-E411-B803-0025905746B2.root'
dcap://cluster142.knu.ac.kr//pnfs/knu.ac.kr/data/cms/store/user/spak/LatinoProduction/WGToLNuG_TuneCUETP8M1_13TeV-madgraphMLM-pythia8/crab_Wg_MADGRAPHMLM/160425_014431/0000/stepB_27.root
export LD_PRELOAD=/usr/lib64/libpdcap.so
ls dcap://cluster142.knu.ac.kr//pnfs/knu.ac.kr/data/cms/~~
export X509_USER_PROXY=~/proxy.cert

#### UberFTP ####
voms-proxy-init --voms cms
uberftp cluster142.knu.ac.kr "ls /pnfs/knu.ac.kr/data/cms/store/user/spak"
get -r directory # copy files from SE to local
put -r directory # copy files from local to SE
Command : help, put, get, ldir, lcd, etc..

#### CERNBOX ####
/afs/cern.ch/project/eos/installation/0.3.84-aquamarine.user/bin/eos.select
/afs/cern.ch/project/eos/installation/0.3.84-aquamarine.user/bin/eos.select -b fuse mount ~/eos_cernbox #cernbox mount
ls /eos/user/j/jlauwers/HWW2015/

#### FDT Usage (Client side) ####
java -jar /u/user/sangilpark/fdt/fdt.jar -S&  # same as ./fdtstandby.sh
java -Xms32M -Xmx100M -jar [fdt location] -c [Destination server] -d [Destination directory] -P 12 -r [Directory to send]
java -Xms32M -Xmx100M -jar /home/spak/fdt.jar -c cms02.knu.ac.kr -d /u/user/sangilpark/tmp -P 12 -r /Storage1/CernBox_Jasper_76X
#### FDT Usage (Server side) ####
java -jar /u/user/sangilpark/fdt/fdt.jar -S& # same as ./fdtstandby.sh

#### EDM commands ####
edmFileUtil -d  /store/data/Run2015D/SingleMuon/MINIAOD/PromptReco-v4/000/258/159/00000/6CA1C627-246C-E511-8A6A-02163E014147.root
mkedanlzr DemoAnalyzer
edmDumpEventContent /afs/cern.ch/cms/Tutorials/TWIKI_DATA/TTJets_8TeV_53X.root
#### PickEvent ####
edmPickEvents.py "/SingleMuon/Run2015B-PromptReco-v1/RECO" 251252:127:14760672 --runInteractive
edmCopyPickMerge inputFiles=root://cms-xrd-global.cern.ch//store/data/Run2015B/SingleMuon/RECO/PromptReco-v1/000/251/493/00000/0C35D6F8-D028-E511-9651-02163E012283.root outputFile=/u/user/khakim/forSangil/0C35D6F8-D028-E511-9651-02163E012283.root maxEvents=5000

#### UI SE mount location ####
/pnfs/knu.ac.kr/data/cms/store/user/(UserID)
