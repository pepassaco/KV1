# KV1
A hydrofoil-based flying kayak 

**IMPORTANT**: This project is currently UNDER DEVELOPMENT and in the prototyping stage. As a result, the final deisgn has not be tested yet. Build it at your own risk. Any kind of advice, testing or collaboration will be highly appreciated :)


## Recommended guides and related projects

First things firsts. 

- Optimal Cl/Cd ratio: [video](https://www.youtube.com/watch?v=RyCcKV8puSE)
- Calculating lift in hydrofoils: [Forum discussion](https://www.boatdesign.net/threads/calculating-lift-bernoulli-forces-on-hydrofoil-for-windsurfing-board.60062/)
- List of tutorials on how to design and simulate an airfoil(/hydrofoil) in XFLR 5 from zero (in Spanish): [link 1](https://www.youtube.com/watch?v=bGubYDDyFB4), [link 2](https://www.youtube.com/watch?v=IUO3XJQxrvs), [link 3](https://www.youtube.com/watch?v=fuJba9P9ncE), [link 4](https://www.youtube.com/watch?v=owMY_eJGt3o)

## Design considerations

The design stage of this project took place under the following constraints:

- At cruising speed, no part of the hull must be touching the water
- The foils must be able to lift a person with a body mass of at least 90Kg
- The hydrodynamic lift must be greater than the weight of the paddler and the vessel for velocities as low as 3m/s
- All of the above must take place in fresh calm water at at least 15ºC

While due to their fluid-mechanical nature these are the main considerations to have into account in this stage, there are other important conditions for this project to succeed, such as the hydrofoils being relatively lightweight and resilient or being able to manufacture with enough accuracy.

## Obtaining the right airfoil shape

The very first step in this case is analysing our fluid so that we can adequately choose the optimal hydrodynamic foil shape. Assuming an average salinity of our water of 10g/Kg, at 15ºC, its kinematic viscosity will be of about 1,15e6 m^2/s: 

![](https://github.com/pepassaco/KV1/blob/main/images/kine.jpg)

Pluggin this value in the definition of Reynold's NUmber, we get Re ~ 5.2e5:

![](/images/reynolds.jpg)

Taking this value into account, it was determined that an airfoil [NACA 4412](http://airfoiltools.com/airfoil/details?airfoil=naca4412-il) resulted in one of the best candidates to be used in this project, due to both its high lift coefficient (Cl) as well as lift-drag tadio (Cl/Cd) at low Angles of Attack:

![](/images/cl_a.jpg)

![](/images/cd_a.jpg)

Moreover, it was decided that at cruising speed, the AoA of the main foil should be of 5º in order to maximize Cl/Cd. 

![](/images/ld_a.jpg)

Note however that in the transition phase from water to air, we expect the front hydrofoil to lift first, inducing an extra AoA in the main wing. Taking into accoun the geometry of a K1 (5,4m of length), this increase in the AoA can be obtained in an approximate way (it will depend on the final position in the Z axis of the foils) achieving values from 5º to 8º, leading to global AoAs of between 10º and 13º. As we can see in the plot of Cl vs AoA, these are exactly the angles that maximize lift, helping pushing the paddler upwards.

## Computing the shape and angles of the hydrofoils

The shape and angles of the hydrofoils were obtained by means of the numerical simulation software [XFLR5](https://sourceforge.net/projects/xflr5/files/). First, an approximation for the global size of the airfoils was determined in terms of the lift force we require. Then, their aspect ratios were chosen so that they are the largest possible (for minimising drag) without impacting the maneuverability of the vessel (excessively long hydrofoils can be unconfortable for paddling) and manufacturing requirements (in our particular case, the longest piece must be less than 1m long). Finally, it was time to tweek the remaining parameters: the exact position of the hydrofoils in the X axis of the vessel with respect to the center of mass, their depth or position in the Z axis, the AoA of the front foil and the shape and width of the masts that will attach the foils to the hull.

The optimization of these parameters was carried out by finding a slightly positive Momentum Coefficient (Cm) at 0º of vessel pitching that becomes 0 for low pitching angles (around 2º in this case). The physical meaning of this is that, when reaching certain threshold speed (the rotation speed) with the kayak perfectly flat, the lift generated will be enought for both lifting the bow (increasing the AoA) and lifting the paddler in the vertical axis. At 2º of pitching, the weigth forces and the lift forces will cancel out and the vessel will remain "flying":

![](/images/Resultados.png)

The final deign can be seen in the following images (the XFLR5 file is also included in the folder simulations/):

![](/images/xflr_delante.jpg)
Front hydrofoil

![](/images/xflr_detras.jpg)
Rear hydrofoil

![](/images/xflr_general.jpg)
General geometry

The airfoil chosen for the masts is a [NACA 0012](http://airfoiltools.com/airfoil/details?airfoil=n0012-il) due to its low drag properties:

![](/images/xflr_mastil.jpg)
NACA 0012 mast

And these are the final simulation results for a kayak velocity of 3,5m/s and no angle of attack:

![](/images/Resultados3D.png)

## Manufacturing and assembly

*Note:* this stage has not been finished yet.

Currently, the best approach we could ifnd for manufacturing these hydrofoils at home in a cheap and resilient way is by 3D printing. These parts will not be lightweight enough for a final build, but they can definitely serve a prototyping purpose. 

![](/images/Resultados_modeloDelantero.png)

The rear hydrofoil was splitted into four different parts (one center part, two laterals and the mast) in order to fit in a common 3D printer. Holes for joining them through aluminum rods were also inserted in the design. You can find the STL files in the models/ folder.
