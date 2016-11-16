Retention Policies
======

A retention policy blocks permanent deletion of content for a specified amount of time. Admins can create retention policies and then later assign them to specific folders or their entire enterprise.

* [Create Retention Policy](#create-retention-policy)
* [Get Retention Policy](#get-retention-policy)
* [Update Retention Policy](#update-retention-policy)
* [Get Retention Policies](#get-retention-policies)
<<<<<<< HEAD
=======
* [Get Retention Policy Assignments](#get-retention-policy-assignments)
* [Create Retention Policy Assignment](#create-retention-policy-assignment)
* [Get Retention Policy Assignment](#get-retention-policy-assignment)

>>>>>>> 93a87a7281c9cc3703b228eaa937a0599c32a4c3

Create Retention Policy
--------------

The static [`createIndefinitePolicy(BoxAPIConnection, String)`][create-indefinite-retention-policy] method will let you create a new indefinite retention policy with a specified name.

```java
BoxRetentionPolicy.createIndefinitePolicy(api, name);
```

The static [`createFinitePolicy(BoxAPIConnection, String, int, String)`][create-finite-retention-policy] method will let you create a new finite retention policy with a specified name, amount of time to apply the retention policy (in days) and a disposition action. the disposition action can be "permanently_delete" or "remove_retention".

```java
BoxRetentionPolicy.createFinitePolicy(api, name, length, action);
```

[create-indefinite-retention-policy]: http://opensource.box.com/box-java-sdk/javadoc/com/box/sdk/BoxRetentionPolicy.html#createIndefinitePolicy(com.box.sdk.BoxAPIConnection,%20java.lang.String)
[create-finite-retention-policy]: http://opensource.box.com/box-java-sdk/javadoc/com/box/sdk/BoxRetentionPolicy.html#createIndefinitePolicy(com.box.sdk.BoxAPIConnection,%20java.lang.String,%20java.lang.int,%20java.lang.String)

Get Retention Policy
--------------

Calling [`getInfo(String...)`][get-info] will return a BoxRetentionPolicy.Info object containing information about the retention policy. If necessary to retrieve limited set of fields, it is possible to specify them using param.

```java
BoxRetentionPolicy policy = new BoxRetentionPolicy(api, id);
policy.getInfo("policy_name", "status");
```

[get-info]: http://opensource.box.com/box-java-sdk/javadoc/com/box/sdk/BoxRetentionPolicy.html#getInfo(java.lang.String...)

Update Retention Policy
--------------

Updating a retention policy's information is done by calling [`updateInfo(BoxRetentionPolicy.Info)`][update-info].

```java
BoxRetentionPolicy policy = new BoxRetentionPolicy(api, id);
BoxRetentionPolicy.Info policyInfo = policy.new Info();
policyInfo.addPendingChange("policy_name", "new policy name");
policy.updateInfo(policyInfo);
```

[update-info]: http://opensource.box.com/box-java-sdk/javadoc/com/box/sdk/BoxRetentionPolicy.html#updateInfo(com.box.sdk.BoxRetentionPolicy.Info)

Get Retention Policies
--------------

Calling the static [`getAll(BoxAPIConnection, String...)`][get-retention-policies] will return an iterable that will page through all of the retention policies.
It is possible to specify filter for the name of retention policy, filter for the type of the policy, filter for the id of user, limit of items per single response and fields to retrieve by calling the static [`getAll(String, String, String, int, BoxAPIConnection, String...)`][get-retention-policies-with-fields] method.

```java
Iterable<BoxRetentionPolicy.Info> policies = BoxRetentionPolicy.getAll(api);
for (BoxRetentionPolicy.Info policyInfo : policies) {
	// Do something with the retention policy.
}
```

[get-retention-policies]: http://opensource.box.com/box-java-sdk/javadoc/com/box/sdk/BoxRetentionPolicy.html#getAll(com.box.sdk.BoxAPIConnection,%20java.lang.String...)

[get-retention-policies-with-fields]: http://opensource.box.com/box-java-sdk/javadoc/com/box/sdk/BoxRetentionPolicy.html#getAll(java.lang.String,%20java.lang.String,%20java.lang.String,%20int,%20com.box.sdk.BoxAPIConnection,%20java.lang.String...)

Get Retention Policy Assignments
--------------

Calling [`getAllAssignments(String...)`][get-all-assignments] will return an iterable that will page through all of the assignments of the retention policy. It is possible to specify maximum number of items per single response and fields to retrieve by calling [`getFolderAssignments(int, String...)`][get-all-assignments-with-params].
If it is necessary to retrieve only assignments of certain type, you can call [`getFolderAssignments(int, String...)`][get-folder-assignments] or [`getEnterpriseAssignments(int, String...)`][get-enterprise-assignments].

```java
BoxRetentionPolicy policy = new BoxRetentionPolicy(api, id);
Iterable<BoxRetentionPolicyAssignment.Info> allAssignments = BoxRetentionPolicy.getAllAssignments("assigned_by");
Iterable<BoxRetentionPolicyAssignment.Info> folderAssignments = BoxRetentionPolicy.getFolderAssignments(50, "assigned_by");
Iterable<BoxRetentionPolicyAssignment.Info> enterpriseAssignments = BoxRetentionPolicy.getEnterpriseAssignments();
for (BoxRetentionPolicyAssignments.Info assignmentInfo : allAssignments) {
	// Do something with the assignment.
}
for (BoxRetentionPolicyAssignments.Info assignmentInfo : folderAssignments) {
	// Do something with the assignment.
}
for (BoxRetentionPolicyAssignments.Info assignmentInfo : enterpriseAssignments) {
	// Do something with the assignment.
}
```

[get-all-assignments]: http://opensource.box.com/box-java-sdk/javadoc/com/box/sdk/BoxRetentionPolicy.html#getAllAssignments(java.lang.String...)
[get-all-assignments-with-params]: http://opensource.box.com/box-java-sdk/javadoc/com/box/sdk/BoxRetentionPolicy.html#getAllAssignments(int,%20java.lang.String...)
[get-folder-assignments]: http://opensource.box.com/box-java-sdk/javadoc/com/box/sdk/BoxRetentionPolicy.html#getFolderAssignments(int,%20java.lang.String...)
[get-enterprise-assignments]: http://opensource.box.com/box-java-sdk/javadoc/com/box/sdk/BoxRetentionPolicy.html#getEnterpiseAssignments(int,%20java.lang.String...)

Create Retention Policy Assignment
--------------
To create new retention policy assignment call [`assignTo(BoxFolder)`][create-assignment] method, or [`assignToEnterprise()`][create-assignment-to-enterprise] to assign retention policy to enterprise.

```java
BoxRetentionPolicy policy = new BoxRetentionPolicy(api, policyID);
BoxRetentionPolicyAssignment.Info enterpriseAssignmentInfo = policy.assignToEnterprise();
BoxFolder folder = new BoxFolder(api, folderID);
BoxRetentionPolicyAssignment.Info folderAssignmentInfo = policy.assignTo(folder);
```

[create-assignment]: http://opensource.box.com/box-java-sdk/javadoc/com/box/sdk/BoxRetentionPolicy.html#assignTo(com.box.sdk.BoxFolder)
[create-assignment-to-enterprise]: http://opensource.box.com/box-java-sdk/javadoc/com/box/sdk/BoxRetentionPolicy.html#assignToEnterprise()

Get Retention Policy Assignment
--------------

Calling [`getInfo(String...)`][get-assignment] will return a BoxRetentionPolicyAssignment.Info object containing information about the retention policy assignment.

```java
BoxRetentionPolicyAssignment assignment = new BoxRetentionPolicyAssignment(api, id);
BoxRetentionPolicyAssignment.Info assignmentInfo = assignment.getInfo("assigned_to");
```

[get-assignment]: http://opensource.box.com/box-java-sdk/javadoc/com/box/sdk/BoxRetentionPolicyAssignment.html#getInfo(java.lang.String...)
