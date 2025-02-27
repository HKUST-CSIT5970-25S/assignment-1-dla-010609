[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)
# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: DENG,Luoao
### Student Id: 21090802
### Email: ldengap@connect.ust.hk

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

    > Measurement Tool Name
Phoronix Test Suite.
Configuration of the Measurement Tool
Installation Environment
Ensure that PHP is installed on the system (PHP 5.3 or later is recommended) along with the PHP DOM extension.
PHP can be installed via a package manager (e.g., yum install php or php7-cli).
After downloading Phoronix Test Suite, extract the files and run the installation script.
Test Suite Selection
Use the command phoronix-test-suite list-available-tests to view all available tests.
Select test suites suitable for CPU and memory performance testing, such as:
pts/cpu: for CPU performance testing.
pts/sysbench: which includes memory performance testing.
Running the Tests
Use the command phoronix-test-suite run <test or suite name> to execute the tests.
For example: phoronix-test-suite run pts/cpu or phoronix-test-suite run pts/sysbench.
Test Parameter Configuration
By default, Phoronix Test Suite automatically configures test parameters, but you can also manually adjust them by editing the test's XML file.
For example, you can adjust the number of test runs or the size of the test data to better match real-world scenarios.
Reasons for Parameter Settings
Number of Runs: Typically, multiple runs (e.g., 3 or more) are configured to reduce random errors and obtain more stable results.
Test Data Size: The size of the test data is chosen based on real-world application scenarios to simulate actual workloads accurately.
Test Type: Tests are selected based on the target hardware performance (e.g., CPU-intensive or memory-intensive tasks) to provide a more accurate assessment.
Meaning of Measurement Results
CPU Performance:
The results are usually expressed as "Events Per Second" (e.g., in Sysbench CPU tests).
A higher value indicates that the CPU can handle more tasks per unit of time, reflecting stronger performance.
Memory Performance:
Memory bandwidth results are typically shown as "Megabytes per Second" (MiB/sec) (e.g., in Sysbench memory tests).
Higher bandwidth indicates faster memory data transfer, which is beneficial for memory-intensive tasks.
Other Metrics:
The results may also include the standard deviation to measure the stability of the results.
By comparing the results with samples on OpenBenchmarking.org, you can understand the relative performance level in the industry.
Conclusion
In summary, Phoronix Test Suite is a powerful open-source performance testing tool that offers flexible configuration and detailed results. It is suitable for evaluating CPU and memory performance in various scenarios.

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance | Memory performance |
    | ----------- | --------------- | ------------------ |
    | `t2.micro` |          3612 MIPS       |          10880.66 MB/s          |
    | `t2.medium`  |            5858 MIPS     |               19517.40 MB/s     |
    | `c5d.large` |        4880 MIPS         |       13690.00 MB/s             |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    | Type                      | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t3.medium` - `t3.medium` |    3910        |   0.299  |
    | `m5.large` - `m5.large`   |    4950        |   0.158  |
    | `c5n.large` - `c5n.large` |    4950        |   0.134  |
    | `t3.medium` - `c5n.large` |    1810        |   0.786  |
    | `m5.large` - `c5n.large`  |    4180        |   0.198  |
    | `m5.large` - `t3.medium`  |    1820        |   0.693  |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.

2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      |      32.2      |   60.950 |
    | N. Virginia - N. Virginia |      4960      |   0.238  |
    | Oregon - Oregon           |      4910      |   0.172  |
 
    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.
