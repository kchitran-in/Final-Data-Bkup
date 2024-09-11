

 **Background** 

A  _FrameWork_  is a hierarchical representation of  _Concepts_  (in the context of education, "addition of two single digit numbers" is a  _Concept_ ). Boards can use a Framework to represent their curriculum in a machine readable form. From a structural standpoint, a FrameWork is a Graph, where Concepts form the nodes and relationships among them form the edges (or links). For example, Concept is a type of Node and Parent-Of is a type of edge (or a relationship or a link). There can be several different types of FrameWorks. One such FrameWork is  _Spine_ . A Spine, as the name implies, acts like a spine holding multiple implementations of FrameWorks together. For example, Spine can act as a link between Maharastra State Board's FrameWork and Rajasthan State Board's Framework. But how do we create a FrameWork, how do we do seed it?. This is where Vocabulary comes in. Vocabulary is a set of accepted and/or curated words/terms which form the basis to create a FrameWork. In addition to that, Vocabulary also maintains a set of relationships among those words such as a synonyms, which enable semantic search and discovery.  In this document, we discuss the approach to creation and application of Vocabulary, FrameWorks and the change management services that the Learning Platform needs to support.



 **Problem Statement** 

For motivation and why do we need them, please refer to the [Framework PRD](https://docs.google.com/document/d/1kRvPz1Dl5Vg5MUxAemizbdftMDunKlpkiK6Kf7mTwfM/edit?usp=sharing) and [Vocabulary PRD](https://docs.google.com/document/d/17KOeFZQmlFiOpsuTj1lFNGKzJgbcK4OGt2MD_4D0H-o/edit?usp=sharing)  documents



 **High level Capabilities required:** 


1. FrameWork:
    1. Define, Create, Update,  Delete, Inherit, in parts or whole, via uploads or APIs, where applicable

    
1. Vocabulary:
    1. Define, Create, Update, Delete, Inherit, in parts or whole, via uploads or APIs, where applicable

    
1. Change Management and Conflict resolution

    
    1. Propagate, via configurable policies and rules, the changes made 
    1. inform, warn, summon a stakeholder with information for action when required
    1. Guide a stakeholder either in the authoring or in the migration process, with system generated inputs and suggestions

    

At the outset, it appears like, Spine, Vocabulary, WordNet, etc., all are different. They are different from a functional standpoint but not from structural standpoint. Essentially they all can be represented as graphs. Consequentially, a single Graph management system should suffice. Below we make strong assumptions that dictate the rest of the story. The existing Language Platform supports many of the functionalities. Vocabulary, as it is envisioned above, can be seen in a more general sense as a Knowledge Graph (KG). A KG describes common sense knowledge as well domain knowledge that is machine readable/understandable. An example might illustrate that point. The term "Science" in the context of a Spine, might mean a "Domain" that students need to study as a part of the curriculum. However, in the world sense, "Science" could also mean a popular Television Channel. From here onwards, we refer to KG as a more general version of the Vocabulary. We also use Term to imply a word or a phrase that by itself has meaning in the context of Sunbird.



 **Modeling Premise:** 


1. Any referable entity in Sunbird is a Term in the Knowledge Graph (KG). So all Terms in the KG constitute a master list of Terms.
1. KG provides multiple Views. Each View selects a parts of the KG that serves one functional domain -- Spine,  _a_  Framework, Vocabulary etc.. all are different Views of the underneath KG. 
1. A View is described in the KG itself – by way of specifying what Objects the View is interested and what type of relationships it is interested in. A Spine is a type of View, for eg.. We will give a concrete example in a moment. 
1.  **Everything is a pattern on a Graph: the domain, the policies, its change management, and they can be templatized.** 



 **Design Goals** 


1. Self-describable
1. Domain Agnostic
1. Agile (Configurable, Adaptable to Change)
1. Scalable
1. Modular

In little more concrete terms

 **Taxonomy Framework Representation:** 


1. A Framework is a Taxonomy. It has a hierarchical representation of Concepts. Any Term appearing in a Framework is a Concept.
1. A Framework HAS_A Terms of type "Concepts". Framework HAS_A relationships of at least PARENT_OF. 
1. Framework is a Term by itself in the KG. 
1. A Term in KG would have IS_A_MEMBER_OF a Framework it that Term is representing a Concept in  _that _ Framework
1. It  _must_  support PARENT_OF relationship between Concepts. The resulting taxonomy shall be a DAG (no cycles). The PARENT_OF actually is referring to subtypes going from specific to general.
1. A given Taxonomy to be modeled IS_DERIVED_FROM a FrameWork. They can inherit and extend, in the OOPs sense, a Framework graph with additional relationships and Term types. 
1. Examples:
    1. Spine IS_DERIVED_FROM Framework.
    1. Karnataka framework IS_DERIVED_FROM Spine, when it chooses to inherit and modify the Spine framework.
    1. Mizoram IS_DERIVED_FROM Framework (root). This state is creating a Framework from scratch.
    1. Nagaland IS_DERIVED_FROM Spine and IS_DERIVED_FROM Framework Mizoram. \[ Note: A framework can have more than one parent (multiple inheritance). As a result, Diamond problem needs to be tacked via a convention or conflict resolution or acknowledge and handle later, at the time of creation/updation) ]. 

    

 **Taxonomy Framework Behavior** 


