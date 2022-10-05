# lecture notes about things related to biotechnology

## motivation

- as biotech is a booming industry, lots of investment capital will be attracted into this area
- risks
  - biotech dotcom-like bubbles are inavitable if investors are not specialists in this field
  - lets say someone delivers you a nice presentation with lots of analogical/intuitive material
    - how do you know its true?
    - what's probability of whole presentation beign giberrish?
      - whats probability of 50% of it being bs? 
      - how about 20%? 
      - can you tell the difference?
      - is there some verification harnesses akin to unit-tests but for biotech?


## basics of verification

- how do you examine/verify/reproduce results of a bio/nanotech research?
  - molecular mechanics at nano scales are currently impossible to film (in motion)
    - only static images are possible
      - and even they may be destructive for the observed structures
  - when people are talking about constructing molecules from fist-principles
    - you can only reliably verify static structures, observable in electronic microscope you own
  
  - random ideas
    - electonic microscope
      - so you can verify by looking at static images
    - well-known chain of chemical reactions
      - that produces macro result only if synthesised material is legit
      - you have to learn to "write" and "run" chemical "unit-tests" at minimum


## microscopy basics

- microscope main parts
  - eyepiece lens
    - usually 10x or 15x power
  - revolving nosepiece or turret
    - holds two or more objective lenses and can be rotated to easily change power (magnification)
    - objective lenses
      - usually you will find 3 or 4 objective lenses on a microscope
        - they almost always consist of 4x, 10x, 40x and 100x powers
          - 100x may not give a sharp image, so some ppl recommend to use 60x instead
        - there may be an oil-immersion lens, you need to use a drop of oil to look through it
          - most likely an oil have to be on top of a glass covering specimen?
      - when coupled with a 10x (most common) eyepiece lens
        - we get total magnification of 40x (4x times 10x), 100x, 400x, and 1000x
        - to have good resolution at 1000x, you will need a relatively sophisticated microscope with an Abbe condenser
  - rack stop
    - an adjustment that determines how close the objective lens can get to the slide
  - stage
    - stage clips
  - illuminator
    - a steady electric light source (used in place of a mirror, like it used to be in ancient models)
    - condenser lens
      - focuses light onto the specimen
      - most useful at the highest powers (400x and above)
      - microscopes with a stage condenser lens render a sharper image than those with no lens (at 400x)
      - allows to control resolution, light, depth of field
      - stage mounted lens
        - if your microscope has a maximum power of 400x
        - you will get the maximum benefit by using a condenser lenses rated at 0.65 NA or greater
        - 0.65 NA condenser lenses may be mounted in the stage and work quite well
        - stage mounted lens is that there is one less focusing item to deal with
      - focusable condenser lens
        - if you go to 1000x then you should have a focusable condenser lens with an N.A. of 1.25 or greater
        - most 1000x microscopes use 1.25 Abbe condenser lens systems
          - the Abbe condenser lens can be moved up and down
          - it is set very close to the slide at 1000x and moved further away at the lower powers
      - diaphragm or iris
        - many microscopes have a rotating disk under the stage
        - this diaphragm has different sized holes
          - is used to vary the intensity and size of the cone of light that is projected upward into the slide
      - slide
        - a piece of glass where specimen is located

- good general purpose microscope
  - price range: 300-1k
  - number of oculars
    - monocular: cheaper, bit lighter, more portable
    - binocular: a bit dimmer, but easier on eyes
  - objective lenses
    - should conform to one of the following standards
      - din 160mm (most popular)
      - din 170mm
    - bright-field acromatic objectives (basic ones)
    - should be of the same series
      - in order to refocus less when switching between different lenses/magnifications
  - condenser
  - coarse and fine focus knobs
  - light intensity regulator
  - exchangeable eyepiece lenses
    - here you can connect a digital camera
  - okay magnification 600x, no reason to buy anything higher 1000x (marketing trick)
  
