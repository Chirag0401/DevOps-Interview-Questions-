Deployment Strategies

	1.	Recreate (Stop and Start)
	•	Description: Shuts down the existing version completely before deploying the new version.
	•	Use Case:
	•	When downtime is acceptable.
	•	Simple applications without complex dependencies.
	•	Advantages: Easy to implement.
	•	Disadvantages: Causes downtime during deployment.

	2.	Rolling Deployment
	•	Description: Gradually replaces instances of the existing version with the new version, one or a few at a time.
	•	Use Case:
	•	When you want zero downtime.
	•	Suitable for stateless applications.
	•	Advantages: No downtime, controlled deployment.
	•	Disadvantages: Hard to roll back if issues arise.

	3.	Blue-Green Deployment
	•	Description: A new environment (green) is deployed and tested while the old environment (blue) continues serving traffic. Traffic is switched to green after validation.
	•	Use Case:
	•	When zero downtime and easy rollback are critical.
	•	For high-risk deployments.
	•	Advantages: Zero downtime, quick rollback.
	•	Disadvantages: Requires duplicate infrastructure, increasing cost.

	4.	Canary Deployment
	•	Description: Deploys the new version to a small subset of users or infrastructure first, then gradually increases coverage.
	•	Use Case:
	•	To test a new version with a small group of users before full rollout.
	•	Advantages: Early detection of issues, minimal user impact.
	•	Disadvantages: Slower deployment process.

	5.	Shadow Deployment
	•	Description: The new version is deployed in parallel with the old version, but only receives traffic in a mirrored fashion (does not impact real users).
	•	Use Case:
	•	For testing production-like traffic without user impact.
	•	Advantages: Safely validates new versions.
	•	Disadvantages: Requires additional infrastructure and complex traffic routing.

	6.	A/B Testing
	•	Description: Deploys multiple versions (e.g., v1 and v2) simultaneously, routing traffic to each based on user segmentation.
	•	Use Case:
	•	To evaluate the effectiveness of new features or UI changes.
	•	Advantages: Validates user experience and performance.
	•	Disadvantages: Limited to frontend applications.

	7.	Feature Flags (Toggle)
	•	Description: New features are toggled on/off in the application without changing the deployed code.
	•	Use Case:
	•	To gradually enable features for users.
	•	Advantages: Instant rollback by toggling the feature off.
	•	Disadvantages: Requires proper implementation and monitoring.

Rollback Strategies

	1.	Rollback to Previous Version
	•	Description: Reverts to the previous stable version.
	•	Use Case:
	•	When issues are detected after deployment.
	•	Advantages: Simple to execute with backups.
	•	Disadvantages: Downtime may occur during the process.

	2.	Blue-Green Rollback
	•	Description: Revert traffic back to the old (blue) environment.
	•	Use Case:
	•	With blue-green deployment strategies.
	•	Advantages: Instant rollback without downtime.
	•	Disadvantages: Higher cost for maintaining duplicate environments.

	3.	Canary Rollback
	•	Description: Roll back changes gradually, reverting to the old version for affected users only.
	•	Use Case:
	•	With canary deployment strategies.
	•	Advantages: Controlled rollback with minimal user impact.
	•	Disadvantages: Requires complex traffic management.

	4.	Feature Toggle Rollback
	•	Description: Disable problematic features via a feature toggle.
	•	Use Case:
	•	When feature flags are used in deployment.
	•	Advantages: Instant rollback without redeployment.
	•	Disadvantages: Requires feature toggle support.

	5.	Database Rollback
	•	Description: Reverts database changes alongside application rollback.
	•	Use Case:
	•	When a new application version involves schema changes.
	•	Advantages: Maintains compatibility between versions.
	•	Disadvantages: Requires careful database backup and restore planning.

Which Strategy to Use?

Use Case	Recommended Strategy
Zero downtime	Rolling Deployment, Blue-Green Deployment
High-risk changes	Canary Deployment, Blue-Green Deployment
Testing new features in production	Canary Deployment, A/B Testing
Fast rollback capability	Blue-Green Deployment, Feature Toggles
Backend application changes	Rolling Deployment
High-availability systems	Canary Deployment, Blue-Green Deployment
Production-like testing before release	Shadow Deployment
Cost-sensitive environments	Rolling Deployment, Recreate Strategy

