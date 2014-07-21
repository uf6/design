# UF6

Uranium Hexafluoride - Used for enrichment

![](http://upload.wikimedia.org/wikipedia/commons/thumb/9/94/Uranium_hexafluoride_crystals_sealed_in_an_ampoule.jpg/330px-Uranium_hexafluoride_crystals_sealed_in_an_ampoule.jpg)

# Problem

Too many graphs, too many frameworks, too many data structures, too many good intentions, not enough concrete technical interoperability.

Developers need reusable components, data structures and practical advice on the way to Linked Open Data without getting lost in the complexity of it.

## Problem solvers
 - [Pudo](http://granoproject.org/) / Grano [demo](http://beta.grano.cc/#/) - [source](https://github.com/granoproject)
 - [iilab](https://iilab.org) / Open Oil Corporate Network Navigator [demo](https://openoil.iilab.org) - [source](https://github.com/iilab/openoil)

### Others to get on board
 - [Journalism++](http://www.jplusplus.org/en/) / Detective.io - [demo](http://www.detective.io) - [source](https://github.com/jplusplus/detective.io)
 - [Shidash](https://github.com/shidash) / Transparency Toolkit - [demo](http://transparencytoolkit.org/) - [source](https://github.com/TransparencyToolkit/Transparency-Toolkit)
 - MC
 - Open Corporates
 - ... (Submit a Pull Request with your name)

# Solutions

Find solutions by openly designing interoperability approaches such as:
 - Data enrichment in practice (our own user centric because its good to try and share about the hurdles)
   - How do I import CSV from Open Oil into Detective.io ?
   - How do I use Transparency Toolkit scrapers
 - Experimenting with user experience patterns
   - How to make query building natural for investigators?
   - How can patterns be found in the graph?
   - When are tables best, when are graphs best, when are they both needed, in which proportion?...
 - Identify opportunities to use common data structures 
   - Provenance
   - Reputation
   - ...
 - Keep track of computer science development that can be applied to real world applications
   - Distributed Stores / Federated Queries
   - UI description layers
   - ...

# Implementation

## User experience patterns

This is a relatively new area and a number of approaches should be tested by allowing several components to be easily reused/composed/sequenced/layed out in different ways.

Example use cases:
 - Add table interface to the Open Oil corporate network navigator
 - Add a graph visualisation component to grano-ql
 - ...

Links:
 - [Rough thoughts from iilab about navigating/querying/investigating graphs](https://www.penflip.com/jun/iilab-graph/blob/master/graph-interfaces.txt)
 - ...

### Components

This is a first attempt, using [Web Components](http://webcomponents.org/) / [Polymer](http://polymer-project.org/), to design abstract components that could be using different implementions, interaction patterns, be displayed/hidden...

Other implementation following the same patterns could co-exist (in Angular, Meteor,...)

```
<uf6-app query="{{query}}" backend="cypher" endpoint="localhost:7474" result="{{results}}" context="{{context}}">
    <!--
	/**
	 * uf6-engine probably extends uf6-engine and implements 
	 *   the connection to the backend
	 *
	 * @backend is the backend type (cypher, mql, sparql, gremlin)
	 * @endpoint is the backend end point
	 * @query is query built from the query components.
	 */
	-->
	<uf6-results results="{{results}}" context="{{context}}">
	    <!--
		/**
		 * uf6-results is the component displaying results 
		 *
		 * @results is the current query results within the context.
		 * @context is the whole slice of data the user is interested in. 
		 *   This could be for instance a "saved query" which the user 
		 *   has "pinned" and within which s/he is navigating.
		 */
		-->
	    <uf6-context-control context="{{context}}"></uf6-context-control>
	        <!--
			/**
			 * uf6-context-control exposes controls for the context, for instance
			 *   by allowing to narrow down a selection or expand it (which might 
			 *   be something that uf6-table and uf6-graph also do by themselves) 
			 */
			-->
		<uf6-table results="{{results}}" context="{{context}}"></uf6-table>
	        <!--
			/**
			 * uf6-table probably extends uf6-results-component
			 *   and is a table view for results.
			 */
			-->
		<uf6-graph results="{{results}}" context="{{context}}">
	        <!--
			/**
			 * uf6-graph probably extends uf6-results-component
			 *   and is a graph view for results.
			 */
			-->
			<uf6-graph-overview results="{{results}}" context="{{context}}">
		        <!--
				/**
				 * uf6-graph-overview is a zoomed out navigation component to see more 
				 *   more context and navigate
				 */
				-->
			</uf6-graph-overview>
		</uf6-graph>
	</uf6-results>
	<uf6-querybuilder query="{{query}}">
		<uf6-query-fulltext></uf6-query-fulltext>
		<uf6-query-facet type="node|relationship"></uf6-query-facet>
	</uf6-querybuilder>
</uf6-cypher-engine>
```

## Data structures

We'd like standards on data that allow simple and meaningful reuse of data such as:
 - Dealing with provenance
 - Deals with key entities like organisations and people

Ideally there would be different levels of implementatin which would allow:
 - Minimum: very quick fixes that can be made to allow data sets to interoperate.
 - Core: the solid way to make data enriching predictable and repeatable
 - Extended: the cherry on top.

### Provenance

 - Provenance
 	- Open Provenance (Ontology)
 	- ICFJ provenance
 - Verification
 - Reputation
    - ?
 - Organisations/Institution
    - [Popolo](http://popoloproject.com/) 
 - Contracts
    - Open Contracts?
    - Open Spending?


