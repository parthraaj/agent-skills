---
name: ibm-block-csi
description: Official IBM Block CSI Driver 1.14.0 documentation. Use for creating, configuring, or troubleshooting any block.csi.ibm.com or csi.ibm.com resource.
---
# IBM Block CSI Driver skill (driver 1.14.0)

All official docs are under docs/. Read the relevant file BEFORE writing any manifest
or diagnosing a failure. Use grep -ril "<keyword>" docs/ when unsure which file applies.
Doc samples are templates: replace every placeholder with real values from the user or
the cluster. Never invent parameter names that do not appear in these docs.

## Which source to use
Use the right source for each kind of field. If sources disagree, follow the order below.

1. Driver-specific values: ONLY these docs
   - StorageClass `parameters` (pool, SpaceEfficiency, secret references, fstype, etc.)
   - Array Secret keys (docs/configuration/creating_secret.md)
   - VolumeSnapshotClass, VolumeGroupClass and VolumeReplicationClass `parameters`
   - Allowed values and meaning of any csi.ibm.com field
   These are free-form or driver-defined. The cluster schema cannot validate them, so
   never guess them from general Kubernetes knowledge.

2. Structure of csi.ibm.com resources: the live CRD schema
   - Read the CRD with k8s_get_resource_yaml on resource type
     customresourcedefinitions, for example hostdefinitions.csi.ibm.com.
     Its spec.versions[].schema.openAPIV3Schema lists the real field names, types and
     required fields for the CRD version installed on this cluster.
   - The schema gives field names and types. The docs give meaning and valid values.
     Use both.
   - Installed CRDs: list them with k8s_get_available_api_resources (group csi.ibm.com).

3. Standard Kubernetes fields: general Kubernetes API knowledge
   - PVC spec (accessModes, resources.requests.storage, storageClassName, volumeMode)
   - StorageClass top-level fields (reclaimPolicy, volumeBindingMode, allowVolumeExpansion)
   - Pod volumes and volumeMounts, StatefulSet volumeClaimTemplates
   - VolumeSnapshot spec (snapshot.storage.k8s.io)
   These are standard upstream APIs. Still check the docs/ sample for the related
   resource, because it shows how the driver expects them combined.

4. Current state: always the live cluster
   - Whether a Secret, StorageClass, PVC or CRD exists, its status, events and logs.
   - Never assume something exists because a doc mentions it.

## Where to look
- Secret for the array: docs/configuration/creating_secret.md (topology: creating_secret_topology_aware.md)
- StorageClass: docs/configuration/creating_volumestorageclass.md (topology: creating_storageclass_topology_aware.md)
- PVC: docs/configuration/creating_pvc.md, expand: expanding_pvc.md
- StatefulSet / sample app: docs/configuration/creating_statefulset.md, docs/using/sample_stateful_container.md
- Snapshots: docs/configuration/creating_volumesnapshotclass.md, creating_volumesnapshot.md
  (topology: creating_volumesnapshotclass_topology_aware.md)
- Volume groups: docs/configuration/creating_volumegroupclass.md, creating_volumegroup.md,
  creating_storageclass_vg.md, creating_pvc_vg.md; docs/using/delete_vg.md, promoting_vg.md, removing_pvc_vg.md
- Replication: docs/configuration/creating_volumereplicationclass.md, creating_volumereplication.md
- Policy-based replication: docs/configuration/configuring_policy_based_replication.md,
  creating_volumereplication_pbr.md, finding_replication_policy_name.md, finding_systemid.md;
  docs/using/using_policy_based_replication.md
- Host definer: docs/configuration/configuring_hostdefiner.md, docs/using/using_hostdefinition.md,
  using_hostdefinition_labels.md
- Importing existing volumes: docs/configuration/importing_existing_volume.md, importing_existing_volume_group.md
- Connectivity: docs/using/changing_node_connectivity.md, adding_fc_interface_to_worker_node.md,
  docs/configuration/enable_multipath.md
- Topology: docs/configuration/configuring_topology.md
- SVC partitions / VMs / advanced: docs/configuration/configuring_svc_partitions.md, configuring_vm.md,
  advanced_configuration.md
- Install / upgrade / uninstall: docs/installation/
- Troubleshooting: docs/troubleshooting/, then docs/release_notes/known_issues.md and limitations.md
- Compatibility: docs/release_notes/compatibility_requirements.md, supported_*.md
- What changed in 1.14.0: docs/release_notes/changelog_1.14.0.md
- Full table of contents: docs/SUMMARY.md

## Workflow for create requests
1. Read the matching doc. 2. For csi.ibm.com resources, also read the CRD schema.
3. Check that prerequisites exist in the cluster (Secret, StorageClass).
4. Ask for missing values. 5. Show the final manifest. 6. Apply only after the user confirms.
7. Verify (PVC Bound, pod Running) and report.

## Workflow for troubleshooting
1. Read docs/troubleshooting/troubleshooting.md. 2. Gather events, resource status, driver logs.
3. Check known_issues.md for a match. 4. Report: problem, evidence, fix, doc reference.