1.  _Seeding a Taxonomy from scratch_ : A Framework object that supports PARENT_OF relationship shall be created. It can accept new relationships such as HAS_DIFFICULTY_FOR for a new Term which is of type Class (as in Grade).
1.  _Seeding a Taxonomy from a single existing Framework such as a Spine: _ On inheritance, all inherited Terms and Relationships are first class objects themselves.  They will be created in the KG. The names may be same but the interpretation of them in the respective Frameworks could be different. These new Terms will have IS_MEMBER_OF to the new Framework, and they will have relation pointers "EQUIVALENT_TO" to  parent Framework, as a default relation. In that sense, logically, every framework is a separate View. Inheritance only accelerates the creation of new relatable frameworks. After inheritance, all Terms and Relationships will be instantiated, and equivalence or parent-child relations will be automatically formed.
1.  _Seeding a Taxonomy from more than one Framework:_ Same as above, except that conflict resolution process has to kick in.
1.  _Conflict Resolution (strategies):_ 
    1.  _A  node is deleted in the Framework, but some other entity has linked to it. _ 
    1. do not permit deletion in such cases
    1. warn about the number of contents impacted, and delete. check if the downstream dependent node can have direct link to to the upstream dependent node (relation dependent resolution management).
    1. warn, delete, and mark the node deleted and make it not available in the Framework for usage
    1. warn, and delete (with impacts)

    
    1. A node is renamed
    1. Renamed node is created. Change is propagated downstream
    1. A new node is created with the "new name" and and Content/Textbooks tagged are not updated. But old concepts can have an "HAS_ALIAS" and point to the new Renamed Node in the taxonomy.

    
    1. A new node is added
    1. It is added to KG as a Concept Term with a membership to the Framework from which is getting created
    1. That newly created node must be attached/linked to some Node (including the root) in the Framework
    1. If no parent is specified, root will be assumed (but can lead to wide graphs, if User is careless)

    
    1. Two or More nodes are merged into One
    1. Do not permit 
    1. Allow if one or both of them are not yet connected (unlikely, if we do not permit dangling nodes to be created in the first place) 
    1. Merge means a Super Concept is being created:
    1. A new Node is created with a new Name and the to-be-merged Nodes are attached to it as children
    1. Existing pointers to the children are unaffected. Only a new Parent is created.  The old parents will be moved as parents of the "merged" node.
    1. however, it might create cycles. 
    1. highlight the cycles, and retain the parent that does not cause this. present option to select one or the other 

    

    
    1. Merge means – two current nodes mean the same thing, therefore, there is no necessity to maintain two distinct nodes in the graph. So they are in principle synonyms to each other. 
    1. Remove one of them, in case other node did not have any content tagged.
    1. Retain both and create an equivalence between these two. 

    

    
    1. A Node is Split into two or more
    1. Meaning a split here is that, two subtype of the Concept are being created
    1. Create the desired number of Child Nodes, with a parent-child relationship
    1. Suggest existing publishers that a new subtype is available, so they can re-visit their Textbook tagging to the Framework. That publisher could be the Framework author itself.

    
    1. Meaning of two separate Concepts not sharing the same parent.
    1. Delete and create two new nodes. 
    1. Handle delete node as described above
    1. Handle two new nodes as addition of two nodes

    

    

    
    1. A link between two nodes is removed
    1. a dangling Concept or disconnected sub Graph are created, which can not be reached
    1. do not permit
    1. attach to the parent (with a specified level). It can be root which is the domain itself.
    1. warn, and force user to re-attach the affected Node to "some" allowable node in the Framework.

    

    
    1. all links between two nodes are removed
    1. analyze each link to be broken one at a time
    1. analyze collectively the best possible salvageable situation

    
    1. a new link is added
    1. the introduction of this new link might cause meaning problems that are specific to the link type.
    1. Examples:
    1. "a grand children" and "parent" are same (w.r.t PARENT_OF) – leading to cycles in the taxonomy
    1. when a new "IS_EQUIVALANT_TO" relationship is added, due to its commutativity, it might induce additional link types at the time of inferencing

    

    
    1. A link between two nodes is renamed

    

    

 **Taxonomy Framework Flow** 


