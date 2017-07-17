# pakbon-ld
Linked Data translation of the SIKB archaeological protocol 0102 (aka Pakbon)

## Description
Archaeological projects typically produce a large number of information containers, amongst which are documents and reports on excavation activities and discovered artifacts. In Modern archaeology, this often also includes various forms of media, as well as general-purpose and geospatial databases. Common practice amongst archaeological institutes and companies is to store everything on a hard drive once a project has been wrapped up, only to be retrieved on request. As a result, the majority of the world’s recent archaeological knowledge is currently being contained in almost forgotten silos. Together with the thoughtless use of various (dated) proprietary and closed data formats, as well as a lack in uniformity with respect to those data formats, this quickly becomes any researcher’s worst nightmare.

The need for a solution became apparent as recent as the last decade, with several local initiatives having been set up around the world since. In the Netherlands, a collaborative effort of the KNAW, the RCE, and the SIKB has resulted in a three-part solution. Vital to that solution is the Archaeological Protocol 0102, developed and maintained by the SIKB. This protocol provides a specification as to how rich XML summarizations, aptly named the pakbon (package slip in English), could and should be extracted from archaeological projects. Once created, a pakbon could then be uploaded at the online data storage service DANS; an institute of the KNAW and NWO that aims to offer a sustainable platform for archiving and reusing research data.
Despite now having an online depot full of pakbonnen (pl. in Dutch), each one is still an isolated entity. Therefore, researchers still have to look up and download every pakbon which might be of use in their research. Moreover, the use of a XML data format imposes several limitations upon the data and its use, amongst which are its limited support for semantics and for reasoning, as well its habit of enforcing a tree-structure upon the data it holds. Fortunately, these limitations can largely be lifted by moving to a different data format.

In the context of ARIADNE, a joined venture between the VU and Leiden University is currently working on a Linked Data version of the pakbon, called pakbon-ld. To this end, we first translated the original tree-structured data model to a graph-structured version that is capable of supporting more complex relationships and dependencies. This was followed by the conversion of domain-specific thesauri to a version that complies with Semantic Web standards. Once these foundations were completed, we started working on a tool for automatic conversion from pakbon to pakbon-ld formats, and we have been perfecting this tool ever since. We will concisely describe these parts next.

While differently structured, the new data model incorporates the exact same set of archaeological concepts as are specified in the original protocol. However, while the original properties were used as starting point, we have both restructured and expanded them to fully benefit from the graph structure. Both element types have been defined using the well-known CIDOC CRM ontology, which is particularly well suited for modeling data from the cultural heritage domain. In addition, an extension to this ontology, CIDOC CRM-EH, was used to model domain-specific concepts and relations. Note that, to ensure domain validity, each change to the model has been evaluated together with archaeological researchers.
To minimize the possible ambiguity between project documentation, Dutch archaeologists generally refer to the ABR. Managed by the RCE, the ABR contains a set of multiple thesauri on specific archaeological terms. To facilitate this convenience, we created a Semantic Web complaint version of the ABR. For this purpose, we employed SKOS, thereby allowing users to benefit from the semantic hierarchy.

In order for the conversion tool to ensure uniqueness of URIs, we generate a hash value from each concept instances’ properties. These values are crosschecked together with the online data cloud to see whether this exact instance has already been converted at an earlier stage. If such a clash occurs, then the processing of that instance will be skipped and the already-processed version will be used instead. If no clash occurs, then that instance and its properties will be converted in a depth-first approach. If desired, a separate ontology and vocabulary graph could be created as well. Once completed, the user may decide whether or not to add the newly-created graph to the data cloud.

Those wanting to experiment, a live test server is running on pakbon-ld.spider.d2s.labs.vu.nl.

## Dependencies
- python >= 3.4
- python library rdflib

## Usage
`pakbon-ld.py [-h] [-i INPUT_PATH] [-o OUTPUT_PATH] [-d DEFAULT_NAMESPACE] [-f {n3,nquads,ntriples,pretty-xml,trig,trix,turtle,xml}] [--version] [--ignore_version] [--align {local,global,both}] [--enable_georesolver] [--align_with [ALIGN_WITH [ALIGN_WITH ...]]] [--endpoint ENDPOINT] [--interactive] [--generate_ontology] [--generate_vocabulary]`



Author: wxwilcke,
Source: https://github.com/wxwilcke/pakbon-ld