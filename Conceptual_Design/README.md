The Thrust_to_Weight workbook is based on equations from <a href="https://books.google.com/books?id=XtU4HVnWeZIC&pg=PA57&lpg=PA57&dq=MS+Dos+program+for+airplane+Performance+Assessment&source=bl&ots=CgCfVzvNZP&sig=ACfU3U1OXvFW83ZYDGyV1CxHTV9blSkmkA&hl=en&sa=X&ved=2ahUKEwjDlZrS07fkAhXVIDQIHVCnB-QQ6AEwDXoECAgQAQ#v=onepage&q=MS%20Dos%20program%20for%20airplane%20Performance%20Assessment&f=false"></a></li><u>General Aircraft Design: Applied Methods and Procedures</u></a> Chapter 3 Constraint Analysis and Example 3-1 on Page 64, ref 1 above.  Equations in this chapter relate the thrust loading, thrust to weight ratio (T/W or tw for ease of use with Python) of an aircraft, to its wing loading, weight to reference surface area ratio (W/S or ws for ease of use with Python) at several critical (from a conceptual design standpoint) stages of flight.  I have rearranged the equations in the order they would take place in a normal flight to make it easier for me to keep track. the stages are:
<li>Takeoff T/W</li>
<li>Climb T/W</li>
<li>Cruise T/W</li>
<li>Maneuver (level constant velocity turns) T/W</li>
<li>Service Ceiling (at Rate of Climb = 100 fpm or 0.508 m/s) T/W</li>

I am a beginning Python programmer.  I wrote this python code initially to see if I could solve example 3-1 in reference 1 using Python.  I believe the code produces results similar to the equations given in the reference, but being neigher a professional programmer, nor an aeronautical engineer, I assume no liability for any use of this code, as the MIT License states.

Inputs are given in section 2, Airplane Reguirements.  
Outputs are printed or plotted in section 4. 

Future: I plan to add a capability to write the output data from this notebook to a disk file, but haven't done so yet.

# The Problem

One of the problems encountered at the conceptual or even the preliminary design stage is that the geometry of the aircraft is mostly unknown.  As a result, the designer can only estimate some basic values needed for the aircraft design calculations such as  estimated minimum drag coefficient $C_{Dmin}$, Drag Coefficient at lift off $C_{Drot}$, or Lift Coefficient at lift off $C_{Lrot}$ , and the Lift induced drag constant $k$. However, we can estimate these quantities by looking to existing aircraft of the same class as those being designed.

In the following sections, I have separated each section of code by a markup cell containing a header, and possibly some comments about the code that follows to enable the NBextensions Table of Contents to build an TOC for the notebook.

In Section 2, we will document our aircraft requirements and define our assumptions about the characteristics of our aircraft, first in a Markdown cell, then in a Code cell as Python variables.  Following that code cell will be one that allows us to select a test case for detail analysis. 

In Section 3, the first subsection defines the common variables and establishes a range of wing loading (ws) between 2 and 58 Lb per sq ft for our analysis. This W/S range can be changed in the code below, but is generally applicable to most LSA, Normal Category personal, and experimental aircraft, LSA aircraft and potentially small business jets. The following sections contain the python version of the equations for each flight stage listed above, followed by a print cell and a plot cell I used for debugging and left as they might be useful to others using the code.  The print and plot debug sections are all commented out.

Note: ref 1, example 3-1 was set up at wing loading (W/S) of 10 lbs / sqft, so I have the initial test case set to extract this value from the W/S and T/W arrays so we can compare the results with the example to verify the coding of the equations.  I have also included print and plot statements so each individual calculation can be debugged individually.  Generally, these cells would not be executed while working through the conceptual test cases.  

The test case cell can be executed without rerunning the array computataions.  The only thing this cell does is all the user to pick a single W/S and consequently T/W from the arrays.  The Individual Case code would have to be reexecuted in order to pull different test cases from the arrays.

# Solution:

Section 4, Using the arrays (data) generated in section 3, we can plot all the thrust loading vs the wing loading for all the computed situations, takeoff run, climb, sustained turns, and service ceiling, for our particular requirements. The TW values are then converted to horsepower (BHP) so we can find an appropriate engine.  The BHP vs ws is then plotted.  Since piston and turboprop engines loose power at higher altitudes, we have to take the horsepower we computed and increase it back to sea level for those stages whose altituce was above sea level.  This is the BHP - SL vs ws Plot (dia 3)

Finally, we select what we estimate is the highest horsepower in the BHP-SL vs ws curves and change the test_case value to that to allow us to print our selected values for each flight condition.  (the test_case value is changed in the second code cell at the top of the Notebook.)  The arrays don't have to be rerun when we change out test_case value, just the print statements in section 4.1.  

Note: the maximum horsepower given is not necessarily the horsepower in the final airplane design, only a starting point.  See the example of this notebook applied to a Cessna 172 

The Thrust_to_Weight notebook computes the required engine horsepower for various wing loadings. Given the maximum takeoff weigth. wing loading and aspect ratio selected for the individual aircraft, the notebook computes (in section 4.2) the <b>Stall Speed</b>, <b>CLmax</b>, <b>wing span</b>, and <b>wing reference area</b> required for this aircraft.</li>

<li>Subfolder "Examples"</li>
        <ul><li>Thrust_to_Weight_GA_172 -- Change the aircraft requirements to reflect a General Aviation (GA) Cessna 172 type aircraft</li>
            <li>Thrust_to_Weight_LSA -- Change the aircraft requirements to reflect a Light Sport Aircraft(LSA)</li></ul>