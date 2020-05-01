# Create a content type

As a site visitor, I want to see FAQ items on the website so that I can find answers to questions. 

Scenario 1: Content Type exists in Drupal Spec Tool 
 As a site admin,
 When I am looking at the [Drupal Spec tool](https://docs.google.com/spreadsheets/d/18nolqFkp1dY_fGm4YGjmHzrktu3blMyDRnyH-iL5mU8/edit#gid=858986005) 
 then I will see a FAQ content type and all associated fields
 
Scenario 2: Site is updated according to Drupal Spec tool
 As a site admin,
 When I am looking at the website 
 then I will see all fields and specs according to the Drupal Spec tool
 
Exercise 
Step one: Review Drupal Spec tool 
() Take note of the bundle and fields associated to the FAQ content type.
  
Step two: log into your local drupal site
`cd [your-path]/sites/dev-assessment`

Step three: navigate to Content types
`/admin/structure/types`

Step four: Add a new content type
() Name: FAQ
() Display settings: uncheck Display author and date information
() Save and manage fields 

Step Five: Add fields based on spec tool. 
Review [Drupal Spec tool](https://docs.google.com/spreadsheets/d/18nolqFkp1dY_fGm4YGjmHzrktu3blMyDRnyH-iL5mU8/edit#gid=858986005) and add all fields associated with FAQ.
