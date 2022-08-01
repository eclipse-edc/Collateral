# Usage Control

## Content:

- [Overview & Viewpoints](./README.md)
- [Ecosystem](ecosystem.md) (TODO)
- [IAM](iam.md) (TODO)
- [Access Control](access_control.md) (TODO)
- [Transparency](transparency.md) (TODO)
- [Temper Resistance](temper_resistance.md) (TODO)
- [Enforcement](enforcement.md) (TODO)
- ...

## Overview

Usage Control is a concept to expand data protection from the provider system to the IT environment of the user. Similar to IT Security, Usage Control can never be reached in an absolute manner but always depends on the requirements and potential threads of each use case. In that sense, _enough_ Usage Control is reached if the effort necessary to bypass the measurements is significantly higher than the value of the data. Also similar to IT Security, the overall control level is only as strong as its weakest aspect, therefore, Usage Control requires always comprehensive treatment, including technical methods, organizational practices as well as the awareness of the envolved people.

Due to the complexity of the topic and the huge amount of influencing factors, a matrix structure is outlined in the following to organise the various aspects. The relevant topics are grouped in _viewpoints_, each regarding a dedicated set of _concerns_, which have been introduced through identified _stakeholders_. This approach follows roughly the recommendations of ISO/IEC 42010 and uses its terminology in the following.

![Viewpoints](diagrams/usage_control_viewpoints.png)

*Matrix of horizontal and vertical viewpoints of Usage Control.*

Separating the concerns and to simplify the following discussion, the interdependencies of the horizontal viewpoints are mostly limited to the direct neighbors. The vertical viewpoints, however, affect all horizontal ones. For instance, the horizontal viewpoint _Technical Communication_ mostly affects and is affected by the _Business Interactions_ and the _Contract Representation_ as well as the descriptions in all vertical viewpoints.


## Business Viewpoint

### Roles: Organizations, Human and Technical Users

Contracts are negotiated in principle between legal entities. In the case of the EDC, that implies that organisations are the anchors of any ContractOffer or ContractAgreement, therefore, only organisations possess or grant usage rights. Nevertheless, policies need to provide the expressiveness to further restrict the potential users of an Asset. If for instance Company A grants its business partner Company B access to their production plan, Company A usually wants to prohibit that every employee of Company B can see it. Consequently, the ContractAgreement between Company A and Company B need a Constraint describing the allowed endusers.

The EDC fulfills this requirement by ... <!-- TODO: Explain the solution. -->
