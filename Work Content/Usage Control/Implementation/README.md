# Implementation Viewpoint

The implmentation of the usage control concepts and their enforcements happens in the EDC in the several phases, starting with the access to the `catalog`, the `negotiation` of contracts, and the `data_request` (not yet implemented) to download assets.

In each phase, a respective contract service provides methods to the business workflow. These services forward context information together with the given phase (called 'scope') to the policy engine, which when decides whether or not the respective access is granted.


## Initialisation 

As of August 2020, the EDC has no capabilities to check the surounding environment or the parameters of its underlying operating system. Future extensions could add hardware checks or Trusted Platform Modules (TPM) to verify the integrity of that.


## Discovery

The discovery phase is the point in time when a connector requests access to another connector's asset catalog. Depending on the nature of the connector, a providing connector may only display a filtered number of its data offers. One motivation could be that already the data offers and the asset's self-description can expose valuable information to direct competitors.

The EDC approaches this challenge in the `catalog` scope, which ellaborates a `ContractDefinitionService` instance to check incoming requests against the pre-defined configurations of a `PolicyDefinitionStore`. The ContractDefinitionService fowards the found definitions to the Policy Engine, and thereby filters the exposed self-descriptions at runtime.


## Negotiation

After finding relvant data assets during the discovery activities, the potential consumer initiates a negiation with the data provider. All steps of this process are stored in the `PolicyNegotiationStore`, including the finally achieved `Contract Agreements`. 


## Enforcement

Whenever a consumer connectors requests a download from a providing connector or a business application wants to consume data assets under a usage control regime, an enforcement of the agreed contracts must apply. The business applications therefore queries the `PolicyNegotiationStore` for the respective contract agreement and then calls the Contract Validation Service.


### Contract Validation Service 

The Contract Validation Service executes a number of syntax and plausibility checks and then forwards the request to the policy engine.


### Policy Engine

Each implementation of an EDC usage enforcement engine must implement the `PolicyEngine` interface from the core Service Provider Interface (spi/core-spi) module. The `PolicyEngine` ensures that the basic funtions are provided:
- register rules
- evaluate rules for a certain situation (assetId, consumerId, ...)


## Limitations

### 1. No external Enforcement possible
The current design with the ContractValidationService and the PolicyEngine as the main parts does not allow the integration of stand-alone enforcement solutions, as for instance the [Open Policy Agent](https://www.openpolicyagent.org/) or other proprietary solutions. As real-world enforcement scenarios will most likely rely on products independent of the EDC, a well-defined and future-proven interface concepts both to embedded, policy engine-like solutions as well as remote services is required.

This concept needs to provide manners to manage contract agreements also in stores outside of the `PolicyNegotiationStore`, as the external solutions provide their own policy storage, as well as a easily exchangeable pattern for requesting access or usage permissions. The [XACML](https://docs.oasis-open.org/xacml/3.0/xacml-3.0-core-spec-os-en.html) proposed concept of `Policy Points` appears as a suitable and well-proven concept.


### 2. Separation of Negotiation and Enforcement Policies
Follwing the principle of separation of concerns, the applicable policies should be stored in an own location, instead of being mixed with non-applicable ones still in the negotiation phase.


### 3. Access Desicion independent of Contract Identifier
The identifier of a suitable contract should not be in the scope of the business application but encapsulated within the evaluation functionality. The business application should not be bothered which policy applies to a given situation but can rely on the policy engine that any (or none) permits the current request.


### 4. No Retrival of external Information possible
The current design limits the evaluation of policies to the locally available attributes, e.g. preconfigured attributes like location or directly available information like the system time. Additional attributes sent with the incoming request, e.g. attributes of a message token, are also available for the decision process. However, policies which require the request of externally provided information, for instance whether or not a financial transaction has been cleared already, cannot be supplied.

Such external `Policy Information Points` (PIP) are however necessary to open the evaluation process to necessary information from its environement. Extending the PIP idea also to locally available information provisionings, e.g. the system time, decouples the parameter access and thereby simplifies the development of policy extensions.