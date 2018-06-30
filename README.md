# SObjectNode
SObjectNode can be used  to create a tree for any Salesforce parent/child object structure


//Role Hierarchy Example


//Get Parent Role

UserRole parentRole = [SELECT DeveloperName,Id,Name,ParentRoleId FROM UserRole where ParentRoleId = null LIMIT 1];

List<UserRole> roles = [SELECT DeveloperName,Id,Name,ParentRoleId FROM UserRole where ParentRoleId != null];


//Set parent to node

SObjectNode parentRoleNode = new SObjectNode(parentRole);



//Populate childern - Pass Child, Parent, and parent identifier field

SObjectNode.addChildren(roles, parentRoleNode, 'ParentRoleId');



//Test it out

//Create a path(track) to store results of our search

List<SObjectNode> track = new List<SObjectNode>();



//Start at parent node node and find a particular role ID. Pass path(track) variable

SObjectNode.searchNoChildren(parentRoleNode, '00E31000000esfA', track);



//See path 

System.debug(track);



//See reverse path

List<SObjectNode> reverseTrack = SObjectNode.reversePath(track); 

System.debug(reverseTrack);
