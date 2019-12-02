# complementary_filter_node

## Subscribed Topics

* imu/data_raw (sensor_msgs/Imu)
  * Message containing raw IMU data, including angular velocities and linear accelerations.
* imu/mag (sensor_msgs/MagneticField)
  * [optional] Magnetic field vector

## Published Topics

* imu/data (sensor_msgs/Imu)
  * The fused Imu message, containing the orientation.
* imu/rpy/filtered (geometry_msgs/Vector3)
  * Debug only: The roll, pitch and yaw angles corresponding to the orientation published on the imu_data topic. (only published when ~publish_debug_topics == true)
* imu/steady_state (std_msgs/Bool)
  * Debug only: Whether we are in the steady state when doing bias estimation. (only published when ~publish_debug_topics == true)

## Parameters

Not Dynamically Reconfigurable Parameters

* ~gain_acc (double, default: 0.01)
  * Gain for the complementary filter, belongs in [0, 1].
* ~gain_mag (double, default: 0.01)
  * Gain for the complementary filter, belongs in [0, 1].
* ~bias_alpha (double, default: 0.01)
  * Bias estimation gain, belongs in [0, 1].
* ~do_bias_estimation (bool, default: true)
  * Whether to do bias estimation of the angular velocity (gyroscope readings) or not.
* ~do_adaptive_gain (bool, default: true)
  * Whether to do adaptive gain or not.
* ~use_mag (bool, default: false)
  * Whether to use the magnetic field data in the data fusion.
* ~fixed_frame (string, default: odom)
  * The parent frame to be used in publish_tf.
* ~publish_tf (bool, default: false)
  * Whether to publish a TF transform that represents the orientation of the IMU, using the frame specified in fixed_frame as the parent frame and the frame given in the input imu message as the child frame.
* ~reverse_tf (bool, default: false)
  * If set to true, publish transforms from imu_frame to fixed frame instead of the other way around.
* ~constant_dt (double, default: 0.0)
  * The dt to use; if 0.0 (default), compute dt dynamically from message headers.
* ~publish_debug_topics (bool, default: false)
If set to true, publish a couple of debug topics.

***[Experimental]***

* ~bias_angular_velocity_x_threshold (double, default: 0.01)
  * Angular velocity threshold used for the bias estimation
  * It should be at least the double of the angular velocity drift
* ~bias_angular_velocity_y_threshold (double, default: 0.01)
  * Angular velocity threshold used for the bias estimation
  * It should be at least the double of the angular velocity drift
* ~bias_angular_velocity_z_threshold (double, default: 0.01)
  * Angular velocity threshold used for the bias estimation
  * It should be at least the double of the angular velocity drift
* ~bias_k_acceleration_threshold (double, default: 0.1)
  * Acceleration threshold used for the bias estimation
* ~bias_k_delta_angular_velocity_threshold (double, default: 0.01)
  * Delta angular velocity threshold used for the bias estimation
* ~bias_k_angular_velocity_x_drift (double, default: 0.005)
  * Estimated angular velocity drift of the sensor
* ~bias_k_angular_velocity_y_drift (double, default: 0.005)
  * Estimated angular velocity drift of the sensor
* ~bias_k_angular_velocity_z_drift (double, default: 0.005)
  * Estimated angular velocity drift of the sensor


## Provided tf Transforms

* fixed_frame → imu_frame
  * Only for debug purposes! This is a transform from the fixed frame (specified in the parameter fixed_frame, default: "odom") to the header.frame_id frame from the incoming imu messages. Only the rotation is valid.
