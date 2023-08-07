# Caning Peg Lattices

This is a caning peg lattice. I assembled it from three parts: struts and nodes fabricated from 3/4" plywood, and caning pegs, which are commercially available tapered maple rods. Struts slide loosely into nodes and can be pinned into joints by pressing a caning peg into the gap. The joint is further secured by driving the peg in with a mallet, which can be conveniently fabricated from a strut, a node, and a caning peg. This forms a strong, stiff connection, which can be repeated to produce large honeycomb lattice sheets.

If you get one thing out of this video, I hope it is that caning peg lattices are fun to build, particularly as a group, so if your fab lab has cycles available on its CNC mill please consider devoting a few hours and a sheet of plywood to building a set. Don't forget to buy a pile of caning pegs; they're well under a buck each and you'll need two for every strut you mill. 

## Design

I started experimenting with what I call orthogonal taper pin joints in grad school a few years ago. Then, I used the joints to fabricate assembleable flexural mechanisms out of metal at a smaller scale than is shown here. I'll include a few links in the video description if you want to learn more. 

Caning peg lattices get their size and form factor from a few places. I had some left-over 3/4" plywood from building a pump house, and my 3018 Pro CNC has a fairly small working area. I wanted to be able to mill a few parts from each sub-sheet to reduce waste, although offcut volume still ended up being substantial. And while caning pegs may not be ubiquitous or locally for sale, they at least seem to be standardized and available from many vendors. All of the sources I looked at (which were only a few, to be fair) agreed that the pegs are 2 3/4", or roughly 70 millimeters long, and 7/16" or roughly 11 millimeters in diameter at the large end, tapering down to a 1/8" or roughly 3 millimeter point. 

In this particular instantiation, the nodes can accept three struts in one plane, at equal (or 120 degree) angles to one another. This means a fully dense lattice is a honeycomb point set, which is a type of hexagonal lattice that exists in a single plane. Carbon atoms can be convinced to sit this way to form layers of graphene. Here, it keeps nodes simple and means you can fill a lot of space with not a lot of plywood. Since I hope to make other lattice configurations, I call this type of node a "trinode" in the documentation. To keep things simple, and because I haven't fabricated any other node types yet, I will call them "nodes" in this video. 

These are the dimensions of the three parts. The original design files, along with fabrication outputs, are linked in the video description, but I think this shows the critical values. The key number to know when thinking about the scale of a caning peg lattice is the node-to-node spacing. It is 236 millimeters, or 9.3 inches. That means hexagons measure around 400 millimeters, or 16 inches, across their smaller width. 

Now is probably a good time to talk about optimization and math, or rather a lack thereof. While the parts and resulting joints seem simple in hand, there are a great many variables one can modify depending on which axis they wish to improve along. For example, struts could probably be thinner before they start failing or significantly deforming. I'll talk about this and other interesting rabbit holes later; for now, just know that the current design is a first iteration at this scale. 

An important detail worth mentioning at the end of the "design" section as a lead-in to the "fabrication" section is how the reliefs are milled into the ends of the struts and nodes. In the design files, both parts appear to have tapers which match the 6 degree included angle of the caning peg. To mill this perfectly, one would need a matching taper mill or a greater-than-3-axis machining setup. Of course, there are plenty of ways to approximate the the taper using standard mills; one simply must make a trade-off between resolution and machining time, and think about the orientation of the cuts they make. Here, I used a parallel tool path aligned with the strut axis, and chose a stepover which resulted in each joint having four pointed corners that I hoped would bite into the taper pins a bit. Prior experience with planar pins suggested that 6 degrees might be a bit aggressive without some deformable features to prevent the pins from sliding loose. And after playing with the lattices for a bit, this seems to bear out; each assembly process produces another set of striations in the caning peg. Time will tell whether these eventually weaken the pegs and resulting joints.

## Fabrication

I bought a car from my colleague Janet, and she included a low-cost CNC mill she purchased for a course and ended up not needing. Thanks Janet! 

