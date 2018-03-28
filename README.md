FermionHamiltonian

Before doing calculation of a finite size fermion system, one need to define a Hamiltonian object. This object contains all the information of Hamiltonian in the cluster, like : hopping terms, Coulomb U, inter site V....

After it being defined, it can futher be used for Lanczos or Hoseholder method directly.


## example
In this example, adding a hopping term between site 0 and site 3 is shown. In formalism, it represent the term:   

  t<sub>03</sub>Σ<sub>σ</sub>(c<sup>+</sup><sub>0σ</sub>c<sub>3σ</sub>+h.c.) </br>

one can find many more kinds of interactions in source code directly.



    program main
      use FermionHamiltonian
      implicit none

      TYPE(Ham)::h
      integer::hpara(8)
      complex*16::v
      character*16::Intp


      ! Initialization  (needed)
      call h%Initialization( ns = 6)


      ! start append H terms  (needed)
      call h%StartAppendingInteraction()


      ! append a hopping term between site 0 and site 3
      Intp     = "Hopping"
      hpara(1) = 0
      hpara(2) = 3
      v        = (1.0_8,0._8)

      call h%AppendingInteraction(InterType=Intp,InterPara=hpara,InterV=v)


      !End appending (needed)  After this subroutine being called, no more terms can be appended into H
      call h%EndAppendingInteraction()


      ! more terms can be found in source code directly.
    endprogram



## tips
function h%StartAppendingInteraction() must be called before appending interactions. And h%StartAppendingInteraction() must be called after all appending finished. These two subroutines should only (and must ) be called once. h%StartAppendingInteraction() can be called for many times in order to append all kinds of interactions.
