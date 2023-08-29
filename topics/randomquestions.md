What is the difference between Git pull & Git fetch?

Both `git pull` and `git fetch` are Git commands used to update your local repository with changes from a remote repository. However, they work differently and have distinct purposes:

**1. Git Fetch:**
- `git fetch` is used to retrieve updates from a remote repository without automatically merging them into your working branch.
- It downloads new objects and references from the remote repository but doesn't apply any changes to your local branches.
- The fetched changes are stored in a separate area of your repository called the "remote-tracking branches" (e.g., `origin/master`).
- This allows you to see what changes have been made on the remote repository before deciding to merge or rebase.

**2. Git Pull:**
- `git pull` is a combination of two commands: `git fetch` followed by `git merge` or `git rebase`.
- It fetches the changes from the remote repository and then automatically merges or rebases them into your current local branch.
- If the remote changes and your local changes overlap (resulting in a merge conflict), Git will ask you to resolve the conflict before proceeding.
- If you want to update your local branch to match the remote branch's state, including any new commits, you can use `git pull`.

In summary, `git fetch` retrieves changes from the remote repository but leaves your local branches unchanged. `git pull`, on the other hand, incorporates the fetched changes into your local branch. The choice between them depends on whether you want to review changes before merging and whether you want more control over how and when changes are integrated into your local branch.

==================================================

·     What is Blue/Green deployment?

Blue/Green deployment is a software release strategy used in the context of deploying applications or services to production environments. It involves having two separate environments, referred to as "Blue" and "Green," where one environment is active and serving live traffic while the other remains idle. This approach allows for seamless and low-risk deployments with minimal downtime and the ability to quickly rollback if issues arise.

Here's how the Blue/Green deployment strategy works:

1. **Blue Environment (Current Production):**
   - The currently active environment that is serving live traffic.
   - Represents the current version of the application that users are interacting with.
   - Stable and thoroughly tested.

2. **Green Environment (New Deployment):**
   - The new version of the application that you want to deploy.
   - Essentially a clone of the Blue environment but with the updated codebase.
   - Has undergone thorough testing, including integration and user acceptance testing.

The deployment process typically involves these steps:

1. **Deployment Preparation:**
   - The new version of the application is built, tested, and packaged, ready for deployment.
   - The Green environment is set up with the new version of the application code but is not yet actively serving traffic.

2. **Testing:**
   - The Green environment undergoes rigorous testing to ensure that the new version functions correctly, performs well, and meets all requirements.

3. **Switching Traffic:**
   - Once testing is successful, traffic routing is switched from the Blue environment to the Green environment. This can be done using load balancers or DNS changes.
   - All incoming requests are now directed to the Green environment.

4. **Validation and Monitoring:**
   - The new version of the application is monitored in the Green environment to ensure it's stable and performs as expected under real-world conditions.

5. **Fallback (Rollback):**
   - If issues are detected, you can quickly and easily switch traffic back to the Blue environment. This allows for rapid rollback in case of unexpected problems.

6. **Blue Environment Update:**
   - While the Green environment is actively serving traffic, the Blue environment can be updated, tested, and prepared for the next deployment cycle.

The key benefits of Blue/Green deployment include:

- **Minimal Downtime:** Switching traffic from one environment to another minimizes downtime since the inactive environment is unaffected by deployment-related activities.

- **Reduced Risk:** The active Blue environment remains untouched during deployment, reducing the risk of user-facing issues.

- **Quick Rollback:** If problems occur in the Green environment, switching traffic back to the Blue environment provides an immediate rollback mechanism.

- **Parallel Testing:** Testing can occur in parallel with production traffic, allowing for thorough validation of the new version.

- **Predictable Deployment:** The process is standardized, making deployments more predictable and less error-prone.

It's worth noting that while Blue/Green deployment is an effective strategy, it might not be suitable for all types of applications or organizations. Some applications require more complex strategies, such as canary deployments or feature flags, depending on specific requirements and infrastructure constraints.

==================================================

·     Difference between CloudWatch & CloudTrail?
==================================================

·     Can you recover your key pair when it lost?
==================================================


·     What is horizontal & vertical scaling?
==================================================


·     What is A records in Route53?
==================================================


·     How to maintain state.tf file in terraform?
==================================================


·     What is the purpose of Lambda?
==================================================


·     What are the components of Kubernetes?
==================================================


·     What is the difference between Docker & Kubernetes?
==================================================


·     What you do if Master node gets failed?
==================================================


·     What is the Command for making Zip file & how can we see the contents without unzipping the file?
==================================================


·     What is Active Directory?
==================================================


·     What is difference between I am a role and I am a policy?
==================================================


·     What is Trust policy?
==================================================


·     What is DB parameter group?
==================================================


·     What is bucket policy and ACL?
==================================================


·     What is terraform taint command do?
==================================================


·     What is terraform state file. Why we need it?
==================================================


·     What is RUN and CMD is used in docker file?
==================================================


·     What is difference between Entry point and CMD?
==================================================


·     Which command is used to mount a device or unmount a device?
==================================================


·     How to check device mapping in Linux?
==================================================


·     What will do when our RDS getting shortage of storage, how you will be notified?
==================================================


·     What happen when someone goes to the console and change the instance type which you created from terraform & if you again apply the same file what happen.

==================================================


·     Can you delete Docker container while running state.
==================================================


·     What is Docker daemon?
==================================================


·     What happen if you somehow lost the key pair?
==================================================


·     Difference between NLB & ALB?
==================================================


·     How to automate your instance that it automatically shuts down at 10 pm and open on 5am.
==================================================


·     How you can configure your s3 bucket that every object delete at the end of the day.
==================================================


·     How you can find out that your linux os is physical or virtual?
==================================================


·     What is the other way to connect two vpc instead of vpc peering?
==================================================


·     What is LVM?
==================================================


·     Difference between Security Group and NACL. 
==================================================
