# UsefulCommands

Settting CMS environment
====
    source /cvmfs/cms.cern.ch/cmsset_default.sh
    export SCRAM_ARCH=slc6_amd64_gcc530

CRAB Commands
====
    source /cvmfs/cms.cern.ch/crab3/crab.sh
    crab submit --dryrun crab_cfg.py
    crab proceed -d crab_project/crab_analysis

Screen commands
====
    screen -S sessionname #create session
    screen -R sessionname #go into session
    screen -list          #screen list
    Ctrl-a,d # detach

KNU Boson pT
====
    git clone git@github.com:d4space/TerraNova.git
    git clone git@github.com:d4space/WZRunII.git

KNU HWW
====
    git clone git@github.com:d4space/HWWSE.git

MIT W/Z
====
    git clone https://github.com/cmedlock/CSA14.git WZ/CSA14
    git clone https://github.com/jaylawhorn/MitEwk13TeV.git
    git clone https://github.com/jaylawhorn/BaconProd.git
    git clone https://github.com/jaylawhorn/BaconAna.git

MetTools
====
    git clone -b SangEunBranch git@github.com:cms-met/MetTools.git

MET Scan
====
    https://github.com/cms-met/MetScanning.git

XROOTD commands
====
protocols :\
cmsxrootd.fnal.gov : US\
xrootd-cms.infn.it : Europe and Asia\
cms-xrd-global.cern.ch : global\

    xrdcp root://[protocol]///store/mc/.../sample.root .
    xrdfs root://eoscms.cern.ch stat /store/data/.../sample.root
    
batch job submission on KNU T2
====
    qsub -q cms -l walltime=500:00:00,cput=500:00:00 job_desc_$isec.sh -N WpMu_dyn13_$isec
    create-batch --jobName testjob1 --fileList fileList.txt --maxFiles 1 --cfg USER_CONF.py

Storage Element access on KNU T2
====
    gfal-ls -Hl 'srm://cluster142.knu.ac.kr:8443/srm/managerv2?SFN=/pnfs/knu.ac.kr/data/cms/store/user/spak/'
    gfal-copy 'srm://cluster142.knu.ac.kr:8443/srm/managerv2?SFN=/pnfs/knu.ac.kr/data/cms/store/user/spak/ForUnfBiasNtuple/WJetsToLNu_S7/wAcceptance_62_2_Xhi.root' file:///d1/scratch/sangilpark/Wpt/CMSSW_5_2_6/src/KoSMP/WAnalyzer/AodToNtuple/S8/MuNeu/WJetsToLNu_S7/ntuples/
    gfal-copy file:///`pwd`/UsefulCommand 'srm://cluster142.knu.ac.kr:8443/srm/managerv2?SFN=/pnfs/knu.ac.kr/data/cms/store/user/spak/'

dcap protocol
====
    'dcap://cluster142.knu.ac.kr//pnfs/knu.ac.kr/data/cms/store/mc/RunIISpring15DR74/WJetsToLNu_TuneCUETP8M1_13TeV-amcatnloFXFX-pythia8/MINIAODSIM/Asympt50ns_MCRUN2_74_V9A-v1/50000/166EBB38-39FE-E411-B803-0025905746B2.root'
    dcap://cluster142.knu.ac.kr//pnfs/knu.ac.kr/data/cms/store/user/spak/LatinoProduction/WGToLNuG_TuneCUETP8M1_13TeV-madgraphMLM-pythia8/crab_Wg_MADGRAPHMLM/160425_014431/0000/stepB_27.root
    export LD_PRELOAD=/usr/lib64/libpdcap.so
    ls dcap://cluster142.knu.ac.kr//pnfs/knu.ac.kr/data/cms/~~
    export X509_USER_PROXY=~/proxy.cert

UberFTP
====
    voms-proxy-init --voms cms --valid 168:0
    uberftp cluster142.knu.ac.kr "ls /pnfs/knu.ac.kr/data/cms/store/user/spak"
    get -r directory # copy files from SE to local
    put -r directory # copy files from local to SE
    Command : help, put, get, ldir, lcd, etc..

