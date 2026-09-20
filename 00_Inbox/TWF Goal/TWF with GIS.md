# Motivation

The proposed enhancement leverages the existing fiber mapping platform and OTDR monitoring infrastructure to add intelligent analysis capabilities to the technician result collection tool. While the mapping system is currently used primarily for point-to-point OTDR monitoring on the OLT side, the existing data model already supports full PON topology representation, including OLTs, splitters, feeder fibers, distribution fibers, drops, and ONTs. By integrating this topology data with uploaded field measurements such as optical power levels, OTDR traces, and speed tests, the system can calculate the expected optical power range at any point in the network and automatically compare it against technician measurements in real time.

This creates immediate operational value by improving technician troubleshooting and validation workflows. Today, technicians often rely on experience or manual calculations to determine whether a measured optical power level is acceptable. With this enhancement, the software can automatically determine whether a reading is within the expected range for the exact measurement location — whether at the OLT, splitter input, splitter output, terminal, drop, or ONT. When abnormal readings are detected, the platform can provide guided troubleshooting recommendations and identify the most likely fault zone within the network.

Because the platform understands the physical network topology, it can also provide intelligent diagnostics based on neighboring network behavior. Instead of evaluating a technician’s measurement in isolation, the system can compare the result against similar branches, splitter legs, or nearby ONTs within the same PON. For example, if multiple customers on the same splitter are operating within expected ranges while a single branch shows excessive loss, the software can suggest that the issue is likely isolated to the drop, connector, or customer-side equipment. Conversely, if multiple branches on the same splitter show similar degradation patterns, the platform can identify the splitter or upstream feeder segment as the probable fault area.

The enhancement also enables proactive network health monitoring by tying uploaded field tests directly to network segments. Operations teams gain visibility into recurring degradation trends, unhealthy splitter legs, chronic feeder issues, or areas with repeated failed installs and service calls. Instead of reacting only after customer complaints occur, the platform can begin identifying potential network issues earlier using data that technicians are already collecting today.

The business value is especially compelling because the core infrastructure and workflows already exist. The organization already maintains detailed fiber topology data and already collects technician test results through the current platform. As a result, the enhancement primarily focuses on correlation logic, optical budget analysis, and operational intelligence rather than deploying new hardware or significantly changing field processes. This creates a relatively low-risk, high-value enhancement that can reduce mean time to repair (MTTR), decrease repeat truck rolls, improve install quality, and provide leadership with better visibility into overall network health across both point-to-point and PON environments.
	
AI Integration




# Vision

Capabilities
* Fault Localization - Use OTDR traces along with geolocation and fiber map to identify where an issue is.
* Path Tracing
	* Identify path from ONT->OLT
	* Which splice points are in this path
	* Which cable segments is causing loss
* Contextual test interpretation
	* Expected loss based on splice count
	* Expected reflections based on connectors
	* Whether a failing segment is upstream or downstream
* Job guidance - Much more detailed data
		Go to this hand hole, open tray 2, work on fiber 12 blue-orange"
* Basis for data collection) [[Standards]]
	
	
Features
* [[Segment Health Scoring]]
* [[Live Path Validation]]
* [[Splice Visulalization]]
* [[Workorder Auto-Population ]]
* [[Field Mode]]

# FiberTestandMappingAppOverview

## FiberTestandMappingAppOverview

## ProblemStatement

The team is developing a fiber test and mapping application that needs to:
▪ Import and visualize fiber network data(e.g.,KMZ/KML files).
▪ Model realistic Passive Optical Network(PON) topologies.
▪ Provide operational intelligence for field technicians (segment health, path validation).
▪ Integrate with existing monitoring standards forOLT/ONT devices.

## Goals& Objectives

▪ **DataImport:** Enable ingestion of fiber geometry fromKMZ/KML sources (e.g.,FiberNetwork
Alliance).
▪ **Synthetic PON Modeling:** Generate realistic PON layouts anchored to real backbone fiber for
demo/testing.
▪ **HealthScoring:** Implement segment health scoring to detect degradation before outages.
▪ **PathValidation:** Provide live path validation to isolate faults quickly.
▪ **MonitoringIntegration:** SupportOLT/ONT telemetry via OMCI, TR-069/369, and vendor
APIs.
▪ **TopologyIntelligence:** Automatically detect and label fiber breakouts, and infer OLT
locations from geometry.
▪ **CoverageModeling:** Define expected geographical coverage are as for single PONs.

## KeyFeatures

1. **KMZ/KMLImport**
    ▪ Support importing fiber routes and geometry.
    ▪ Align synthetic PON structures with real backbone fiber.
2. **SegmentHealthScoring**
    ▪ Compute health scores(0-100) based on loss, reflectance, failure history, trends, and
       environment.
3. **LivePathValidation**
    ▪ Trace optical path from ONT to OLT.
    ▪ Validate each segment using latest test results.
    ▪ Highlight failing/marginal segments visually.
4. **OLT/ONTMonitoringIntegration**
    ▪ UseOMCI(viaOLT),TR-069/369, and vendor SNMP/NETCONFAPIs.
    ▪ Display ONT optical power, LOS/LOF, alarms, and status in realtime.
5. **SyntheticPONGeneration**
    ▪ Example Douglas,GA topology:1 OLT,4 splitters, 128 ONTs.
    ▪ KML skeleton for feeder, distribution, and drop cables.
6. **TopologyIntelligence**
    ▪ Detect and label fiber breakouts (splice, splitter, cabinet).
    ▪ Infer OLT locations from fan-out analysis and cable hierarchy.
7. ▪ Identify expected PON coverage areas (5-^10 km radius typical).

## UserStories

▪ **As a field technician** , I want to see segment health scores so I know which fibers are
degrading before they fail.
▪ **As a dispatcher** , I want live path validation so I can send techs directly to the failing
segment.
▪ **As a developer** , I want to import KMZ/KML files and generate synthetic PONs for demo
purposes.
▪ **As a network engineer** , I want to integrate OLT telemetry so I can monitor ONTs without
test equipment.
▪ **As a planner** , I want to detect fiber breakouts and OLT locations automatically from
geometry.

## OpenQuestions/ NextSteps

▪ Define exact data fields required for segment health scoring and path validation.
▪ Build pseudocode/algorithms for break out detection and OLT inference.
▪ Map out vendor-specific OLTAPIs and telemetry fields to integrate.
▪ Expand synthetic PON inventory (cables, fibers, ONTs) into importableCSV/JSON schema.


▪ Decide on visualization standards for breakout types and health scoring.

## Tasks
* Get embedded WMS working
* Attach fiber ID and/or circuit id to test result

## Appendix

### SpilloverInsights

▪ Public PON KMZs are not available for security reasons; synthetic generation is required.
▪ Fiber Network Alliance KMZ provides real backbone geometry but not PON details.
▪ Theoretical PON reach is up to 20 km, but practical deployments limit to 5-10 km radius.
▪ Images referenced(e.g.,RabinowitzFacility)likely show OLT hubs with feeder/distribution
fan-outs.

This document synthesizes the group’s exploration into a **ProductRequirementsDocument
(PRD)** for the fiber test and mapping app, capturing both technical concepts and practical
deployment considerations.