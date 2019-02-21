# Pose Frame Semantics

In version 1.4 and earlier of the SDF spec, the `<pose>` element represents
a relative coordinate transformation between a frame and its parent.
Link frames were always defined relative to a model frame and joint frames
relative to the child link frames.
In version 1.5 of the SDF spec, the `frame` attribute string was added to
`<pose>` elements to allow poses to be defined relative to a named frame
instead of the default frames from version 1.4.
For example, this would allow an SDF model to define its kinematics like a
URDF, with joint frames defined relative to the parent link frame and
link frames of the child links of a joint relative to the joint frame.

The 1.5 spec also adds `<frame>` elements which can define named coordinate
frames in addition to the existing link and joint frames in the model.

This document is a work in progress to define the semantics of the pose frame
attribute.

## Legacy behavior

### Parent frames in sdf 1.4

Use these as default values if pose frame is unspecified.

### Specifying parent and child link names

Joints currently specify parent and child links by name.

nested model convention?

## Proposed behavior

This section includes proposals for
