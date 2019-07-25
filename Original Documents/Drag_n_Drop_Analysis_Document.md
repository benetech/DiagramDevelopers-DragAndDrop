# Introduction
The notes collected in this document complement other documents developed by the DIAGRAM Developers' Drag and Drop Sub-Committee. Herein, we discuss the accessibility of drag and drop interactions in general terms, distinguish different types of drag and drop interactions which are germane to accessibility, and examine their implications. Educational applications are the focus of this effort, but, due to the nature of the subject-matter, the findings of the analysis are more generally applicable.

These notes should be read in combination with the examples collected in the [accompanying spreadsheet](https://docs.google.com/spreadsheets/d/1GJ-CTczylYjjt-fWB7J8dea6sjm17E4sbkFWsa6dXxo/edit#gid=0).

# Classifying Drag and Drop Interactions
Drag and drop interaction is an instance of direct manipulation: the user moves an on-screen object from a source (starting position) to a destination (final position). This operation can be performed by the user directly if a pointing device or touch input can be controlled with sufficient precision to allow both the source (hence the object to be operated upon) and the destination to be specified. The source, destination and object are typically displayed visually, but auditory or tactile output can also be provided, thus making the interaction non-visually accessible.

## Examples of Accessible Approaches to Drag and Drop
* Drag and drop interaction with a mouse or touch screen, coordinated with a visual display.
* Drag and drop interaction with speech output (e.g., reading the objects encountered as the user finds the source location, the objects passed over as the object moves, and the destination). This can be effectively implemented on a touch screen.
* Drag and drop interaction on a dynamic tactile graphics display, with touch or mouse input and tactile output. (It isn't clear whether this has actually been implemented. The tactile displays developed in the [HyperBraille Project](http://www.hyperbraille.de/?lang=en) should be capable of it, as should be the [Graphiti display device](http://www.orbitresearch.com/graphiti.php) currently under development by Orbit Research and the American Printing House for the blind.)

## Enhancing Visual Drag and Drop Interactions

Users who encounter difficulty with fine motor control or who have a vision impairment that makes small objects difficult to distinguish without enlargement can be expected to benefit from constraints on the minimum visual size of sources and destinations. For further details, see the "target size" proposal which is under consideration for inclusion in [Web Content Accessibility Guidelines (WCAG) 2.1](https://www.w3.org/TR/WCAG21/).

## Keyboard Access
The drag and drop operation can be performed via a keyboard. To achieve this, a key (e.g., space bar or enter) is assigned to the operations of selecting a source and selecting a destination, respectively. Additional keys (typically arrow keys, possibly supplemented by application-specific shortcuts) alter the position of the object. If multiple objects can be selected in a single drag and drop operation, additional keyboard commands are required. In this scenario, there are two subcases that typically need to be supported.

In the first case, the objects occur contiguously; in a typical
implementation, they may be selected by holding down a modifier key
(conventionally the shift key) while using cursor movement keys to bring
focus to each of the objects to be selected. In the second case, the objects do not occur contiguously, and therefore each is selected via an explicit keyboard action (e.g., by the space bar while holding down the control key to sustain the selection operation). These examples of keyboard behavior are illustrative only. Alternative designs are possible.

In some applications of drag and drop, the keyboard user need only specify the source and the destination, whereas in other applications the path to the destination, including objects traversed along the route are significant. See the examples enumerated in the accompanying spreadsheet.

If the path from source to destination is significant, then it is necessary to complicate the keyboard interface. The best design to adopt depends on the nature of the interaction, including the actions that can be performed along the route.

In some applications, the velocity of the user's action (i.e., the timing of the direct manipulation) contributes to the effect. Examples can be found in educational simulations. Although the intervals between keystrokes can be timed, doing so violates the restriction established by [Web Content Accessibility Guidelines 2.0](https://www.w3.org/TR/WCAG20/), success criterion 2.1.1, on relying upon keyboard timing data in user interfaces. This restriction is intended to support assistive technologies that operate by simulating keystrokes. Thus, an alternative solution for keyboard users is needed to applications that depend on the speed of the user's drag and drop action, such as a control (e.g., slider) that varies the speed of the action.

Two distinct cases should be noted. In the first case, the input events themselves (e.g., the succession of touch or pointer events with changing coordinates, or the duration of a key's being held) are timed. In the second case, the entire drag and drop operation - specifically, the time elapsed after completion of the object selection operation but before the destination selection operation - is timed. This does not involve timing of individual keystrokes, and thus does not appear to contradict the letter of WCAG 2.0.

Keyboard access becomes tedious for the user if the number of potential sources and destinations is large (e.g., moving an object on a plane in an educational game or simulation). This problem is amplified if a screen reader is to be used, as it is not possible to gain a quick overview of the available sources or destinations, and navigating among them can be a slow process with output in speech or braille. If the number of drag and drop operations required to complete a task is large, carrying them out with a keyboard interface likewise becomes significantly time consuming. If a screen reader is used, the time taken to complete the task is further increased by the need to review the available objects to be dragged and dropped, including the effects of previous such operations.

## Consequences of the Drag and Drop Operation
The effects of a drag and drop operation must be made perspicuous to the user. To achieve this, it is necessary not only that effects be plainly visible in the user interface, but that they also be conveyed to assistive technologies via applicable accessibility APIs.

A noteworthy special case occurs where the application moves the object being dropped from the destination chosen by the user to another destination. For example, in a chemistry simulation, a dropped electron may be immediately moved from the location chosen by the user to an outer electron shell in accordance with the physical laws that the simulation depicts. As a second example, an object which is dropped into a grid may be moved to the destination which is geometrically closest to the point on the screen at which the drop action takes place, thus correcting for inaccuracies on the part of the user. Such correction is likely to benefit users who, though capable of operating a touch screen or pointing device, encounter difficulty in positioning objects precisely.

In general, if an object moves upon being dropped, the final destination must be made clear to the user, for example through a visual animation that shows the movement, and via an appropriate notification delivered to accessibility APIs (e.g., a message describing the effects of the drop).

## Speech Input
To support speech input, the user needs to be able conveniently to refer to the object which is to be manipulated, and to specify the destination. Where the presentation of the user interface makes this difficult to achieve, an alternative means of requesting the desired operation must be provided. For example, selecting from among a large number of objects located in a plane is difficult to do via speech input unless the coordinates or other means of reference are readily obtainable.

## Support for Screen Readers
This support has largely been addressed in the preceding sections. Suitable widget roles, accessible descriptions, etc., need to be associated with all of the components of the user interface, and changes in state resulting from the user's actions must be properly reported to the screen reader via the platform accessibility API. The accessible name of each source or destination must be sufficient to make it easily identifiable for the purpose of selection.

## When to Use the Drag and Drop Metaphor
Application designers should carefully consider whether or not to use a drag and drop metaphor, and implement an alternative where appropriate. It may also be reasonable, in some circumstances, to provide a user-configurable option that changes the type of interaction offered. Guidance needs to be developed for deciding whether a drag and drop interaction is appropriate, given the nature of the task to be performed and the diverse needs of users. This sub-committee is yet to develop such guidance.

