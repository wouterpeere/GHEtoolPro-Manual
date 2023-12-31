.. _tab aim:

Aim
###

In this tab the user can define what he or she is going to be calculating in this specific scenario.

Determine temperature profile
*****************************
This is the most basic and widely used functionality within GHEtool. If you have a certain (geothermal) heating and cooling demand given
and you select a specific borefield design (including the borehole depth), this aim will give you the temperature profile back.
It can be used with both a monthly load profile and an hourly load profile (see also :ref:`tab thermal demand`).

.. note::
If you want to use an hourly profile with this aim, you need to set the software to use the hourly profile under the tab :ref:`tab options`.

Determine required depth
************************
If you have a certain (hourly) load profile given even as the borefield configuration, this method calculates the required borehole depth
so that the load can be achieved by the borefield. There are three different methods implemented for this calculation, which are explained
in depth here: :ref:`sizing methods`.

.. include:: ../General/warning_required_depth.rst

Optimise load profile
*********************
Most of the times, it is economically unattractive to put 100% of your load onto a geothermal borefield, either due to high peak loads or a large imbalance.
In that case, you want to hybridise your system, but which part of the load can be put onto the borefield?
This methodology will give you back how many percentage of the heating and cooling can be full-filled geothermally and how
many peak heating/cooling has to be full-filled with another solution.

.. note::
    Since this method uses the load-duration curve of the thermal demand profile in the background,
    this method only works when **an hourly load profile** is used.
    If this is not set in the tab :ref:`tab thermal demand`, the interface disables further actions.

.. note::
    This method currently does not allow a DHW load on top of the hourly load.
    Please include your DHW load into the hourly profile if you want to take it into account.

.. note::
    This method uses a monthly based temperature calculation in the background in order to speed op the algorithm.
    However, where the monthly method in the 'determine required depth' method converges based on an absolute or relative
    difference in calculated depth between two iterations, this method converges based on a temperature difference between the average
    fluid temperature and the respective limit.

    This small difference in the background, can lead to a small difference in result between the 'calculate required depth' and 'optimise
    load profile' methods. If you have a certain borefield of 150m deep which can cope with 100% of the building load, using the method 'calculate
    required depth' can give you back a depth that differs from 150m. This is due to the difference in convergence criteria, but is will always be very small.
