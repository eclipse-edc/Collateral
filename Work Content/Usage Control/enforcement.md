# Viewpoint Enforcement


## Decision Logic

Usage requests to a specific Asset usually result in the consideration of a set of applicable policies. The Policy Decision Points can have more than one stored ContractAgreement for one Asset and one Subject, which individual decisions need to be combined. In accordance with XACML3.0, this process is called a _policy-combining algorithm_.

---
*Example 1*: The company Example Inc. has exactly two ContractAgreements for the bill of material of company Example2 SE's product. ContractAgreement1 specifies the usage for EMEA and ContractAgreement2 for APAC. This leads to the following situations:
 1. A _read_ request originating from a server located in Central Europe is evaluated to `permit` by ContractAgreement1 but to `deny` from ContractAgreement2.
 2. A _read_ request originating from a Chinese server is evaluated to `deny` by ContractAgreement1 but to `permit` from ContractAgreement2.
 3. Any requests coming from servers in North America lead to a `deny` decision from both policies.

 In the cases 1. and 2., conflicting individual results need to be combined through the PDP. Obviously, the expected results are that the usage of the bill of material is granted for the first and second cases but prohibited for the third.
___

 As motivated in Example 1, the default policy-combining algorithm for the EDC is `permit-overrides`, meaning that the usage shall be granted if at least one policy allows it.

 ---
 *Note*: Explicit prohibitions are not possible with this approach. More sophisticated policy-combining algorithms are required to solve situations where at least one ContractAgreement allows an usage action while another ContractAgreement explicitly denies it.
___
