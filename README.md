Gazebo Hub Dyntronics Work Area - 3rd Party Components - Node Red
=================================================================

Work Area Source Repository: [wa-dyntronics-3p-node-red](https://github.com/GazeboHub/wa-dyntronics-3p-node-red)

See Also: [_Integrating DIY Electronics Projects into Dynamic Scientific Practices and Lifestyles_ - Gazebo Hub Work Area](https://github.com/GazeboHub/wa-dyntronics)

## Overview

[Node-RED](http://nodered.org/) defines an API in HTML and JavaScript, for defining models comprised of _node_ elements and _flow_  associations. Broadly, Node-RED defines an implicit _meta-model_ within that API, such that a Node-RED _model_ may be represented with a SysML _block diagram_ - ostensibly, via the SysML4UML subset, using a UML _profile_ extending on SysML.

Pragmatically, a SysML model for Node-RED _node networks_ may be implemented in EMF, then supported with a domain-specific application of the Eclipse IDE. 

Abstractly, Node-RED provides a simple example of a network device control system, such that may serve as making an interesting study before studying more complex frameworks such as [Fieldbus](http://www.fieldbus.org/).

Regular Node-RED usage: Refer to [Node-RED _Getting Started_ Guide](http://nodered.org/docs/getting-started/)

## Goals

* SysML compatibility - Develop a third party UML profile for Node Red
  models, supporting transform to/from Node Red  (Modelio platform / EMF, Rhino, Xerces-J)
* Add electrical component ratings to meta-model – current draw, etc
  (SysML block via UML profile - UML stereotypes - tagged values)
* Add vendor information to meta-model (SysML...)
* Add data sheet references to meta-model (SysML...)

## Notes

* Node Red uses JavaScript and HTML for node modeling
    * A generic `Node` data type is extended with various node
      definitions provided in the Node Red codebase (hardware -
      Arduino, Raspberry Pi GPIO; protocols - MQTT, HTTP, WebSocket,
      generic TCP, UDP, etc; etc.)
    * Logic and presentation
* To do: Define a model transform methodology for interpreting Node
  Red node models as SysML diagram 'block' elements, each applying a
  'NodeRed::Node' UML stereotype
    * Is the Node Red _node_ API too heterogenous for that transform
      to provide modeling for any more speicific qualities beyond a
      generic mapping of UML elements to JavaScript objects?
* Referring to the example code:
    * File `tree/node-red/nodes/99-sample.js.demo`
        * makes reference to `tree/node-red/red/red.js` (JavaScript
          `require` reference)
        * creates JavaScript _node_ objects via
          `RED.nodes.createNode(node,def)` - refer to file
          `tree/node-red/red/nodes.js`
    * File `tree/node-red/nodes/99-sample.html.demo` and similar HTML
      files under `tree/node-red/nodes/core/`
        * Note the usage of `script type="text/x-red"`
            * Attributes on the script element: Various, non-standard
                * xpath
                  `script[@type='text/x-red' and @data-template-name]` -
                  script element defines a forms interface for
                  configuring a _node type_ defined in a corresponding
                  JavaScript `script` block located within the same
                  file. Typically, that _node type_ is denoted with
                  the value of the script element's
                  `data-template-name` attribute.
                * xpath
                  `script[@type='text/x-red' and @data-help-name]` -
                  script element defines documentation about that same
                  _node type_. Typically, that _node type_ is denoted with
                  the value of the script element's `data-help-name`
                  attribute.
            * Contents: pseudo-HTML `div` blocks containing effective
              _form input fields_ and _field label_ values (in
              `data-template-name` script elements), or HTML markup (in
              `data-help-name` script elements)
            * Usage: The HTML file provides an interface onto
              programmatic logic implemented in the correspnding
              JavaScript format node type definition file, as well as
              presentational qualities for the node type, in a node
              graph
        * Refer to `script[@type='text/javascript']` elements, whose
          contents would typically represent node type registration
          calls, namely in HTML files under
          `tree/node-red/nodes/core/`
            * Refer to those contained calls made to
              `RED.nodes.registerType(...)`, for determining node
              configuration properties (node logic and presentation)
              such as would be available for _node type_
              representation in a corresponding UML model - see, for
              example the file `tree/node-red/nodes/core/32-udp.html`
    * How do the node type definitions interact with actual network
      elements, in a node network?
        * See, for instance `setupTcpClient()` in
          `tree/node-red/nodes/core/io/31-tcpin.js`
            * Connection is to `node.host` and `node.port`
    * Flat node type schema
        * Note that the nodes type definitions do not use an API for
          class _mixin_ or _abstract_ class inheritance, thus making
          it more difficult to effectively model _node types_ for
          properties re-use
