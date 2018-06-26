<!--
* Copyright (c) 2017, 2018 IBM Corp. and others
*
* This program and the accompanying materials are made
* available under the terms of the Eclipse Public License 2.0
* which accompanies this distribution and is available at
* https://www.eclipse.org/legal/epl-2.0/ or the Apache
* License, Version 2.0 which accompanies this distribution and
* is available at https://www.apache.org/licenses/LICENSE-2.0.
*
* This Source Code may also be made available under the
* following Secondary Licenses when the conditions for such
* availability set forth in the Eclipse Public License, v. 2.0
* are satisfied: GNU General Public License, version 2 with
* the GNU Classpath Exception [1] and GNU General Public
* License, version 2 with the OpenJDK Assembly Exception [2].
*
* [1] https://www.gnu.org/software/classpath/license.html
* [2] http://openjdk.java.net/legal/assembly-exception.html
*
* SPDX-License-Identifier: EPL-2.0 OR Apache-2.0 OR GPL-2.0 WITH
* Classpath-exception-2.0 OR LicenseRef-GPL-2.0 WITH Assembly-exception
-->

# -XX:[+|-]UseContainerSupport

**(Linux<sup>&trade;</sup> only)**

If your application is running in a container that imposes a memory limit, and you want the VM to allocate a larger fraction of memory to the Java heap, set the  `-XX:+UserContainerSupport` option.

## Syntax

        -XX:[+|-]UseContainerSupport



| Setting                    | Effect  | Default                                                                            |
|----------------------------|---------|:----------------------------------------------------------------------------------:|
| `-XX:-UseContainerSupport` | Disable | <i class="fa fa-check" aria-hidden="true"></i><span class="sr-only">Default</span> |
| `-XX:+UseContainerSupport` | Enable  |                                                                                    |


When using container technology, applications are typically run on their own and do not need to compete for memory. The VM detects when OpenJ9 is running inside a container that imposes a memory limit, and if `-XX:+UserContainerSupport` is set, adjusts the maximum Java heap size appropriately.

The following table shows the values that are used when `-XX:+UserContainerSupport` is set:

| Physical memory *&lt;size&gt;* | Maximum Java heap size  |
|--------------------------------|-------------------------|
| Less than 1 GB                 | 50% *&lt;size&gt;*      |
| 1 GB - 2 GB                    | *&lt;size&gt;* - 512 MB |
| Greater than 2 GB              | 75% *&lt;size&gt;*      |

When [`-XX:MaxRAMPercentage`](xxmaxrampercentage.md) or [`-XX:InitialRAMPercentage`](xxinitialrampercentage.md) are used with `-XX:+UseContainerSupport`, the corresponding heap setting is determined based on the memory limit of the container. For example, to set the maximum heap size to 80% of the container memory, specify the following options:

    -XX:+UseContainerSupport -XX:MaxRAMPercentage=80



<!-- ==== END OF TOPIC ==== xxusecontainersupport.md ==== -->