---
deck: Mastermind my memory::ReactJS
---
# Thinking in React

<!-- basicblock-start oid="ObsUZdrJw3d45XM3K3w8MeIh" -->
***What is the 5 steps to follow to build an app thinking in React ?::

Begin with mock and then :

1) Break the UI into the component hierarchy
2) Build the static version
3) Identify The Minimal (but complete) Representation Of UI State
4) Identify Where Your State Should Live
5) Add Inverse Data Flow

<u>More details :</u> 

1) - **Break the UI into the component hierarchy
	- Respect the single responsability principle
2) - **Build the static version
	- renders the UI with no interactivity
	- Don’t use state at all to build this static version , use only props. State is reserved only for interactivity.
	- The component at the top of the hierarchy (`FilterableProductTable`) will take your data model and will pass data to childs.
3) - **Identify The Minimal (but complete) Representation Of UI State
	- Use DRY : Don't Repeart Yourself.
4) - **Identify Where Your State Should Live
	- Identify every component that renders something based on that state.
	- Find a common owner component (a single component above all the components that need the state in the hierarchy).
	- Either the common owner or another component higher up in the hierarchy should own the state.
	- If you can’t find a component where it makes sense to own the state, create a new component solely for holding the state and add it somewhere in the hierarchy above the common owner component.
5) - **Add Inverse Data Flow



<!-- basicblock-end -->