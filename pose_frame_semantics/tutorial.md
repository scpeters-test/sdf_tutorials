# Pose Frame Semantics

In version 1.4 and earlier of the SDF spec, the `<pose>` element represents
a relative coordinate transformation between a frame and its parent.
Link frames were always defined relative to a model frame and joint frames
relative to their child link frames.

In version 1.5 of the SDF spec, the `frame` attribute string was added to
`<pose>` elements to allow poses to be defined relative to a named frame
instead of the default frames from version 1.4.
For example, this would allow an SDF model to define its kinematics like a
URDF, with joint frames defined relative to the parent link frame and
a joint's child link frames relative to the joint frame.

The 1.5 spec also adds `<frame>` elements which can define named coordinate
frames in addition to the existing link and joint frames in the model.

This document is a work in progress to define the semantics of the pose frame
attribute.

## Legacy behavior

### Parent frames in sdf 1.4

With the exception of joint frames, all `<pose>` tags in sdf 1.4 define
a relative transform between the current element's frame and the frame of its
parent xml element.

For example, in the following model, the link frame is defined relative to
the model frame, and the inertial, collision, visual, and sensor frames
are all defined relative to the model frame.

    <sdf version="1.4">
      <model name="model">
        <pose>...</pose>
        <link name="link">
          <pose>...</pose>
          <inertial>
            <pose>...</pose>
          </inertial>
          <collision name="collision">
            <pose>...</pose>
          </collision>
          <visual name="visual">
            <pose>...</pose>
          </visual>
          <sensor name="sensor">
            <pose>...</pose>
          </sensor>
        </link>
      </model>
    </sdf>

The one exception is the joint frame, which is defined relative to the child
link frame. In the following example, the joint frame is defined relative
to the link frame of `link2`.

    <sdf version="1.4">
      <model name="model">
        <pose>...</pose>
        <link name="link1">
          <pose>...</pose>
        </link>
        <link name="link2">
          <pose>...</pose>
        </link>
        <joint name="joint" type="fixed">
          <pose>...</pose>
          <parent>link1</parent>
          <child>link2</child>
        </joint>
      </model>
    </sdf>

Given this longstanding behavior, this pattern should be followed for
sdf 1.5+ when the pose frame attribute is empty.
This would imply that the following models are equivalent to the previous
models discussed in this section:

    <sdf version="1.5">
      <model name="model">
        <pose frame=''>...</pose>
        <link name="link">
          <pose frame=''>...</pose>
          <inertial>
            <pose frame=''>...</pose>
          </inertial>
          <collision name="collision">
            <pose frame=''>...</pose>
          </collision>
          <visual name="visual">
            <pose frame=''>...</pose>
          </visual>
          <sensor name="sensor">
            <pose frame=''>...</pose>
          </sensor>
        </link>
      </model>
    </sdf>

 

    <sdf version="1.5">
      <model name="model">
        <pose frame=''>...</pose>
        <link name="link1">
          <pose frame=''>...</pose>
        </link>
        <link name="link2">
          <pose frame=''>...</pose>
        </link>
        <joint name="joint" type="fixed">
          <pose frame=''>...</pose>
          <parent>link1</parent>
          <child>link2</child>
        </joint>
      </model>
    </sdf>


### Specifying parent and child link names

Joints currently specify parent and child links by name.

nested model convention?

## Proposed behavior

This section includes proposals for
