# rclcpp: Time

The _rclcpp::Time_ and _rclcpp::Duration_ are a significant departure from
their ROS1 equivalents, but are more closely related to
[std::chrono](https://en.cppreference.com/w/cpp/chrono).

When porting certain ROS1 libraries, there may be significant usage of
timestamps as floating-point seconds. To get floating point seconds from
an _rclcpp::Time_:

```
// node is instance of rclcpp::Node
rclcpp::Time t = node.now();
double seconds = t.seconds();
```

There is no constructor for Time from seconds, so you first need to convert
to nanoseconds:

```
rclcpp::Time t(static_cast<uin64_t>(seconds * 1e9));
```

_rclcpp::Duration_ does have functions to go both directions:

```
rclcpp::Duration d = rclcpp::Duration::from_seconds(1.0);
double seconds = d.seconds();
```