1.  _APPLY _ CRUD on  _a Framework in part or whole_ 
    1.  _add, _  _delete, move, rename nodes_ 
    1.  _add, delete, rename, move  a relationships between two nodes_ 
    1. split or merge nodes

    
1.  _ANALYZE _ Changes
    1.  _validate rights and privileges_ 
    1.  _Detect conflicts, and downstream effects_ 
    1.  _Provide action plan_ 

    
1.  _CORRECT _ 
    1.  _with or without user intervention, prepare a valid "commit"_ 

    
1.  _RE-ANALYZE (go to Step 2)_ 
1.  _COMMIT _ 

 **Methods** 


1.  _Nodes and Relations_ 
    1.  _add, _  _delete, move, rename nodes_ 
    1.  _add, delete, rename, move  a relationships between two nodes_ 
    1. split, merge nodes

    
1.  _Graphs:_ 
    1.  _Create a Graph object_ 
    1.  _attach Objet (Node types), relationship types, and which nodes can bind to which using what type of relationships_ 

    
    1.  _Merge Graph A with Graph B. (Graph A is added to Graph B and Graph B is modified)_ 
    1. Validated Graph A against its own View properties 
    1. Validated Graph B against its own View properties 
    1. Specify the joins (links from Graph A to Graph B)

    
    1.  _Merge Graph A with Graph B to form Graph C_ 
    1.  _same as above except that Graph C is to be created afresh with specified rules_ 

    
    1.  _Filter a Graph_ 
    1.  _Select a sub graph based on few properties such as node and relationship types_ 

    

    
1.  _Policies_ 
    1.  _Create, Remove, Update, Read a policy template_ 
    1.  _Attach, Update, Remove, a partially materialized policy to a Domain_ 
    1.  _Evaluate a policy at run time_ 

    



 **Template Examples (in psuedo code): Everyhing is a pattern on the Graph:** 


1. Create a Framework Factory Graph object
    1. create the Framework name in the KG. 
    1. MERGE (anchor:Term {name:"{{ FrameWorkToBeCreated }}"})

    
    1. Load the supported relationships and their bindings
    1. CREATE (anchor – \[SUPPORTS_RELATIONSHIPS]→ x) FOR ALL  x IN {{ neededRelationships}}

    
    1. Load the compatiable node-node types (a bipartitite graph)
    1. CREATE (anchor:{{relationshipType}} – \[HAS_LEFTNODE_IN]-x) WHERE x IN {{ leftNode}}, (anchor:{{relationshipType}} – \[HAS_RIGHTNODE_IN]-y) WHERE y IN {{rightNodes}}

    

    
1. Add a Concept to a Framework
    1. MERGE (anchor:Term {name:"{{ conceptNameToBeCreated }}"})
    1. CREATE (anchor – \[BELONGS_TO] → (term:{ {FrameWorkName}}))

    
1. Read a Framework
    1. Simply filter the KG with all terms belonging to the Framework. Extract the required subgraph
    1. (in efficient) MATCH p = (anchor:Term – \[BELONGS_TO]→(name:{{desiredFrameWork}})) and  anchor – \[relationships:]– anchor RETURN anchor, relationships

    
1. Policies
    1. Create a policy
    1. No Concept should be left without any parents (in a Framework)
    1. WITH Framework Subgraph, 
    1. Left Operand: MATCH x WHERE NOT (a) – \[: {{supportedRelationship}}] → ()  RETURN  count(a)
    1. Right Operand : 0
    1. Comparator: equal to

    

    
    1. Attach a policy
    1. Framework HAS_POLICY policy_id

    
    1. Apply a policy on a given graph object
    1. Run the concrete query, evaluate all individual predicates, report the troubling predicates with explanation and remedial actions

    

    

 _Drafts Schema ( TBD: have to JSONify)_ 


