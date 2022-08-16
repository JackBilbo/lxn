# Nav rework for MSFS gliders

Basic Features

All Information is organized in „pages“ (horizontally) and „sub-pages“ (vertically). Pages can be changed by „click and drag“ with the mouse or - more comfortably - through keybinding „transponder(100)“ for horizontal and transponder (1) for vertical scrolling. 

Currently there are five main pages: „APT“ for navigation to the selected Airport, „WPT“ for navigating a task/flightplan, „TASK“ for the current state of the task, "Kinetic Assitant" for launching throug KA and „CONFIG“, which is currently only used to switch units between metric and imperial and for a read-only view of weight & balance.

„APT“ Page automatically selects the nearest Airport as target. On the second subpage „below“ Airport overview there is a list of close airports where you can click any airport to select it for navigation.

„APT“ and „WPT“ feature a maximum of 16 data fields each that can be configured in game. The „tools“ button in the upper right corner of the map toggles „configuration mode“. Data fields are then marked with a light blue outline. Click any data field to bring up a popup, where you can set background color, text color and Information to be displayed. A second background color can be selected to be displayed when the displayed value <= 0 (e.g. switch background to red when arrival height is negative)

Data field Configurations are persistent between simulator sessions. Click „reset all“ in the configuration popup to reset all data fields to default.

The task management system is a clone of Ian „B21“ Lewis’ Soaring Engine in the AS33. Some features like calculating glide ratios could not be recreated, as they are dependent of other instruments in the AS33. 

The wind indicator in the center of the map is loosely based on the LX-„Hawk“ system displaying current (blue) and average (grey) wind-arrows and a green/red column indicator for the vertical wind component.


Known Limitations: 

- Knobs and buttons in the cockpit do not directly interact with the Nav screen, as they are configured in the model XML and that’s beyond my scope.

- Airport navigation currently lacks information on airport elevation. Still trying to get this info out of MSFS.

- The map can not be panned. To avoid collision with „click and drag“ page changing another „mode switch“ would be needed. Considering the current quality of the ingame map, I don’t think it’s worth the added complexity. 

- „Thermalling help“ through the typical green and red dots is a very basic „quick and dirty“ implementation

 

 

Developers:

The front end is intended to be easily extensible with new features. New pages and sub-pages can be added by simply copy/pasting the respective HTML-Structures.

All variables that are displayed in the frontend are stored in the „this.vars“-object. This object contains the value itself as well as unit- and label-information and make the variable user-selectable in the in game configuration popup. To add a new readout to your panel all you have to do is add a line to the „this.vars“-object with your own variable name and label/unit information. When you start the next flight, you can simply assign your variable value to a data field of your choice and if the variable value is manipulated somewhere in the javascript, the cockpit readout will be updated automatically.

If you need a variable displayed somewhere outside of the data fields, you can do so directly in the html using the attributes  class=“livedata“ data-value=„VARIABLE“. See the ballast readout in the weight & balance configuration as an example.

Units: All variables are kept in a „base unit“, which is (currently) „imperial“ units. When displayed in a data field or as „livedata“ in the html the value is converted to the user preferred unit. So if you like to display a distance you should store nautical miles in the variable and conversion will be automatic

 

