---
title: MDI Pipelines
has_children: true
nav_order: 40
---

## {{ page.title }}

You now have the tools and skills in place
to begin to work with MDI Stage 1 Pipelines, where
a **pipeline** is a set of analysis actions applied to a
set of data inputs.

### High-level view of pipeline execution

We will guide you to installing a pipeline command line utility, 
or interface (sometimes called
a CLI). The utility is a program subject to the same rules you 
learned for any Linux command. It will have subcommands, take 
options and inputs, and create outputs and messages.  

The primary input to the mdi program is
a is a **job configuration file**, a YAML-format file 
whose purpose is to declare values for the sometimes
long set of options required to describe a data analysis, 
including what pipeline you want to run, the target 
data, analysis parameters, what account to use, etc.

The mdi utility will read your job configuration file and 
either run the requested work synchronously, i.e., in your
terminal window, or asynchronously, by submitting the request
to the job scheduler on your behalf.

The primary output of the mdi utility depends on the subcommand,
but in general is a summary report of the jobs submitted,
their status, log reports, etc.
