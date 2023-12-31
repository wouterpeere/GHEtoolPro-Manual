.. _eed data:

How to convert EED data to GHEtool?
###################################
Earth Energy Designer (or EED in short) is the first and most used geothermal sizing software in Europe, so it can happen
that your competitor or client is working with this software instead of GHEtool. Although the features of EED differ (quite a lot)
from those of GHEtool (see also `are FAQ <https://ghetool.eu/faq/>`_), it is possible to convert an EED
project to a GHEtool project. The only thing you need to ask for is the EED data export file. An example can be found here :download:`this one <Figures/EED_example.txt>`.
In this article we will go over the different conversion steps if you want to work on an EED project within GHEtool.
A discussion on the difference in results, can be found in this FAQ: :ref:`eed comparison`.

.. note::
    Currently, a method to load EED data directly into GHEtool is in development. For the time being however,
    some manual input is required.

Input values
=============
To input the values from the EED export file into GHEtool, it is best to read the document from top to bottom, so
you don't miss any information. The different sections that appear in the EED export file are mentioned in order below.

.. caution::
    Please select the 'Determine temperature profile' aim in the :ref:`tab aim` tab. The other methods are not relevant
    if you want to enter a EED project into GHEtool.

Ground
------
The first piece of data you come across in the export, is the ground data. This can be set in GHEtool in the :ref:`tab earth` tab.

.. image:: Figures/EED_ground.png
  :alt: Ground data in the EED export file

* **Ground thermal conductivity** This can be directly set in GHEtool.
* **Ground heat capacity** This can be directly set in GHEtool.
* **Ground surface temperature** If you select *custom*, you can set the surface temperature.
* **Geothermal heat flux** If you select *flux*, you can set the geothermal heat flux.

The result in GHEtool looks like this:

.. image:: Figures/GHEtool_earth.png
  :alt: Ground data set in GHEtool

Borehole
--------
The next section you see, is related to the borehole internals and configuration. First, we will input the borefield data
in the :ref:`tab borefield` tab.

.. image:: Figures/EED_borehole.png
  :alt: Borehole data within the EED export file

* **Configuration** This tells you something about the borefield configuration. In this case, we have a borefield with 1 borehole in the width
  direction and 10 in the length direction. You can set this directly in GHEtool.
* **Borehole depth** You can set this directly in GHEtool.

.. note::
    If you don't see the borehole depth, please select 'Determine temperature profile' in the :ref:`tab aim` tab.

* **Borehole spacing** You can set this directly in GHEtool.

.. caution::
    EED works with a limited number of possible borefields, with **equal spacing** in both length and width direction.
    The borehole spacing you find in the EED export should therefore always be used for both spacings within GHEtool.

* **Borehole diameter** In GHEtool you need to set the borehole radius, so you need to divide this diameter by 2.

If you do so, you get the result below:

.. image:: Figures/GHEtool_borefield.png
  :alt: Borefield data set in GHEtool

.. note::
    EED does not have a parameter for the *buried depth*. This can lead to some (minor) variation
    in the result, since the buried depth is used to estimate the heat losses to the earths surface.
    A detailed discussion can be found in this FAQ: :ref:`eed comparison`.


Next, you open the :ref:`tab thermal resistance` tab.
If you don't see the possibility to enter the borehole internals here, you need to set the borehole thermal resistance to *dynamic*
in the :ref:`tab options` tab like explained here: :ref:`borehole internals`.

* **Borehole installation** This can be directly set in GHEtool using the toggle button *Borehole internals* and the *Number of pipes [-]* input.
* **U-pipe diameter** GHEtool requires a pipe radius, so you need to divides this value by 2 to get the *outer pipe radius*.
* **U-pipe thickness** GHEtool works with inner and outer radii, so you can get the *inner pipe radius* by substracting the pipe thickness from the outer pipe radius.
* **U-pipe thermal conductivity** This can directly be set in GHEtool.
* **U-pipe shank spacing** GHEtool works with a pipe distance from the center. This is simply half of the shank spacing.
* **Filling thermal conductivity** This can be set in GHEtool as the *grout thermal conductivity*.
* **Contact resistance pipe/filling** This is not an input parameter in the GHEtool pipe model.

.. note::
    The pipe roughness is not an input parameter within EED, but it is used to determine accurately the boundary
    between laminar and turbulent flow. Just set it to a very small number (like 10^-6m for a smooth pipe)
    in order to get the same results as in EED.