- advanced microscope
  - price range: 1k-5k
  - phase contrast microscopy/lenses
  - photo tube (trinocular)
    - on binocular you can use one eyepiece to put relatively simple camera in
  - halogen light source for advanced photography
  - objective lenses
    - 'infinity optics' 
    - phase contrast lenses option

- things i need to look up later
  - All quality microscopes have achromatic, parcentered, parfocal lenses ... whaaat?
  - numerical aperture (NA)
    - NA of an optical system is a dimensionless number that characterizes the range of angles over which 
      the system can accept or emit light. 



## protein design

- a quest for a lowest energy state of the structure
    - if we want to design a protein
    - we are looking to produce a certain desired structure
        - for example: 
        - to neutralize toxins or viruses, by attaching to them
        - to mimick certain catalysts and trigger a cascade of chemical reactions we need
    - we must find a sequence of aminoacids that produces a protein for which
        - that desired structure has a lowest energy state
        - david uses analogy of a 'backbone'
- folded state of a protein is likely an energy-minimal configuration, a "native structure"
- stats
    - # of naturally occuring proteins 10e15
    - number of possible combination for 100 length sequence is 1.3e130
      - essentially, combinatorial explosion
- relatively simpler approach is "neanderthal protein design"
  - adding changes to already existing proteins
  - in a hope that result will resemble what we need

- examples of molecular designs from first principles
  - molecular gates/filters
    - potassium channels (калиевый канал)
    - nanopores of different sizes (nanopore is a pore of nanometer size)
    - large transmembrane beta barrels (TMB)
      -  function as transporters for ions and small molecules that cannot diffuse across a cellular membrane
  

## minimal self-replicators
      
- axenic culture
  - state of a culture in which only a single species, variety, or strain of organism is present
    - and entirely free of all other contaminating organisms
  - typically prepared by subculture of an existing mixed culture

- minimal cell 
  - natural: LUCAs
    - last universal common ancestors
    - there are several of them
      - because of horizontal gene transfer happenning between coexisting replicators
  - synthetic (chassis)
    - 2016 JCVI-Syn3.0, derived from bacterial cell
      - 531,490 bp
        - it has a smaller genome than that of any known organism that can be grown in axenic culture
      - there are only 438 protein-coding genes and 35 RNA-coding genes
      - how hard to prepare such culture?

- see <repo>/notes/comuting.md for info about more generic models


## synthetic biology

- areas of research
  - bioengineering
    - altering dna, making new proteins and protein systems
  - xenobiology
    - describes novel biological systems and biochemistries that differ from the canonical DNA–RNA-20 amino acid system 
    - for example
      - instead of DNA or RNA, XB explores nucleic acid analogues, termed xeno nucleic acid (XNA) as information carriers.
      - it also focuses on an expanded genetic code and the incorporation of non-proteinogenic amino acids into proteins
  - synthetic genomics
    - main goal: artificially create cell genome
    - whole dna is synthesised


## xenobots

- definition
  - synthetic lifeforms that are designed by computers to perform some desired function and built by combining together different biological tissues

- organizms built up to date (2022)
  - less than 1 millimeter (0.039 inches) wide
  - some composed of just two things: skin cells and heart muscle cells
    - cells derived from stem cells
    - stem cells harvested from early (blastula stage) frog embryos
  - skin cells provide rigid support and the heart cells act as small motors, contracting and expanding in volume to propel the xenobot forward
  - can grow patches of cilia and use them as small oars(вёсла) for swimming


## environment

- clostridium autoethanogenum [^1]
  - кишечная бактерия, способна преобразовывать угарный газ в этиловый спирт

- ideonella sakaiensis 
  - bacterium from the genus ideonella and family comamonadaceae capable of breaking down and consuming 
    the plastic polyethylene terephthalate (PET) using it as both a carbon and energy source


## references

[^1]: https://korrespondent.net/tech/science/4450037-uchenye-syntezyrovaly-bakteryy-prevraschauischye-uhlekyslyi-haz-v-spyrt
