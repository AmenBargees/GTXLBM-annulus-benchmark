==============================================================================
PROJECT:            Rothman-Keller Multiphase Thermal LBM
AUTHORS:            Peter Mora, Leila Honarbakhsh and Gabriele Morra
PRINCIPAL:          Peter Mora
==============================================================================

This code is part of an unreleased research framework developed by the principal 
author, Peter Mora. To protect the proprietary nature of the framework 
prior to its official release, this code is provided exclusively as a secure, 
private sample for job application review and is not hosted publicly.


++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
+                               COPYRIGHT & TERMS OF USE                             +
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

Copyright (c) 2026. All rights reserved. 
This software and source code are the intellectual property of the principal 
author. This code is provided strictly as a professional sample for job 
application review. It may not be copied, distributed, modified, or used for 
any other purpose without explicit, prior written permission from the 
principal author.

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
+                              DEVELOPMENT HISTORY & CREDITS                         +
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

Peter Mora developed and optimized the original TLBM single-phase code in C 
and Python, and developed the initial prototype immiscible LBM code in Python. 
Building upon these baseline codes, Leila Honarbakhsh commenced the integration 
of the two frameworks, including adapting the C computational kernel.
Leila Honarbakhsh subsequently worked in close collaboration with Peter Mora 
to finalize, optimize, and debug the complete TLBM immiscible multiphase 
code presented here.

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
+                             CODE SUMMARY & CAPABILITIES                            +
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

The presented RKTLBM framework is a geodynamics model, providing a grounded 
approach for modeling the planet's core formation. This model is capable of 
simulating thermal convection and iron-silicate segregation inside the magma ocean.

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
+                                 REPOSITORY STRUCTURE                               +
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
   
The RKTLBM folder consists of:
* RKTLBM C kernel: Performs the core, high-performance computational calculations.
* Python code (RKTLBM.py): Includes the C kernel and executes the model on HPC 
  clusters by managing all parallelization commands.
* optimal_domain_decomposition: Necessary logic for parallelization spatial distribution.

Run Subfolders:
* Ra_tests_runs: Stores the input file where the input simulation parameters are set.
* Ra_tests_tmp: Stores temporary simulation data, including intermediate images.
* Ra_tests_out: Stores final simulation output (.out) files.

* Two initial temperature and velocity arrays (omitted due to file size):
  These arrays represent a steady-state convection profile that can be fed directly into 
  RKTLBM.py. Utilizing these pre-calculated states saves significant computational 
  time by bypassing the initial spin-up phase, allowing the impactor to be placed 
  directly at the top of an already fully convective domain. 
======================================================================================