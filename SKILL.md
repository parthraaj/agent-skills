---
name: ibm-block-csi
description: Official IBM Block CSI Driver 1.14.0 documentation. Use for creating, configuring, or troubleshooting any block.csi.ibm.com or csi.ibm.com resource.
---
# IBM Block CSI Driver skill (driver 1.14.0)

All official docs are under docs/. Read the relevant file BEFORE writing any manifest
or diagnosing a failure. Use grep -ril "<keyword>" docs/ when unsure which file applies.
Doc samples are templates: replace every placeholder with real values from the user or
the cluster. Never invent parameter names that do not appear in these docs.

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
1. Read the matching doc. 2. Check that prerequisites exist in the cluster (Secret, StorageClass).
3. Ask for missing values. 4. Show the final manifest. 5. Apply only after the user confirms.
6. Verify (PVC Bound, pod Running) and report.

## Workflow for troubleshooting
1. Read docs/troubleshooting/troubleshooting.md. 2. Gather events, resource status, driver logs.
3. Check known_issues.md for a match. 4. Report: problem, evidence, fix, doc reference.
