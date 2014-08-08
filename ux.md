# User experience patterns

This is a relatively new area and a number of approaches should be tested by allowing several components to be easily reused/composed/sequenced/layed out in different ways.

Example use cases:
 - Add table interface to the Open Oil corporate network navigator
 - Add a graph visualisation component to grano-ql
 - ...

Links:
 - [Rough thoughts from iilab about navigating/querying/investigating graphs](https://www.penflip.com/jun/iilab-graph/blob/master/graph-interfaces.txt)
 - ...

## Components

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