The mill is a Sainsmart 3018 Pro. The 30 and 18 in the name approximate the working area of the machine: 30 by 18 centimeters, or roughly 7 by 12 inches. I built an enclosure for the machine using off-cuts and various harvested parts I had lying around, and installed an upgraded Z-axis and 300 watt spindle, also from Sainsmart. I bought a variety of mills but ended up only using a 1/4" 2-flute compression bit for these parts. Including the upgrades, tooling, and a budget for an enclosure and a cheap vacuum, you could probably put something like this together for well under $500. Were I to do it again (and have to buy or build the machine itself), I would probably opt for something with a proper wood router and a bit more build space, but it's totally feasible to work at these scales using a desktop machine like mine. I end up running the machine pretty hard to minimize cycle time, but nothing has broken after making dozens of struts and nodes. 

I used Fusion 360 to generate toolpaths for the parts. You can find the Fusion 360 archives in the links, along with the G-code I generated. If you want to use the latter without looking at the former, or if you want to do your own toolpathing, I'll go over a few details of my setup. Again, this is running my machine pretty hard; if you have a more powerful spindle, you can probably rip these parts much faster. 

First, I do a 2-d contour pass around the perimeter of the part, leaving 1.5 x 6 mm tabs at the bottom. I run the machine at 2000 millimeters per minute, or roughly 80 inches per minute, with a 2 millimeter depth per pass. The plunges and subsequent parallel passes which cut the tapers are much slower, at 50-100 millimeters per minute. The machine isn't terribly stiff and I could probably do more in the work-holding department; I compensate by running these passes slowly.

I'm using the free/personal version of Fusion 360, which among other limitations means I have to export machining operations individually. I do this, and then manually mash the G-code files together; both the individual and combined operations are in the linked repository. I use the generic GRBL (G R B L) post-processor, to which I also add a Z-lift operation to avoid dragging the mill to the program start location. Looked at from above, the zero point is at the top left location of the part. In both cases, this is an imaginary point in space due to the curved profile. Importantly, very importantly if you are just grabbing the G-code, are the axis orientations, which you can see here, and the zero point, which is at the surface of the spoil board. This makes the program automatically adapt to slightly different stock thicknesses, but means you need to zero your Z-axis before mounting the stock. 

With the current part dimensions, I can comfortably fit either 4 struts or 3 nodes on one panel cut to the size of the machine's working area. The spoil board I installed is a bit narrower than the plywood panels, which lets me secure the stock to the machine by directly bolting through drilled holes to the T-slot. I also include a strip of high-strength double-sided tape opposite the clamped holes. I've tried running more parts per panel, like say, 5 struts or 4 nodes, but my workholding method requires that I maintain a bridge of material between the two clamped sides. I also have to be careful not to tighten the wing nuts too much, but 3/4" plywood is pretty stiff so this hasn't proven to be an issue. There are plenty of ways to improve this fabrication scheme; for now, the methods I've described result in a cut time of around 9 minutes per strut or node. Perhaps as a relic of early development where I would check every part, I didn't tile the cut file; instead, I manually jog and re-home the machine between cuts. In practice, this is quite fast; I leave the enclosure closed and the mill spinning, and simply use a G0 rapid to get to the appropriate next start location. I figured out these spots mostly manually, by putting cut parts on the remaining stock and jogging the spindle to the approximate start of the next part. If you made it this far, here are the tiling jogs I used for struts and nodes, respectively.

While I show a few clips of the machining process, a note on safety. I tend to putter about the shop while the machine is running, which keeps me occupied but within earshot if I hear something is amiss. I wear earplugs and safety glasses, and make sure my first step when opening the enclosure is to vacuum out the dust. Actually, it's my third step; first, I secure the heavy lid, and second, I disconnect the spindle from its power supply, which isn't linked to the controller. I spliced a bullet connector from the RC world onto the positive lead, so this is an easy step. 

