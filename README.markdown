## VERSIONED ML (VML) ##
The paper (with typos and formatting errors fixed) can be found [here](https://github.com/icfp2017/vml/blob/master/vml.pdf).
VML programming framework and the associated tools are distributed via Docker.
To install Docker, please see
[this](https://docs.docker.com/v1.10/mac/step_one/) for
Mac, or [this](https://docs.docker.com/engine/installation/linux/ubuntu/) for
Ubuntu. 

### Examples ###

To try the examples presented in the paper (counter, canvas etc), please get
the VML docker:

        docker pull icfp2017/vml

Then run `bash` in the docker:

        docker run -it icfp2017/vml bash

Your bash prompt must change to reflect the docker enviroment with `opam` user.
VML and all its dependencies are already installed in the docker. To run the
examples, navigate to `~/DaLi/examples`. Each example is in its own directory,
and comes with a README file describing the example and how to run it. The
examples are all pre-compiled, so you can simply run the executables. For
instance, to run the Canvas example:

        cd ~/DaLi/examples/canvas
        ./canvas

The sample output is shown below:

       $ ./canvas 
        Alice: 
        <45,78>: (17,17,17)
        <93,127>: (23,23,23)
        <98,17>: (23,23,23)
        Bob: 
        <45,78>: (64,64,64)
        <93,127>: (23,23,23)
        <98,17>: (23,23,23) 

### PPX ###

VML relies on [Irmin](https://github.com/samoht/irmin) to persist and
distribute its objects. Irmin's representation of objects differs significantly
from OCaml, and it also requires the object types to provide various
serialization functions. We built a [PPX](https://ocaml.io/w/PPX) plugin called
`derive-versioned` to automate this process. Unfortunately, the PPX plugin and Irmin
have conflicting dependencies (because PPX plugin was built with the future plan of 
extending it with Modular implicits), so we have to package them as separate dockers at the moment.
The `derive-versioned` docker can be obtained as following:

        docker pull icfp2017/derive-versioned

To test its functionality, run bash in the docker:

        docker run -it icfp2017/derive-versioned bash
        
To examine the derived version of the `example.ml` file in the generated `derived.ml` file, by executing:
        
        cd canvas
        make test

To observer similar output as sample output above. 
Use the PPX extension with the compiler and run the canvas example, by executing:
        
        cd canvas
        make
        ./canvas.out
        

