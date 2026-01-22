.. Licensed to the Apache Software Foundation (ASF) under one
   or more contributor license agreements.  See the NOTICE file
   distributed with this work for additional information#
   regarding copyright ownership.  The ASF licenses this file
   to you under the Apache License, Version 2.0 (the
   "License"); you may not use this file except in compliance
   with the License.  You may obtain a copy of the License at
   http://www.apache.org/licenses/LICENSE-2.0
   Unless required by applicable law or agreed to in writing,
   software distributed under the License is distributed on an
   "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
   KIND, either express or implied.  See the License for the
   specific language governing permissions and limitations
   under the License.

CloudStack CSI Driver
=======================

CloudStack Container Storage Interface (CSI) plugin enables Kubernetes clusters running on Apache CloudStack to dynamically provision, manage, and use CloudStack storage volumes

Features
--------

- Automatic provisioning: Create persistent volumes on-demand from Kubernetes PVCs
- No manual intervention: Eliminates need to manually create CloudStack volumes
- Kubernetes-native: Uses standard Kubernetes storage classes and PVC workflows

Advanced Storage Features
-------------------------
- Volume snapshots: Backup and restore capabilities
- Dynamic expansion: Grow volumes without downtime or data migration
- Flexible reclaim policies: Choose between automatic cleanup or data retention

Core Components
-----------------
- CSI Controller: Manages volume lifecycle, snapshots, and CloudStack API interactions
- CSI Node Driver: Handles volume mounting and unmounting on worker nodes
- Storage Class Syncer: Automatically syncs CloudStack disk offerings to Kubernetes storage classes

CSI integration with CKS
~~~~~~~~~~~~~~~~~~~~~~~~~~
From 4.22.0, CloudStack Kubernetes Service provides CSI integration that allows dynamic provisioning of CloudStack volumes for Kubernetes pods running on CKS clusters.
To enable CSI integration, the CKS data ISOs must have the CSI manifests. Rebuilding the CKS data ISOs using the `create-kubernetes-binaries-iso.sh` script will build ISOs with CSI manifests and images. Pre-built ISOs for Kubernetes versions 1.31.1, 1.32.5 and 1.33.1 are available at https://download.cloudstack.org/cks/

|cks-csi-integration.png|

Enabling CSI integration for a CKS cluster can be done by selecting the `Enable CSI Integration` checkbox in the Advanced Settings section of the Kubernetes cluster creation form.
Doing so will setup the CSI components - the CSI controller and the CSI node daemonset - on the cluster during its creation.

|cks-csi-pods.png|

Further details about using CSI with CKS can be found at: https://github.com/cloudstack/cloudstack-csi-driver/blob/main/README.md

.. |cks-csi-integration.png| image:: /_static/images/cks-csi-integration.png
   :alt: Integration of CSI with CKS.
.. |cks-csi-pods.png| image:: /_static/images/cks-csi-pods.png
   :alt: CSI Pods.