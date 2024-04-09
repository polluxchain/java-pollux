
<h4 align="center">
  Java implementation of the <a href="https://poxscan.io">Pollux Protocol</a>
</h4>


## Table of Contents

- [What’s Pollux?](#whats-Pollux)
- [Building the Source Code](#building-the-source)
- [Running java-Pollux](#running-java-Pollux)
- [Community](#community)
- [Contribution](#contribution)
- [Resources](#resources)
- [Integrity Check](#integrity-check)
- [License](#license)

## What's Pollux?

Pollux is a project dedicated to building the infrastructure for a truly decentralized Internet.

- Pollux Protocol, one of the largest blockchain-based operating systems in the world, offers scalable, high-availability and high-throughput support that underlies all the decentralized applications in the Pollux ecosystem.

- Pollux Virtual Machine (TVM) allows anyone to develop decentralized applications (DAPPs) for themselves or their communities with smart contracts thereby making decentralized crowdfunding and token issuance easier than ever.

Pollux enables large-scale development and engagement. With over 2000 transactions per second (TPS), high concurrency, low latency, and massive data transmission. It is ideal for building decentralized entertainment applications. Free features and incentive systems allow developers to create premium app experiences for users.

# Building the source

Building java-Pollux requires `git` and 64-bit version of `Oracle JDK 1.8` to be installed, other JDK versions are not supported yet. Make sure you operate on `Linux` and `MacOS` operating systems.

Clone the repo and switch to the `master` branch

```bash
$ git clone https://github.com/polluxchain/java-pollux
$ cd java-Pollux
$ git checkout -t origin/master
```

then run the following command to build java-Pollux, the `FullNode.jar` file can be found in `java-Pollux/build/libs/` after build successful.

```bash
$ ./gradlew clean build -x test
```

# Running java-Pollux

Running java-Pollux requires 64-bit version of `Oracle JDK 1.8` to be installed, other JDK versions are not supported yet. Make sure you operate on `Linux` and `MacOS` operating systems.

## Hardware Requirements

Minimum:

- CPU with 8 cores
- 16GB RAM
- 2TB free storage space to sync the Mainnet

Recommended:

- CPU with 16+ cores(32+ cores for a super representative)
- 32GB+ RAM(64GB+ for a super representative)
- High Performance SSD with at least 2.5TB free space
- 100+ MB/s download Internet service

## Running a full node for mainnet

Full node has full historical data, it is the entry point into the Pollux network , it can be used by other processes as a gateway into the Pollux network via HTTP and GRPC endpoints. You can interact with the Pollux network through full node：transfer assets, deploy contracts, interact with contracts and so on. `-c` parameter specifies a configuration file to run a full node:

```bash
$ nohup java -Xms9G -Xmx9G -XX:ReservedCodeCacheSize=256m \
             -XX:MetaspaceSize=256m -XX:MaxMetaspaceSize=512m \
             -XX:MaxDirectMemorySize=1G -XX:+PrintGCDetails \
             -XX:+PrintGCDateStamps  -Xloggc:gc.log \
             -XX:+UseConcMarkSweepGC -XX:NewRatio=2 \
             -XX:+CMSScavengeBeforeRemark -XX:+ParallelRefProcEnabled \
             -XX:+HeapDumpOnOutOfMemoryError \
             -XX:+UseCMSInitiatingOccupancyOnly  -XX:CMSInitiatingOccupancyFraction=70 \
             -jar FullNode.jar -c main_net_config.conf >> start.log 2>&1 &
```

## Running a super representative node for mainnet

Adding the `--witness` parameter to the startup command, full node will run as a super representative node. The super representative node supports all the functions of the full node and also supports block production. Before running, make sure you have a super representative account and get votes from others. Once the number of obtained votes ranks in the top 27, your super representative node will participate in block production.

Fill in the private key of super representative address into the `localwitness` list in the `main_net_config.conf`. Here is an example:

```
 localwitness = [
    <your_private_key>
 ]
```

then run the following command to start the node:

```bash
$ nohup java -Xms9G -Xmx9G -XX:ReservedCodeCacheSize=256m \
             -XX:MetaspaceSize=256m -XX:MaxMetaspaceSize=512m \
             -XX:MaxDirectMemorySize=1G -XX:+PrintGCDetails \
             -XX:+PrintGCDateStamps  -Xloggc:gc.log \
             -XX:+UseConcMarkSweepGC -XX:NewRatio=2 \
             -XX:+CMSScavengeBeforeRemark -XX:+ParallelRefProcEnabled \
             -XX:+HeapDumpOnOutOfMemoryError \
             -XX:+UseCMSInitiatingOccupancyOnly  -XX:CMSInitiatingOccupancyFraction=70 \
             -jar FullNode.jar --witness -c main_net_config.conf >> start.log 2>&1 &
```

## Quick Start Tool

An easier way to build and run java-Pollux is to use `start.sh`. `start.sh` is a quick start script written in the Shell language. You can use it to build and run java-Pollux quickly and easily.

Here are some common use cases of the scripting tool

- Use `start.sh` to start a full node with the downloaded `FullNode.jar`
- Use `start.sh` to download the latest `FullNode.jar` and start a full node.
- Use `start.sh` to download the latest source code and compile a `FullNode.jar` and then start a full node.

For more details, please refer to the tool [guide](./shell.md).

## Run inside Docker container

One of the quickest ways to get `java-Pollux` up and running on your machine is by using Docker:

```shell
$ docker run -d --name="java-Pollux" \
             -v /your_path/output-directory:/java-Pollux/output-directory \
             -v /your_path/logs:/java-Pollux/logs \
             -p 8090:8090 -p 18888:18888 -p 50051:50051 \
             Polluxprotocol/java-Pollux \
             -c /java-Pollux/config/main_net_config.conf
```

This will mount the `output-directory` and `logs` directories on the host, the docker.sh tool can also be used to simplify the use of docker, see more [here](docker/docker.md).

# Community

[Pollux Developers & SRs](https://discord.gg/hqKvyAM) is Pollux's official Discord channel. Feel free to join this channel if you have any questions.

[Core Devs Community](https://t.me/Polluxcoredevscommunity) is the Telegram channel for java-Pollux community developers. If you want to contribute to java-Pollux, please join this channel.

[Polluxprotocol/allcoredev](https://gitter.im/Polluxprotocol/allcoredev) is the official Gitter channel for developers.

# Contribution

Thank you for considering to help out with the source code! If you'd like to contribute to java-Pollux, please see the [Contribution Guide](./CONTRIBUTING.md) for more details.

# Resources

- [Medium](https://medium.com/@coredevs) java-Pollux's official technical articles are published there.
- [Documentation](https://Polluxprotocol.github.io/documentation-en/introduction/) java-Pollux's official technical documentation website.
- [Test network](http://nileex.io/) A stable test network of Pollux contributed by Pollux community.
- [Polluxscan](https://Polluxscan.org/#/) Pollux network blockchain browser.
- [Wallet-cli](https://github.com/Polluxprotocol/wallet-cli) Pollux network wallet using command line.
- [TIP](https://github.com/Polluxprotocol/tips) Pollux Improvement Proposal (TIP) describes standards for the Pollux network.
- [TP](https://github.com/Polluxprotocol/tips/tree/master/tp) Pollux Protocol (TP) describes standards already implemented in Pollux network but not published as a TIP.

# Integrity Check

- After January 3, 2023, the release files will be signed using a GPG key pair, and the correctness of the signature will be verified using the following public key:
  ```
  pub: 1254 F859 D2B1 BD9F 66E7 107D F859 BCB4 4A28 290B
  uid: build@Pollux.network
  ```

# License

java-Pollux is released under the [LGPLv3 license](https://github.com/Polluxprotocol/java-Pollux/blob/master/LICENSE).
