wa-dyntronics-3p-node-red
=========================

Gazebo Hub Dyntronics Work Area - 3rd Party Components - Node Red

Goals:
* SysML compatibility - Develop a third party UML profile for Node Red models, supporting transform to/from Node Red  (Modelio platform)
* Add electrical component ratings to meta-model – current draw, etc (SysML block via UML profile - UML stereotypes - tagged values)
* Add vendor information to meta-model (SysML...)
* Add data sheet references to meta-model (SysML...)

Notes:
* Node Red uses JavaScript and HTML for node modeling. 
* To do: Define a model transform methodology for interpreting Node Red node models as SysML diagram 'block' elements, esch applying a 'NodeRed::Node' UML stereotype
