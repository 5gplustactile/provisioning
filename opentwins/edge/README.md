# NOTES

To configure the HA in cluster the ```masterNodes: X``` field should be an odd number. This is because etcd, the distributed key-value store that Kubernetes uses for state management, operates as a consensus-based system. For consensus to be reached, and to tolerate failures, the number of etcd instances should be odd.