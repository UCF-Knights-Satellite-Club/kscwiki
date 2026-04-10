---
description: Details about the mechanical components of T-Sat-0.
---

# Hardware

## Overview

Our mechanical team worked on and iterated design using [OnShape](https://www.onshape.com/en/education/?utm_source=google\&utm_medium=cpc\&utm_campaign=Google_Pmax_NA\&utm_term=\&gad_source=1\&gad_campaignid=22457087470\&gbraid=0AAAAADgbnFnJ2gjElhw0XxAXQ2uHtQ79d\&gclid=Cj0KCQjwjJrCBhCXARIsAI5x66V6pDaH6F1gWIh6D9jksSAQk-fOqibjErFxy45Ss0BbCcIrh9YbisMaAndeEALw_wcB) as our CAD platform. The team developed two major components; [1U Housing Panels](hardware.md#id-1u-housing-side-panels) and the[ Parachute Deployment System (PDS)](hardware.md#parachute-deployment-system-pds). As a low cost and easy prototyping option we used 3D printing as our means of manufacturing utilizing PETG filament. This gave us freedom while iterating and helped our relatively inexperienced team at multiple points as changes were made on the fly during testing or other points during development. The mechanical team was also responsible for the [Launch Hardware](hardware.md#launch-hardware) needed on launch day .



## 1U Housing Panels

The housing used for T-Sat-0 was a[ Universal 1U](https://www.thingiverse.com/thing:4096437) (10x10x10 cm) found on Thingiverse. It was printed in PETG and contained slots for M3 nuts and bolts for attaching each panel.

<figure><img src="../../../.gitbook/assets/Full Structure (1) (1).png" alt="" width="375"><figcaption><p>Isometric view of the Universal 1U structure</p></figcaption></figure>

Each of our panels was specifically designed to be mounted to our housing with its pre-dimensioned through holes as listed on the drawing on the housing page on Thingiverse.&#x20;

<div align="center"><figure><img src="../../../.gitbook/assets/image (9).png" alt="" width="219"><figcaption><p>Top and bottom panel drawing </p></figcaption></figure> <figure><img src="../../../.gitbook/assets/image (6) (1).png" alt="" width="242"><figcaption><p>Side panel drawing, consistent for all four sides</p></figcaption></figure></div>

Fitting a canister large enough to contain a [24 inch nylon parachute](https://www.amazon.com/Estes-Nylon-Parachutes-Pro-Model/dp/B0071NXTCK/ref=asc_df_B0071NXTCK?mcid=cb63d1c12fbf3325ac6a0025d2efe662\&hvocijid=1387236039281515915-B0071NXTCK-\&hvexpln=73\&tag=hyprod-20\&linkCode=df0\&hvadid=721245378154\&hvpos=\&hvnetw=g\&hvrand=1387236039281515915\&hvpone=\&hvptwo=\&hvqmt=\&hvdev=c\&hvdvcmdl=\&hvlocint=\&hvlocphy=9057291\&hvtargid=pla-2281435179058\&psc=1) with a spring release mechanism in a 1U was one of the largest challenges for our team. This was the point that took the most revising and testing as initial prototypes where nearly twice the size of what would be our final hardware. We also had added requirements of securing a [3.7 volt 3 Ah LiPo battery](https://www.digikey.com/en/products/detail/mikroelektronika/MIKROE-4474/13679437?gad_source=1\&gad_campaignid=20243136172\&gbraid=0AAAAADrbLlgT-Bx2bEEux3I84RPcshTUt\&gclid=Cj0KCQjw0qTCBhCmARIsAAj8C4Zn-9abPx8C8oLW5JSKpuo_IiaJdKqwvTlXjQuw4Z39Qsn35Mz2GZYaAiPiEALw_wcB\&gclsrc=aw.ds), a [Arducam Mega 5MP SPI](https://www.digikey.com/en/products/detail/arducam/B0401/19116501?gad_source=1\&gad_campaignid=20232005509\&gbraid=0AAAAADrbLliEnLAkF7qAveyxn_iOWR-L2\&gclid=Cj0KCQjw0qTCBhCmARIsAAj8C4aWq8Wq-fkCzX5ZIKzm6ne_GKkCGVl-ikIGEEK_8w9Ez0h2zS9acJkaAssJEALw_wcB\&gclsrc=aw.ds), and various other access points for when T-Sat is assembled. In order to contain the required components within the housing we had to store all hardware besides our PCB within the side panels.&#x20;

### Servo Panel

This panel was the only one on the CubeSat that didn't have any mounting or access requirements which made it the best candidate for us to list our club sponsors.&#x20;

<div align="center" data-full-width="false"><figure><img src="../../../.gitbook/assets/Servo Panel.png" alt="" width="375"><figcaption><p>Front of servo panel for T-Sat-0</p></figcaption></figure></div>

### Access Panel

A critical component for any flight ready CubeSat is a remove before flight pin to avoid battery drain while the CubeSat is assembled and awaiting launch. For T-Sat we aligned the pin height with our power switch on the PCB so we could easily cutoff power while assembled. The front of the panel also contained a raised ledge that allowed the team to insert the pin and twist it clockwise to lock it in place and prevent the pin from accidently being removed. This was an element that was added after the first assembly, were we found that the remove before flight pin could easily fall out while being handled. The panel also has two rectangle holes that function as access to our ESP32's micro USB header and our micro SD card. These elements were also additions to the panel so we could avoid unneeded removal of the panel. Both of which were vital for analyzing the data collected and making software changes while testing T-Sat while it was assembled.&#x20;

<div align="center" data-full-width="true"><figure><img src="../../../.gitbook/assets/Blank Side Panel I.png" alt="" width="375"><figcaption><p>Front of access panel for T-Sat-0</p></figcaption></figure></div>

### Battery Panel

To securely store our battery while having easy access to remove it for charging we added space for x4 3mm heat pressed threaded inserts that were used to bolt a back plate to the panel. At the bottom of left corner of the raised battery compartment we added a cutout for the battery cable to run to our PCB.

<div align="left"><figure><img src="../../../.gitbook/assets/Battery Panel I.png" alt="" width="375"><figcaption><p>Front of battery panel for T-Sat-0</p></figcaption></figure> <figure><img src="../../../.gitbook/assets/Battery Panel I (1) (1).png" alt="" width="375"><figcaption><p>Rear of panel</p></figcaption></figure></div>

### Camera Panel

The Arducam was secured with a back plate that was taped to the panel itself and a pass through for the camera cable that runs to the PCB. The team originally had hopes of a back plate that slotted and clipped into place similar to a TV remote. There were multiple iterations made with this idea in mind but we found that thin walls and 3D printing of the components made the objective challenging. We ran into many issues with reliability of the design and the overall printability. This panel and the method for securing the camera is a priority for improvements to be made on T-Sat-1.



<div><figure><img src="../../../.gitbook/assets/Camera Panel I (3).png" alt="" width="375"><figcaption><p>Front of camera panel for T-Sat-0</p></figcaption></figure> <figure><img src="../../../.gitbook/assets/Camera Panel (2).png" alt="" width="375"><figcaption><p>Rear of panel</p></figcaption></figure></div>

### Top Panel

The top panel contained four loops on the corners of the panel for the tether to attach to T-Sat and run to the burn wire. Ultimately, the team found that it was best to only use two loops with [#18 braided nylon](https://www.amazon.com/Romeda-Construction-Gardening-Braided-Masonry/dp/B0D2K7RHR5?ref_=pd_ci_mcx_mh_pe_im_d1_hxwPPE_sspa_dk_det_cav_p_11_2\&pd_rd_i=B0D2K7RHR5\&pd_rd_w=thncR\&content-id=amzn1.sym.57b80066-10e8-4be7-a5f2-ce3f1faa4959\&pf_rd_p=57b80066-10e8-4be7-a5f2-ce3f1faa4959\&pf_rd_r=Q3F7SKSMM5YVYR5YEBS8\&pd_rd_wg=5kU0R\&pd_rd_r=bc37c5ec-d1c4-4b6a-b0cd-4aca939d94ee\&th=1) tied between them with enough slack that the nylon would fall to the side and avoid blocking the PDS. The PDS was also mounted alongside the top panel using two of the corner bolt holes and nuts on the inside of the structure. This panel undertook few iterations as its requirements were very straightforward. One of which was adding fillets to the base of each loop to increase their tensile loading abilities.

<figure><img src="../../../.gitbook/assets/Top Panel (1) (1).png" alt="" width="375"><figcaption><p>Isometric view of top panel for T-Sat-0</p></figcaption></figure>

### Bottom Panel

The bottom panel functioned as protection for the pins of the breakout boards that were soldered to the PCB. It was mounted using the holes on two of the side panels with bolts that went through both. The four through holes on the panel were additions to the original design as we overlooked the need for clearance of the M2 Nylon PCB mounting screws.&#x20;

<figure><img src="../../../.gitbook/assets/Bottom Panel.png" alt="" width="375"><figcaption><p>Isometric view of bottom panel for T-Sat-0</p></figcaption></figure>

## Parachute Deployment System (PDS)

T-Sat-0's Parachute Deployment System functioned with the combination of five 3D printed components shown in the exploded view below. The additional hardware used in the PDS was a [23/32" x 3.5" compression spring](https://www.amazon.com/dp/B008RG54YG?ref_=ppx_hzsearch_conn_dt_b_fed_asin_title_2) and two separate M3 bolts that ran through the base and cap of the PDS to secure the spring to the canister. The system had to be printed as separate components in order for us to secure the spring in the canister. For the assembly of the canister we used both epoxy and plastic welding and neither created issues in our testing.

<figure><img src="../../../.gitbook/assets/Assembly 1 (2).png" alt="" width="375"><figcaption><p>PDS exploded view</p></figcaption></figure>

The PDS undertook countless revisions through many phases of testing. This is where 3D printing thrived as we had the flexibility to make substantial changes and compare multiple designs. It also allowed the team to perform drop tests without worries of damaging flight hardware as we were capable of printing several backups for critical parts that would often break during failed drop tests. This was one of our biggest lessons from the project, as trying to save a few dollars at times by purchasing a single electronic component or printing one of each panel caused a ton of delays during testing and even problems the night before our launch.&#x20;

<figure><img src="../../../.gitbook/assets/Assembly 1.png" alt="" width="375"><figcaption><p>Isometric view of final PDS with servo linkage</p></figcaption></figure>

The final design came from a culmination of improvements that we found were needed from testing. At the top of the canister, the two mounting arms were a common weak point if the parachute deployment failed as they would consistently snap with an upside down impact. After a couple of failures we added gussets to the bottom side of each arm which eliminated the issue. Another problem was the cap/plate that pushed the parachute would occasionally get stuck on the corner of the guide when it was rotated. This was fixed with a fillet on the corners to prevent it from binding as the spring pushed if it wasn't fully aligned with the vertical part of the guide.&#x20;

An adjacent problem to the system was the 9g micro servo we were initially using was undersized  and was also being limited by the 3.7 volts we were supplying.  We found that the 9g micro servo was only consistent if the battery was at or near peak voltage. We installed a 21g micro servo that worked without failure that we are going to use on T-Sat-1 as well. The last key issue is the servo linkage being used to rotate the plate for parachute deployment. The main problem with the linkage is the use of bolts to pivot the two links as the nuts backout after a few tests. This linkage was flown on T-Sat-0 but was the teams main point of concern and was carefully tightened before launch. Too loose and the nuts could back out and too tight and the linkage wouldn't pivot as it was needed to in order to pull at the right angle. In the end, significant testing got us to a place we were comfortable with as we were able to revise what was needed and account for potentially points of failure on launch day.&#x20;

&#x20;

{% embed url="https://www.youtube.com/watch?list=TLGG1nj_474P79oxMTA2MjAyNQ&t=3s&v=kfxf41nOwfE" %}

## Launch Hardware

T-Sat-0 was flown with a 600g weather balloon filled with a 125 cubic foot tank using helium as our lifting gas. To tether the payload a forty five pound plate was used with the [#18 braided nylon](https://www.amazon.com/Romeda-Construction-Gardening-Braided-Masonry/dp/B0D2K7RHR5?ref_=pd_ci_mcx_mh_pe_im_d1_hxwPPE_sspa_dk_det_cav_p_11_2\&pd_rd_i=B0D2K7RHR5\&pd_rd_w=thncR\&content-id=amzn1.sym.57b80066-10e8-4be7-a5f2-ce3f1faa4959\&pf_rd_p=57b80066-10e8-4be7-a5f2-ce3f1faa4959\&pf_rd_r=Q3F7SKSMM5YVYR5YEBS8\&pd_rd_wg=5kU0R\&pd_rd_r=bc37c5ec-d1c4-4b6a-b0cd-4aca939d94ee\&th=1) ran through a hole in the center of the plate. A 360 degree swivel with two carabiners on either side was used to rig T-Sat to the 500ft nylon tether. For future flights 3D printed or other non-metal alternative carabiners will be used to reduce the volume of lifting gas needed. As generating enough lift with the harsh winds on launch day was a challenge and the excessive size and weight of the metal carabiners utilized more of our lifting capabilities than what was required.&#x20;

<div data-full-width="false"><figure><img src="../../../.gitbook/assets/image (5) (1).png" alt=""><figcaption><p>T-Sat-0 being lifted simultaneously with another clubs payload. The parachute deployed prematurely due to acceleration readings that triggered our <a href="./#software">freefall detection</a> threshold.</p></figcaption></figure></div>

Another key component within the rigging was a 3D printed stabilizer that can be seen in the image above. This was necessary as we were flying another payload belonging to another club and wanted to avoid tangling.&#x20;

With 3D-printing being our means of manufacturing. Our mechanical team decided on using PLA filament, as it is a budget-friendly prototyping option. Allowing there to be a bit of leniency when it came to adjusting any errors that showed up, such as incorrect measurements or mishaps in the design process. With PLA filament also gives us the ability to create spare parts as needed. Even so, PLA did have its downsides when it came to the rigidity and durability of the prints. In which our mechanical team took notice and decided to change to a PETG filament, relieving such problems. In turn, making our final material of choosing to be PETG.

<figure><img src="../../../.gitbook/assets/image (11).png" alt=""><figcaption><p>Flight Day Final Assembly</p></figcaption></figure>