1. import/export for creating, modifying, deleting, listing parts or whole of one or more Views
    1. export graph (actual upload csv schema might be different than this. upload is actually a UI component)
    1. Nodes tab
    1. <NodeName, additional fields> 

    
    1. Relations Tab
    1. <leftNode, rightNode, relationType, additional relationFields>

    

    
    1. import graph (same as above)
    1. edit graph (actual upload csv schema might be different than this. upload is actually a UI component)
    1. Add Nodes tab (most likely not needed)
    1. <NodeName, additional fields, PolicyName/ID> 

    
    1. Delete Nodes tab
    1. <NodeName, PolicyName/ID>

    
    1. Rename Nodes tab
    1. <OldNodeName, NewNodeName, PolicyName/ID>

    
    1. Split Nodes tab
    1. <OldNodeName, ListOfNewNodeName, PolicyName/ID>

    
    1. Merge Nodes tab
    1. <List of OldNodeNames, NewNode, PolicyName/ID>

    
    1. Add Links tab (most likely not needed)
    1. <leftNodeName, rightNode, linkType, PolicyName/ID> 

    
    1. Delete Links tab (most likely not needed)
    1. <leftNodeName, rightNode, linkType, PolicyName/ID>

    

    

    
1. APIs  for creating, modifying, deleting, listing parts or whole of one or more Views, and their management
    1. can parallel the import/export/edit syntax

    

 **Compound Policy** 




```
{
  "version": 0.1,
  "predicate": {
    "conjunction": "and",
    "predicate": [
      {
        "comparator": "equalTo",
        "policy": "pid_00",
        "value": 0
      },
      {
        "conjunction": "or",
        "predicate": [
          {
            "comparator": "in",
            "policy": "pid_01",
            "value": "[Spine]"
          },
          {
            "comparator": "not in",
            "policy": "pid_02",
            "value": "[Maths, English]"
          }
        ]
      }
    ]
  }
}
```
 **Comments** 


1. For better performance, making Framework, Vocabulary, etc as first entities may be necessary. Handling sets via set membership could result in verbose queries and higher latency
1. Node and Relationship (properties) are listed out here
1. Policies can also have RBAC-based behavior.

 **Summary** 


1. Every referable entity in the Sunbird ecosystem is a Term in the Knowledge Graph (KG)
1. A Framework itself is described in the KG w.r.t what types of Terms can appear, what relationships are supported, and the compatible bindings between entities.
1. Any domain to be modeled such as a Vocabulary or Spine is simply a subgraph (a projection) of the KG. In other words, by applying a set of appropriate filters, we get the desired domain
1. Vocabulary has collection of all Terms appearing in any and all Frameworks and it  inherits the common world knowledge about them (such as synonyms, examples, translations etc..from WordNet)
1. Keywords is again a set of Terms in the KG for a Term in a Framework. So, Keywords is also a certain projection of the KG.
1. Every domain is governed by a set of rules and policies. A policy is a composite predicate. A composite predicted consists of one or more predicates joined by relational operators such as AND and OR and NOT. A predicate evaluates to Truth or False. A predicate takes a function of a result set (of a query on a Graph), and applies a comparator operator to a given policy value, which itself could be a result set. Any policy is a template consisting of the result set (of a graph projection), a comparator and reference value set (truth) that can also be a result set.
1. Any graph operation can be validated w.r.t the policies to be enforced in that domain
1. Policies lend themselves to test cases – thereby this design implicitly enforces TDD approach to building software
1. Upload and Download APIs should be treated as UI components. They should not dictate the import and export schema. Upload is an interface to import, and Download is an interface to Export. (So, Export and Import should be quite general enough). Export can be Download but not vice versa. For example, the current Upload API for ToC in Textbook creation implicitly assumes a PARENT_OF relationship, and support upto a depth of 5. This is not generalizable for arbitrary graphs. Instead, the export schema provided can always be reshaped to support a specific/ restricted API.
1. Since majority of the code (for basic operations, and validation) is outsourced to the underneath graph engined, the developer can focus on business logic and less on low-level Graph management operations. Less code, less bugs





*****

[[category.storage-team]] 
[[category.confluence]] 
