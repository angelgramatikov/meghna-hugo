+++
author = "wifi-ninja"
date = 2022-12-19T22:00:00Z
description = ""
image = "/images/blog/requirements-Gathering-applications.png"
image_webp = "/images/blog/requirements-Gathering-applications.webp"
title = "Requirements Gathering - Applications"

+++
Once you have identified the client devices and their radio capabilities, you must next determine the applications that will be used and their performance requirements (throughput and QoS). A thorough understanding of the application requirements will provide the necessary information to design a successful WLAN that meets organizational needs.

Through this process, you can identify the critical and non-critical applications and establish a target application throughput level for each device that is required for successful operation.

The following table lists common application classes and typical bandwidth requirements. Additionally, recommended QoS classes are provided for both Layer 2 and Layer 3. These QoS classes are based on common network best practices but should be tailored to each environment to ensure integration with existing network policies and consistency with an end-to-end QoS implementation.

![](/images/applications-table.png)

Give special consideration to video applications due to their typical requirements for high bandwidth and low latency. Video applications should use a Constant Bit-Rate (CBR) codec to control the performance and user experience, which ensures that the first few clients do not consume a large amount of bandwidth if using a Variable Bit-Rate (VBR) video codec. In addition, consider using multicast transmission for HD video streams of greater than 2 Mbps to increase client capacity in a high-density setting where multiple clients will be receiving the stream. However, multicast transmission can be less reliable than unicast transmission because clients do not acknowledge the data they receive and the server does not retransmit data if it is corrupted in transit. You can enable multicast-to-unicast conversion to improve reliability (see the “Network Configuration” section), but doing so will reduce the number of clients that APs can support concurrently. Be sure to make note of any applications used internally that are based on UDP or multicast, as client performance and throughput capabilities are typically substantially different due to the lower overhead that these protocols use.

Knowing the application requirements provides the following input into subsequent Wi-Fi network design and configuration:

* **Target Application Throughput Levels (per Device)** – Based on critical applications on each device type and application throughput requirements


* **Client SLA Target Throughput** – Based on target application throughput levels; applied to different user groups


* **Per-User Rate Limits** – Based on maximum application throughput requirements plus a recommended additional 20% to accommodate temporary application bursts

### Forecasting AP Capacity

Once the client device and application requirements have been identified, you can forecast the required access point radio capacity (and subsequently estimate the number of APs) to aid in Wi-Fi network design. The forecast is derived by estimating the network load (based on airtime) required for each client device to achieve its targeted application throughput level. This is represented as a percentage of airtime that will be consumed per-device on an AP radio, with the aggregate sum being used to forecast the required AP capacity to support all clients concurrently.

First, determine how much airtime the target application throughput level will consume on each device type by dividing the required throughput by the maximum TCP or UDP throughput the device can achieve. For example, a 1 Mbps TCP video application running on an Apple iPad mini that can achieve a maximum 30-Mbps TCP throughput on a 20 MHz channel yields an airtime consumption of 3.33% per device on a particular channel. This means that every iPad mini device running the video application requires 3.33% of the capacity of a single access point radio (assuming no outside noise or interference). Perform this calculation separately for every device type that will be supported in the environment. If you are using 40 MHz channels in the 5 GHz frequency band, perform this calculation separately for both frequency bands with dual-band capable clients. This is required since the airtime consumed on a 40 MHz channel for the same application throughput level is less than a 20 MHz channel. For example the same Apple iPad mini will consume only 1.66% airtime on a 40 MHz channel due to the higher peak data rate.

You can also use the airtime consumption value to estimate of the number of devices that a single AP radio can support (when all devices are of the same type). This can be useful in environments where the client device population is controlled by the organization and client distribution is well known (for example, a classroom environment where all students use the same type of device during the lesson plan). To estimate the number of devices supported on a single AP radio, divide the individual device airtime consumption value into 80%. An individual Wi-Fi channel saturates around 80% of airtime utilization. Therefore, the total capacity of a single AP radio is 80% divided by the airtime required per device. For example, a single 2.4 GHz AP radio operating at 20 MHz channel width serving only Apple iPad mini devices running a 1-Mbps TCP video application could support a maximum of 24 devices concurrently (80/3.33).

Second, multiply the quantity of devices for each device type by the required airtime for each device to determine the total airtime required for those devices. If you are using 40 MHz channels in the 5 GHz frequency band then you will need to split dual-band capable clients between both frequency bands (based on the desired band steering ratio) to accurately determine their airtime consumption. Once the total airtime is determined, divide it by 80% to determine the number of AP radios required to support those devices in the environment. For example, if there are 75 total Apple iPad minis on 2.4 GHz and each one consumes 3.33% airtime, then a total of 3.12 AP radios are required to support all 75 devices concurrently: (75 * 3.33%) ÷ 80%. Perform this calculation individually for every client device type that you expect will be in the environment.

Finally, add the number of AP radios needed to support each client device type to determine the total number of AP radios required in the environment; round up if necessary. Adjust the number of radios if only a percentage of clients will be connected to the WLAN concurrently. If all client devices will be online concurrently, then no adjustment is necessary. Since most deployments use dual-radio APs, divide the adjusted number of AP radios by two to forecast the number of dual-radio access points needed to support the identified devices and applications. If a fractional number results, round up.

It is important to understand that the forecasted AP capacity is only an estimate; the final capacity will likely be slightly different. The forecast is useful as an initial starting point for the Wi-Fi network design, especially in circumstances where a preliminary project budget or Bill of Materials (BOM) must be determined prior to facility construction. Use the forecasted AP capacity as input into a predictive RF site survey to ensure sufficient capacity, not simply coverage, exists to serve the anticipated client base. The site survey process verifies your AP capacity forecast and will likely need to be changed due to facility characteristics that require higher capacity by colocating APs or coverage in less-common areas such as hallways, stairwells, bathrooms, and elevators.

Through the process of requirements gathering, you are now armed with adequate information about the client, application, and network infrastructure to begin the planning and designing the network deployment.