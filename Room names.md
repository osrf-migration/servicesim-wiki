The ServiceSim world contains several rooms and locations which can be specified as the place for the robot to start, for the guest to start, or a drop-off area.

***
### Target areas

According to the room, the area may be inside or in front of it.
For example, a meeting room's area is inside it, but a bathroom's area is in front of it.
All rooms have rectangular **areas** which are aligned with the world and a specific **point** inside the area where the robot or guest may start.

Room | Area | Start point
---- | ---- | 
Small meeting room | 3 x 3 m, always without obstacles | Within area, padding = 1.0 m
Large meeting room | 3 x 3 m, always without obstacles | Within area, padding = 1.0 m
Small office | 3 x 3 m, always without obstacles | Within area, padding = 1.0 m
Large office | 3 x 3 m, always without obstacles | Within area, padding = 1.0 m
Refreshment area | 3 x 3 m, always without obstacles | Within area, padding = 1.0 m
Bathroom | 3 x 1.5 m, always without obstacles, outside of room | Within area's center line
Public cubicles (island) | 3 x 3 m, includes the desk and chair | Near area's outer corner
Public cubicles (corners) | 3 x 2 m, always without obstacles | Close to area's outer edge
Front / back / private cafe areas | minimum 2.25 x 2.25 m, always without obstacles | Within area, padding = 1.0 m
Private cubicles | 1.8 x 1.5 m, always without obstacles, outside of cubicle 	Within area's center line

![idleareas_70.png](https://bitbucket.org/repo/gkR8znK/images/1314042663-idleareas_70.png)


* **red**: each target area
* **purple**: areas where there can be idling humans
* **blue**: target area's minimum point
* **green**: target area's maximum point
* **orange**: point within an area where robot or guest is spawned


***
### Service

These are the names of all rooms / areas in the world. Their locations can be acquired with:

    rosservice call /servicesim/room_info <room_name>

***
### Room names

These are the names of all the rooms. For debugging, it should be easy to click on rooms in the scene and associate them to an area name.

Areas to the left of the map are within a private area and prefixed with `Private`; the opposite goes for the areas on the right, which are `Public`.

~~~
  PublicBathroomA
  PublicCafe
  PublicMeetingRoomA
  PublicMeetingRoomB
  PublicMeetingRoomD
  PublicMeetingRoomE
  PrivateMeetingRoomA
  PrivateBathroomA
  PrivateOfficeA
  PrivateOfficeC
  PrivateOfficeD
  PublicCubicle_25_1
  PublicCubicle_25_2
  PublicCubicle_25_3
  PublicCubicle_25_4
  PublicCubicle_26_1
  PublicCubicle_26_2
  PublicCubicle_26_3
  PublicCubicle_26_4
  PublicCubicle_27
  PublicCubicle_28
  PublicCubicle_29
  PublicCubicle_30
  PrivateCubicle_31_1
  PrivateCubicle_31_2
  PrivateCubicle_31_3
  PrivateCubicle_31_4
  PrivateCubicle_31_5
  PrivateCubicle_31_6
  PrivateCubicle_31_7
  PrivateCubicle_31_8
  PrivateCubicle_32_1
  PrivateCubicle_32_2
  PrivateCubicle_32_3
  PrivateCubicle_32_4
  PrivateCubicle_32_5
  PrivateCubicle_32_6
  PrivateCubicle_32_7
  PrivateCubicle_32_8
  PrivateCubicle_33_1
  PrivateCubicle_33_2
  PrivateCubicle_33_3
  PrivateCubicle_33_4
  PrivateCubicle_33_5
  PrivateCubicle_33_6
  PrivateCubicle_33_7
  PrivateCubicle_33_8
  PrivateCubicle_34_1
  PrivateCubicle_34_2
  PrivateCubicle_34_3
  PrivateCubicle_34_4
  PrivateCubicle_34_5
  PrivateCubicle_34_6
  PrivateCubicle_35_1
  PrivateCubicle_35_2
  PrivateCubicle_35_3
  PrivateCubicle_35_4
  PrivateCubicle_35_5
  PrivateCubicle_35_6
  PrivateCubicle_36_1
  PrivateCubicle_36_2
  PrivateCubicle_36_3
  PrivateCubicle_36_4
  PrivateCubicle_36_5
  PrivateCubicle_36_6
  PrivateCafe
  BackEntrance
  FrontElevator
  FrontCouchA
  FrontCouchB
~~~