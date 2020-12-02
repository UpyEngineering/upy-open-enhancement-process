# EP - Upy Open Enhancement Process

Streamlining change approval is one of capabilities which drive higher software delivery and organizational performance according to [devOps research](https://www.devops-research.com/research.html). 

This repository holds Change Proposal, Evolution and Enhancement for the *Upy* and Streamline them via merge requests (MR's)

The proposals themselves are colloquially referred to as EPs.

EPs should be approve by reviewers or change approval boards (or Shepherds) to promote changes through the system.

Compliance managers and security managers rely on EPs to validate compliance requirements, which typically require evidence that all changes are appropriately authorized.

## Current EPs

Current EPs are listed in [issues](https://github.com/UpyEngineering/upy-open-enhancement-process/issues).

That why New EPs and additions to current EPs are submitted as [pull requests](https://github.com/UpyEngineering/upy-open-enhancement-process/pulls). 

## How to give feedback

Discussion of ongoing EPs is held under their related issues.

Please don't create new issues unless really necessary, let's try to keep discussions in one place.

## How to propose

Feel free to submit a pull request with a proposal here. A proposal should describe in detail why the feature is needed, how is it going to be implemented in upy and whether any changes will be required. Use [Kotlin proposals](https://github.com/Kotlin/KEEP/tree/master/proposals) as an inspiration.

We appreciate your work, but can not guarantee that all proposals will be considered soon after submission.

### EPs Shepherds aka reviewers

To get under active consideration, a proposal usually need a **Shepherd**. Proposals are assigned to Shepherds (through the github *assignee* field) that must be maintainer of the EPs project on github. Unfortunately, as our resources are limited, a proposal may remain without a Shepherd for an undetermined amount of time. Some CAPs get Shepherds proposed by the project lead, some don't. In the latter case project members are free to volunteer for the Shepherd role.

> Proposal authors may try to convince potential Shepherds to volunteer. It usually helps to get the proposal under active consideration. 

In the [continuous delivery](https://cloud.google.com/solutions/devops/devops-tech-continuous-delivery)
paradigm the Shepherds has vital **roles responsibilities**, which includes:

- Tracking the feedback and keeping the proposal in check with the discussions. This means that the Shepherd often collaborates with the proposal author on the text of the proposal.
- Coordination between teams and presenting the proposal at design meetings and initiating its consideration for a particular plateform version.   
- Weighing in on important business decisions that require a **trade-off** and
**sign-off** at higher levels of the business, such as the decision between
time-to-market and business risk.

## EPs as a process

We are gradually switching the design of Upy platfom to this open process, the details of EPs will be refined as we go.