FDT Usage 
====
Client side.

    java -jar /u/user/sangilpark/fdt/fdt.jar -S&  # same as ./fdtstandby.sh
    java -Xms32M -Xmx100M -jar [fdt location] -c [Destination server] -d [Destination directory] -P 12 -r [Directory to send]
    java -Xms32M -Xmx100M -jar /afs/cern.ch/user/s/spak/fdt/fdt.jar -c cms.knu.ac.kr -d /d1/scratch/sangilpark/Latino_CernBox/80Xv2/HWW12fb_repro -P 12 -r ./05Jul2016_Run2016B_PromptReco_repro

Destination side.

    java -jar /u/user/sangilpark/fdt/fdt.jar -S& # same as ./fdtstandby.sh

EDM commands
====
    edmFileUtil -d  /store/data/Run2015D/SingleMuon/MINIAOD/PromptReco-v4/000/258/159/00000/6CA1C627-246C-E511-8A6A-02163E014147.root
    mkedanlzr DemoAnalyzer
    edmDumpEventContent /afs/cern.ch/cms/Tutorials/TWIKI_DATA/TTJets_8TeV_53X.root

PickEvent.

    edmPickEvents.py "/SingleMuon/Run2015B-PromptReco-v1/RECO" 251252:127:14760672 --runInteractive
    edmCopyPickMerge inputFiles=root://cms-xrd-global.cern.ch//store/data/Run2015B/SingleMuon/RECO/PromptReco-v1/000/251/493/00000/0C35D6F8-D028-E511-9651-02163E012283.root outputFile=/u/user/khakim/forSangil/0C35D6F8-D028-E511-9651-02163E012283.root maxEvents=5000

UI SE mount location
====
    /pnfs/knu.ac.kr/data/cms/store/user/(UserID)

BrilCalc Usage
====
    export PATH=$HOME/.local/bin:/afs/cern.ch/cms/lumi/brilconda-1.0.3/bin:$PATH
    brilcalc lumi --begin 276315 --end 276811 -u /fb -b "STABLE BEAMS" --normtag /afs/cern.ch/user/l/lumipro/public/normtag_file/normtag_DATACERT.json -i Cert_271036-277933_13TeV_PromptReco_Collisions16_JSON.txt

Vim Spell check
====
    :setlocal spell spelllang=en_us

WebFTS Usage
====
Grid SE endpoint example.

    root://eoscms.cern.ch//store/group/phys_higgs/cmshww/amassiro/
    srm://cluster142.knu.ac.kr:8443/srm/managerv2?SFN=/pnfs/knu.ac.kr/data/cms/store/user/spak
    srm://cms-se.sdfarm.kr:8443/srm/v2/server?SFN=/xrootd/store/user/spak
    srm://maite.iihe.ac.be:8443/pnfs/iihe/cms/store/user/xjanssen/HWW2015/RunII/2016/Apr2017/MC/LatinoTrees/
    srm://dcache-se-cms.desy.de/pnfs/desy.de/cms/tier2/store/user/sbein/NtupleHub/ProductionRun2v3
    
DASGO
====
    dasgoclient -help
    Usage: dasgoclient [options]
      -daskeys
            Show supported DAS keys
      -examples
            Show examples of supported DAS queries
      -json
            Return results in JSON data-format
      -profileMode string
            enable profiling mode, one of [cpu, mem, block]
      -query string
            DAS query to run
      -sep string
            Separator to use (default " ")
      -unique
            Sort results and return unique list
      -verbose int
            Verbose level, support 0,1,2
    Examples:
            # get results
            dasgoclient -query="dataset=/ZMM*/*/*"
            # get results in JSON data-format
            dasgoclient -query="dataset=/ZMM*/*/*" -json
            # get results from specific CMS data-service, e.g. phedex
            dasgoclient -query="file dataset=/ZMM/Summer11-DESIGN42_V11_428_SLHC1-v1/GEN-SIM system=phedex" -json