This gives you the following result:

.. image:: Figures/GHEtool_pipe.png
  :alt: Pipe data set in GHEtool

Thermal resistances
-------------------
This section contains some background information about the calculation method within EED.
This is irrelevant for GHEtool, so this paragraph can be ignored.

.. image:: Figures/EED_thermal_resistance.png
  :alt: Thermal resistance data within the EED export file

Heat carrier fluid
------------------
The following section contains the fluid properties. Therefore, you open once again the :ref:`tab thermal resistance` tab.

.. image:: Figures/EED_HCF.png
  :alt: Heat carrier fluid data within the EED export file

First you need to select *custom* in the *fluid properties* option.

.. note::
    Note that most likely the values in the EED export correspond to a specific glycol %, which itself is not exported. It can
    be of interest to ask for this explicitly, since EED uses most often negative temperature as a references for the fluid properties.
    As discussed here: :ref:`fluid parameters`, this value has a big influence on the final result. If you simply
    want to compare EED with GHEtool, you can leave this note for what it is.

* **Thermal conductivity** This can be directly set in GHEtool.
* **Specific heat capacity** This can be directly set in GHEtool.
* **Density** This can be directly set in GHEtool.
* **Viscosity** This can be directly set in GHEtool ([kg/(m s)] is the same unit as [Pa s].
* **Freezing point** This is not needed in GHEtool.
* **Flow rate per borehole** In GHEtool, a mass flow rate is used, so you need to convert the flow rate in l/s to a flow rate
  in kg/s. Therefore you multiply the *flow rate* from EED with the density and divide that by 1000.

You get the following result:

.. image:: Figures/GHEtool_HCF.png
  :alt: HCF data in GHEtool

Load
----
As the last step, you need to input the load values from EED into GHEtool. Therefore you open the :ref:`tab thermal demand` tab.

.. image:: Figures/EED_load.png
  :alt: Load data within the EED export file

.. caution::
    Please set the *Load type* to *Building* when you use inputs from EED.

* **Annual DHW load** This can be set if you select to include domestic hot water.
* **Annual heating load (DHW excluded)** This is not needed in GHEtool.
* **Annual cooling load** This is not needed in GHEtool.
* **Seasonal performance factor (DHW)** This can be set as *SCOP DHW* in GHEtool.
* **Seasonal performance factor (heating)** This can be set as *SCOP* in GHEtool.
* **Seasonal performance factor (cooling)** This can be set as *SEER* in GHEtool.

.. note::
    Note that the SEER in GHEtool is limited to 1000, since there is always a primary pump working to circulate the fluid
    across the borefield which is consuming electricity. The difference between 1000 or 10000 has not a big impact on the final result.

For the heating and cooling loads, you need to use the *Heat load* and *Cool load* data from the first table.

.. caution::
    Note that you need to multiply these values by 1000 since they are given in MWh in EED and you need to input them in kWh in GHEtool.

For the heating and cooling peaks, you use the values in the second table in the *Peak heat* and *Peak cool* column.

You get this result in GHEtool:

.. image:: Figures/GHEtool_load_type.png
  :alt: SCOP data in GHEtool

.. image:: Figures/GHEtool_load.png
  :alt: load data in GHEtool

Next, we need to set the peak durations. Therefore, we go to the :ref:`tab earth` tab.
Here you can set a single peak duration for both heating and cooling instead of a value per month.
Simply enter the longest duration of EED for both heating and cooling in GHEtool and you're good to go.

.. note::
    GHEtool uses a model that works with a single peak duration for all months. By using just a single peak duration for
    all months, the final feasibility (or the most critical temperature) of the geothermal system will not change, since the most critical month will stay the same.
    In order to speed up the calculation, GHEtool therefore only uses one peak duration for both heating and cooling.

The *simulation period* can also be set in this tab.
The result looks like this:

.. image:: Figures/GHEtool_duration.png
  :alt: Peak duration data in GHEtool

.. note::
    Note that GHEtool always start calculating in the first month of the year. If you have another month than January,
    for now, you need to change the order of the months yourself.

.. admonition:: Congratulations

    Congratulations, you have now successfully entered the EED project in GHEtool!
    When you press calculate, you can see that the results show some differences w.r.t. EED that can be explained
    by the difference in models used within EED/GHEtool. In this FAQ (:ref:`eed comparison`) we will go more into depth in these differences.
    The converted document can be downloaded :download:`here <Figures/GHEtool_example.GHEtool>`.