Once I've machined four struts or three nodes into a sheet, I pull the stock out, vacuum, insert new stock, and get the next parts running. Theory of constraints! Keep the heartbeat ticking. During the next operation, I depanel the parts with a sharp chisle, and use a large rasp to smooth out any remaining material. Then I hit the entire part with a coarse grit sanding pad to knock down edges and splinters, and finally use a V-bit chucked into a portable drill to add the all-important polarity mark which indicates the wider side of the machined taper (and thus, the caning peg insertion side). This full panel operation, along with prepping the next panels, fits into a single 9-minute machining cycle, so I have plenty of time to undertake unnecessary but theraputic garage organization projects. 

## Building Lattices

There is a danger inherent to fabricating things that become more interesting as you build more of them. I've been down this road a few times with various modular projects and it can be deeply satisfying, but also a bit addictive. Once you fabricate a few elements, you start to envision larger and larger collections of parts. A wise person envisions the eventual end result and plans a suitable run to match; however, even this strategy falls apart as you accomplish your initial goals and need to see more complexity. Here, I let myself be limited by the time and plywood I had to spend on the project, and a vague goal of building a lattice larger than myself. 

Caning peg lattices are a carpet toy. Or perhaps a yard toy, or a deck toy, or a floor toy. They are too large for all but the biggest of tables, but also a bit small for an environment you don't want to spend time sitting on. I suggest putting the caning pegs in a small container, so they don't roll about, and leaving the struts and nodes in a big pile. That way you (and, perhaps, a few friends) can sit near everything you need and manipulate the thing you are building as needed. 

Start by making the assembly tool. It's just a mallet, made from a strut handle, a node head, and a caning peg to hold it together. You can use another strut or node to hammer the caning peg home, or you can build two at once by banging the respective pegs against each other. Once you have a mallet, start connecting more struts and nodes using caning pegs. Hold a strut and node together, checking that polarity marks are visible on both parts, and slide a caning peg into the joint. Position your fingers behind the joint so you can keep the strut and node even with each other. Use your thumb to press the caning peg in a bit until it sticks. Use the mallet to tap the caning peg home. After a few uses you'll see marks on the pegs which tell you when they're secure; if it's a fresh joint, plan to tap the peg in until around half an inch (13 mm) is showing. These values are quite approximate; a better way is to give each joint five or so firm taps. Caning peg lattices are pretty forgiving. 

Now, build a hexagon. When you make your way around to the start, after connecting six struts to six nodes, the last joint should slip together nicely. It might not line up perfectly, so just pull it into position and secure it as you did with the others. If you like, you can tension the whole hexagon at once; to do this, assemble the parts to thumb pressure, and then tighten the joints with progressive taps. Then build more hexagons connected to this one until you have a nice lattice, or a beam, or a bunch of struts in a long line, or a big circle, or a star, or something else. 

When you are a done, if you're okay with some floor dents (see: carpet), you can flip the structure over and drop it from head height. Many of the pegs will pop loose, and you can repeat the process a few times to free up the remaining ones. Alternatively, use your mallet to gently tap the pegs free from the small side. You'll find it to be quite easy! Once you remove the pegs, the lattice will easily fall apart.

## Treasure in Rabbit Holes

Orthogonal taper pin joints are a rich area for exploration. Keeping with the video title, I will restrict this discussion to caning peg joints, noting that the peg is a crucial component whose dimensions and material could be interesting exploration axes.

Physically, the joints and lattice system could use a trip to analysis-world. It shouldn't be too hard to figure out the forces exerted 


physical
    dimensional optimization
    grooves
    fatigue
    stretching
    materials
    testing, metrology
conceptual
    other lattices
    three dimensions
    panels, tensioning
    angles, balls
    flexure
    recursion
experiential
    groups
    building challenges
    figuring out recursion
    teamwork, etc.

## Minutae

licensing
like and subscribe if you want zach working on this more