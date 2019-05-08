# ![LOGO](logo.png) trash nothing! **flow**ground Connector

## Description

A generated **flow**ground connector for the trash nothing! API (version 1.0.0).

Generated from: https://api.apis.guru/v2/specs/trashnothing.com/1.0.0/swagger.json<br/>
Generated at: 2019-05-07T17:44:27+03:00

## API Description

This is the REST API for [trashnothing.com](https://trashnothing.com).

To learn more about the API or to register your app for use with the API
visit the [trash nothing! Developer page](https://trashnothing.com/developer).

NOTE: All date-time values are [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time)
and are in [ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601) (eg. 2019-02-03T01:23:53).


## Authorization

Supported authorization schemes:
- API Key- OAuth2
- OAuth2

For OAuth 2.0 you need to specify OAuth Client credentials as environment variables in the connector repository:
* `OAUTH_CLIENT_ID` - your OAuth client id
* `OAUTH_CLIENT_SECRET` - your OAuth client secret

## Actions

### Send feedback

> Allows users to send feedback about the trashnothing.com site or apps.

*Tags:* `misc`

### Search groups

*Tags:* `groups`

#### Input Parameters
* `name` - _optional_ - Find groups that have the given text somewhere in their name (case insensitive).
* `latitude` - _optional_ - Find groups near the given latitude and longitude.
* `longitude` - _optional_ - Find groups near the given latitude and longitude.
* `distance` - _optional_ - When latitude and longitude are passed, distance can optionally be passed to only return groups within a certain distance (in kilometers) from the point specified by the latitude and longitude.  The distance must be > 0 and <= 150 and will default to 100.

* `country` - _optional_ - Find groups in the given country where country is a 2 letter country code for the country (see https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2 ).

* `region` - _optional_ - For countries with regions (AU, CA, GB, US), search groups in a specific region as specified by the region abbreviation.  The supported regions and their abbreviations are listed below. <br /><br /> NOTE: The region and postal_code parameters cannot be used at the same time and if both are passed then the postal_code will take priority. <br /><br /> --- <br /><br /> **AU**<br /> - QLD: Queensland<br /> - SA: South Australia<br /> - TAS: Tasmania<br /> - VIC: Victoria<br /> - WA: Western Australia<br /> - NT: Northern Territory<br /> - NSW: New South Wales - ACT<br /> <br /> **CA**<br /> - AB: Alberta<br /> - BC: British Columbia<br /> - MB: Manitoba<br /> - NB: New Brunswick<br /> - NL: Newfoundland and Labrador<br /> - NS: Nova Scotia<br /> - ON: Ontario<br /> - QC: Quebec<br /> - SK: Saskatchewan<br /> - PE: Prince Edward Island<br /> <br /> **GB**<br /> - E: East<br /> - EM: East Midlands<br /> - LDN: London<br /> - NE: North East<br /> - NW: North West<br /> - NI: Northern Ireland<br /> - SC: Scotland<br /> - SE: South East<br /> - SW: South West<br /> - WA: Wales<br /> - WM: West Midlands<br /> - YH: Yorkshire and the Humber<br /> <br /> **US**<br /> All 50 states and the District of Columbia are supported.  For the abbreviations, see: https://github.com/jasonong/List-of-US-States/blob/master/states.csv

* `postal_code` - _optional_ - Find groups in the given postal code.  Only a few countries support postal code searches (US, CA, AU, GB).  The country parameter must be passed when the postal_code parameter is set. <br /><br /> NOTE: The region and postal_code parameters cannot be used at the same time and if both are passed then the postal_code will take priority.

* `page` - _optional_ - The page of groups to return.
* `per_page` - _optional_ - The number of groups to return per page (must be >= 1 and <= 100).

### Retrieve multiple groups

*Tags:* `groups`

#### Input Parameters
* `group_ids` - _required_ - The IDs of the groups to retrieve.  If more than 20 group IDs are passed, only the first 20 groups will be returned.

### Join groups

> Request membership to one or more groups. <br /><br /> NOTE: Any group with a has_questions field set to true will also require answers to the groups' new member questionnaire to be submitted.  Groups waiting for answers will have their membership field set to 'pending-questions'.  And the questionnaire that needs to be answered can be found in the membership.questionnaire field of the group after a subscribe request is made to that group.

*Tags:* `groups`

### Retrieve a group

*Tags:* `groups`

#### Input Parameters
* `group_id` - _required_ - The ID of the group to retrieve.

### Submit group answers

> Submits answers to a groups' membership questionnaire. <br /><br /> The request body should be a JSON object mapping each question from the group membership.questionnaire.questions field to an answer (eg. {"Where do you live?": "New York City"} ). All questions are required so no null or empty string answers are allowed.

*Tags:* `groups`

#### Input Parameters
* `group_id` - _required_ - The group ID of the group that the user is submitting answers for.

### Contact group moderators

*Tags:* `groups`

#### Input Parameters
* `group_id` - _required_ - The group ID of the group whose moderators will be contacted.

### Leave a group

*Tags:* `groups`

#### Input Parameters
* `group_id` - _required_ - The ID of the group to leave.

### Create a photo

*Tags:* `photos`

### Delete a photo

*Tags:* `photos`

#### Input Parameters
* `photo_id` - _required_

### Retrieve a photo album

> Every post with photos has a photo album associated with the post.   The photo album for a post can be retrieved by passing the photo_id of any photo that is attached to a post. This makes it easier for users edit the photos attached to their post when they are reposting.

*Tags:* `photos`

#### Input Parameters
* `photo_id` - _required_
* `device_pixel_ratio` - _optional_ - Client device pixel ratio used to determine thumbnail size (default 1.0).
* `upload_key` - _optional_ - If set to 1, a new upload_key will be returned to allow the user to alter the photos in the album.

### Rotate a photo

*Tags:* `photos`

#### Input Parameters
* `photo_id` - _required_
* `degrees` - _required_ - Rotation in degrees - currently only 90, 180 and 270 are supported which correspond to rotate left, rotate upside down and rotate right.
* `device_pixel_ratio` - _optional_ - Client device pixel ratio used to determine thumbnail size (default 1.0).

### List posts

> NOTE: Passing the latitude, longitude and radius parameters filters all posts by their location and so these parameters will temporarily override the current users' location preferences. When latitude, longitude and radius are not specified, public posts will be filtered by the current users' location preferences.

*Tags:* `posts`

#### Input Parameters
* `types` - _required_ - A comma separated list of the post types to return.  The available post types are: offer, taken, wanted, received, admin

* `sources` - _required_ - A comma separated list of the post sources to retrieve posts from. The available sources are: groups, trashnothing, open_archive_groups. The trashnothing source is for public posts that are posted on trash nothing but are not associated with any group. The open_archive_groups source provides a way to easily request posts from groups that have open_archives set to true without having to pass a group_ids parameter.  When passed, it will automatically return posts from open archive groups that are within the area specified by the latitude, longitude and radius parameters (or the current users' location if latitude, longitude and radius aren't passed). <br /><br /> NOTE: For requests using an api key instead of oauth, passing the trashnothing source or the open_archive_groups source makes the latitude, longitude and radius parameters required.

* `group_ids` - _optional_ - A comma separated list of the group IDs to retrieve posts from. This parameter is only used if the 'groups' source is passed in the sources parameter and only groups that the current user is a member of or that are open archives groups will be used (the group IDs of other groups will be silently discarded*). <br /><br /> NOTE: For requests using an api key instead of oauth, this field is required if the 'groups' source is passed. In addition, only posts from groups that have open_archives set to true will be used (the group IDS of other groups will be silently discarded*). <br /><br/> *To determine which group IDs were used and which were discarded, use the group_ids field in the response.

* `per_page` - _optional_ - The number of posts to return per page (must be >= 1 and <= 100).
* `page` - _optional_ - The page of posts to return.
* `device_pixel_ratio` - _optional_ - Client device pixel ratio used to determine thumbnail size (default 1.0).
* `latitude` - _optional_ - The latitude of a point around which to return posts.

* `longitude` - _optional_ - The longitude of a point around which to return posts.

* `radius` - _optional_ - The radius in meters of a circle centered at the point defined by the latitude and longitude parameters. When latitude, longitude and radius are passed, only posts within the circle defined by these parameters will be returned.

* `date_min` - _optional_ - Only posts newer than this UTC date and time will be returned.  If unset, defaults to the current date and time minus 90 days.

* `date_max` - _optional_ - Only posts older than this UTC date and time will be returned.  If unset, defaults to the current date and time.
* `satisfied` - _optional_ - Whether or not to return satisfied offer and wanted posts.  This does not affect posts other than offer and wanted posts. If set to '0' (the default), only posts that are not satisfied are returned. If set to '1', only satisfied posts will be returned. If set to 'all', all posts will be returned.


### Submit a post

> Submits a new post. <br /><br /> NOTE: An alternate way to submit posts that does quicker client side validation is to use the script served by the API at the /posts/client.js endpoint (see the description of the /posts/client.js endpoint for usage instructions).

*Tags:* `posts`

### Retrieve client.js

> Defines javascript functions that can be used to validate and submit posts.<br/>
> <br/>
> The advantage of using these functions versus using the post submission endpoint directly is that<br/>
> some of the post validation checks can be done on the client side which will be faster.<br/>
> <br/>
> NOTE: If used, this javascript file MUST be loaded dynamically for each user because the contents<br/>
> of the file are generated dynamically based on the current user.  The file may be cached on a per<br/>
> user basis based on the HTTP cache headers that are returned when the file is requested (currently<br/>
> the cache headers specify that the file should expire after one day).<br/>
> <br/>
> <br/>
> The following functions are available:<br/>
> <br/>
> ---<br/>
> <br/>
> **window.TN.check_crossposting_restrictions(group_ids)**<br/>
> <br/>
> Checks for crossposting restrictions when the user selects more than one group to post to.<br/>
> <br/>
> Parameters:<br/>
> - **group_ids** is an array of group IDs<br/>
> <br/>
> Returns an object with three properties {allowed, restricted, restrictions}.<br/>
> <br/>
> - **allowed** is an array of the group IDs from group_ids that can be crossposted to<br/>
> <br/>
> - **restricted** is an array of the group IDs from group_ids that can't be crossposted to<br/>
> <br/>
> - **restrictions** is an object mapping group IDs that have crossposting restrictions to arrays of group IDs that are restricted.<br/>
>   It is useful for pinpointing why a group ID shows up in the restricted array so that users can be provided feedback<br/>
>   about the reason for the crossposting restriction (eg. a message like 'group A doesn't allow crossposting to group B').<br/>
> <br/>
> For example, given group_ids = [1, 2, 3, 4] and assuming group 1 doesn't allow posting to group 3 and group 2 doesn't allow<br/>
> posting to group 1, the returned object will be:<br/>
> <br/>
> {allowed: [4], restricted: [1, 2, 3], restrictions: {1: [3], 2: [1]}}<br/>
> <br/>
> <br/>
> ---<br/>
> <br/>
> **window.TN.submit_post(args, session, preferences, callback)**<br/>
> <br/>
> Submits a new post and performs validation checks on the post before it is accepted for submission.<br/>
> <br/>
> Parameters:<br/>
> <br/>
> - **args** is an object containing data about the post being submitted and must include<br/>
>   the following properties:<br/>
> <br/>
>   - type: The type of post.  One of: offer, wanted<br/>
>   - title: A short description of the item(s).<br/>
>   - location: A short location description.<br/>
> <br/>
>   The following properties are optional:<br/>
> <br/>
>   - content: A longer description of the item(s).<br/>
>   - group_ids: An array of group IDs to submit the post to (if any).<br/>
>   - fair_offer: If set to 1, the post will be posted with the Fair Offer Policy (only valid for offer posts - see https://trashnothing.com/fair_offer_policy ).<br/>
>   - upload_key: The key used to upload any photos that should be attached to this post.<br/>
>   - latitude<br/>
>   - longitude<br/>
> <br/>
> - **session** is a temporary object that is used by submit_post to store data about the submission<br/>
>   process for a single post.  The first time submit_post is called with a post, session should<br/>
>   be a new empty object (eg. {}).  The session object should be persisted until that post<br/>
>   is successfully submitted and then it can be discarded so that the next post will start<br/>
>   over with a new empty session object.  <br/>
> <br/>
> - **preferences** is a permanent object that the client persists and modifies based on warnings returned<br/>
>   by the post submission process and user input.  Some post warnings passed to the callback object<br/>
>   have a preference_key string property so that users can opt out of those warnings in the future.<br/>
>   To save this opt-out preference, set the property indicated by the preference_key in the preferences<br/>
>   object (eg. preferences[preference_key] = 1).  The preferences object is only read by submit_post and<br/>
>   never modified - it is up to the client to initialize, modify and persist the preferences object.<br/>
> <br/>
> - **callback** is a function used to return the result of the post submission. It is called and passed<br/>
>   one argument - an object with five properties {result, message, preference_key, identifier, session}.<br/>
>   The result property is a string that is one of: success, error, warning.  The identifier property is<br/>
>   set for errors and warnings and will contain a string that represents the type of error or warning that<br/>
>   occurred.<br/>
> <br/>
>   A success result indicates that the post was submitted successfully. Note that posts may not<br/>
>   appear instantly after submission because the moderators of many groups may have additional<br/>
>   automatic or manual review processes in place that can delay the publishing of a post.<br/>
>   <br/>
>   An error result indicates that there is an error with the post to show the user and the message property<br/>
>   will contain text describing the error.<br/>
> <br/>
>   A warning result indicates that there is a warning about the post to show the user and the<br/>
>   message property will contain a string describing the warning.  A warning result doesn't prevent a post from<br/>
>   being submitted, to continue the submission process after a warning result, just re-submit the post<br/>
>   (with the updated session object) to temporarily override that specific warning.<br/>
> <br/>
>   Certain types of warnings can be opted out of.  These warnings will set preference_key to a string that can be <br/>
>   set in the preferences object by the client to opt out of that type of warning in the future (see the description<br/>
>   of the preferences parameter for more details).

*Tags:* `posts`

#### Input Parameters
* `group_ids` - _required_ - A comma separated list of all the group IDs that the current user is a member of. If the current user is not a member of any groups, simply pass an empty string.

* `callback` - _optional_ - The name of a global function to call once the script is loaded.
* `access_token` - _required_ - Passing the current users' OAuth2 access token as a GET parameter makes it easier to load this script in a normal HTML <script> tag.


### Retrieve multiple posts

*Tags:* `posts`

#### Input Parameters
* `post_ids` - _required_ - The IDs of the posts to retrieve.  If more than 10 post IDs are passed, only the first 10 posts will be returned.

### Search posts

> Searching posts takes the same arguments as listing posts except for the addition of the search and sort_by parameters.

*Tags:* `posts`

#### Input Parameters
* `search` - _required_ - The search query used to find posts.
* `sort_by` - _optional_ - How to sort the posts that are returned.  One of: relevance, date <br /><br /> Setting sort_by to date will sort posts from newest to oldest.

* `types` - _required_ - A comma separated list of the post types to return.  The available post types are: offer, taken, wanted, received, admin

* `sources` - _required_ - A comma separated list of the post sources to retrieve posts from. The available sources are: groups, trashnothing, open_archive_groups. The trashnothing source is for public posts that are posted on trash nothing but are not associated with any group. The open_archive_groups source provides a way to easily request posts from groups that have open_archives set to true without having to pass a group_ids parameter.  When passed, it will automatically return posts from open archive groups that are within the area specified by the latitude, longitude and radius parameters (or the current users' location if latitude, longitude and radius aren't passed). <br /><br /> NOTE: For requests using an api key instead of oauth, passing the trashnothing source or the open_archive_groups source makes the latitude, longitude and radius parameters required.

* `group_ids` - _optional_ - A comma separated list of the group IDs to retrieve posts from. This parameter is only used if the 'groups' source is passed in the sources parameter and only groups that the current user is a member of or that are open archives groups will be used (the group IDs of other groups will be silently discarded*). <br /><br /> NOTE: For requests using an api key instead of oauth, this field is required if the 'groups' source is passed. In addition, only posts from groups that have open_archives set to true will be used (the group IDS of other groups will be silently discarded*). <br /><br/> *To determine which group IDs were used and which were discarded, use the group_ids field in the response.

* `per_page` - _optional_ - The number of posts to return per page (must be >= 1 and <= 100).
* `page` - _optional_ - The page of posts to return.
* `device_pixel_ratio` - _optional_ - Client device pixel ratio used to determine thumbnail size (default 1.0).
* `latitude` - _optional_ - The latitude of a point around which to return posts.

* `longitude` - _optional_ - The longitude of a point around which to return posts.

* `radius` - _optional_ - The radius in meters of a circle centered at the point defined by the latitude and longitude parameters. When latitude, longitude and radius are passed, only posts within the circle defined by these parameters will be returned.

* `date_min` - _optional_ - Only posts newer than this UTC date and time will be returned.  If unset, defaults to the current date and time minus 90 days.

* `date_max` - _optional_ - Only posts older than this UTC date and time will be returned.  If unset, defaults to the current date and time.
* `satisfied` - _optional_ - Whether or not to return satisfied offer and wanted posts.  This does not affect posts other than offer and wanted posts. If set to '0' (the default), only posts that are not satisfied are returned. If set to '1', only satisfied posts will be returned. If set to 'all', all posts will be returned.


### Retrieve a post

*Tags:* `posts`

#### Input Parameters
* `post_id` - _required_ - The ID of the post to retrieve.

### Retrieve post display data

> Retrieve a post and other data related to the post that is useful for displaying the post such as data about the user who posted the post and the groups the post was posted on.

*Tags:* `posts`

#### Input Parameters
* `post_id` - _required_ - The ID of the post to retrieve.

### Flag a post

> Flags a post to be reviewed by the moderators.

*Tags:* `posts`

#### Input Parameters
* `post_id` - _required_

### Map a post

> Map a post to a specific location when the post is missing a location or has an incorrect location.

*Tags:* `posts`

#### Input Parameters
* `post_id` - _required_ - The ID of the post to geolocate.

### Reply to a post

> Send a reply to a post from the current user to the post author.

*Tags:* `posts`

#### Input Parameters
* `post_id` - _required_ - The ID of the post to reply to.

### Satisfy a post

> Mark an offer or wanted post by the current user as satisfied (eg. an offer has been taken or a wanted has been received).

*Tags:* `posts`

#### Input Parameters
* `post_id` - _required_ - The ID of the post to satisfy.

### Retrieve post share content

> Retrieve text and html content useful for sharing a post by email.

*Tags:* `posts`

#### Input Parameters
* `post_id` - _required_ - The ID of the post to share.

### Share a post

> Forwards a copy of the post to the current user so that they can forward it to friends.

*Tags:* `posts`

#### Input Parameters
* `post_id` - _required_ - The ID of the post to share.

### Retrieve current user

*Tags:* `users`

### Update current user

> Update the current user.  All fields are optional so requests can update just one or multiple user properties at a time.

*Tags:* `users`

### List current users' email alerts

*Tags:* `users`

### Create an email alert

*Tags:* `users`

### Delete an email alert

*Tags:* `users`

#### Input Parameters
* `alert_id` - _required_ - The ID of the email alert to delete.

### Change email address

> Change the users' current email address.  A verification link will be emailed to the new email address to verify that the email account belongs to the user.  The email change will not take effect until the user clicks the link in the verification email.

*Tags:* `users`

### Set users' email address as not bouncing

> Resets an email address bouncing state to false.  The users' email address may be automatically marked as bouncing again if further emails sent to it are bounced.

*Tags:* `users`

### List current users' groups

*Tags:* `users`

#### Input Parameters
* `membership` - _optional_ - Set the membership parameter to only return certain groups. The options are: <br /><br /> - **subscribed**: Only return groups the user is a member of.<br /> - **pending-questions**: Only return groups where the user needs to respond to a new member questionnaire.<br /> - **pending**: Only return groups where the user is waiting for their membership request to be approved (excludes groups which are pending-questions). <br /><br /> If unset, all groups the user is a member of and pending membership on will be returned.


### Update location

> Update the current users' location. The location is used to determine which posts are shown to the user (both public posts and group posts).

*Tags:* `users`

### List current users' group notices

*Tags:* `users`

#### Input Parameters
* `group_ids` - _optional_ - A comma separated list of group IDs to return notices for.  If unset, notices for all the users groups will be returned.

### List current users' posts

> NOTE: In order to make it easier to see all a users&#39; posts, the current users&#39; location preferences are not applied when listing or searching posts from a single user.  If location based filtering of the posts is needed, the latitude, longitude and radius parameters may be used.

*Tags:* `users`

#### Input Parameters
* `types` - _required_ - A comma separated list of the post types to return.  The available post types are: offer, taken, wanted, received, admin

* `sources` - _required_ - A comma separated list of the post sources to retrieve posts from. The available sources are: groups, trashnothing, open_archive_groups. The trashnothing source is for public posts that are posted on trash nothing but are not associated with any group. The open_archive_groups source provides a way to easily request posts from groups that have open_archives set to true without having to pass a group_ids parameter.  When passed, it will automatically return posts from open archive groups that are within the area specified by the latitude, longitude and radius parameters (or the current users' location if latitude, longitude and radius aren't passed). <br /><br /> NOTE: For requests using an api key instead of oauth, passing the trashnothing source or the open_archive_groups source makes the latitude, longitude and radius parameters required.

* `group_ids` - _optional_ - A comma separated list of the group IDs to retrieve posts from. This parameter is only used if the 'groups' source is passed in the sources parameter and only groups that the current user is a member of or that are open archives groups will be used (the group IDs of other groups will be silently discarded*). <br /><br /> NOTE: For requests using an api key instead of oauth, this field is required if the 'groups' source is passed. In addition, only posts from groups that have open_archives set to true will be used (the group IDS of other groups will be silently discarded*). <br /><br/> *To determine which group IDs were used and which were discarded, use the group_ids field in the response.

* `per_page` - _optional_ - The number of posts to return per page (must be >= 1 and <= 100).
* `page` - _optional_ - The page of posts to return.
* `device_pixel_ratio` - _optional_ - Client device pixel ratio used to determine thumbnail size (default 1.0).
* `latitude` - _optional_ - The latitude of a point around which to return posts.

* `longitude` - _optional_ - The longitude of a point around which to return posts.

* `radius` - _optional_ - The radius in meters of a circle centered at the point defined by the latitude and longitude parameters. When latitude, longitude and radius are passed, only posts within the circle defined by these parameters will be returned.

* `date_min` - _optional_ - Only posts newer than this UTC date and time will be returned.

* `date_max` - _optional_ - Only posts older than this UTC date and time will be returned.
* `satisfied` - _optional_ - Whether or not to return satisfied offer and wanted posts.  This does not affect posts other than offer and wanted posts. If set to '0' (the default), only posts that are not satisfied are returned. If set to '1', only satisfied posts will be returned. If set to 'all', all posts will be returned.


### Search current users' posts

> Searching posts takes the same arguments as listing posts except for the addition of the search and sort_by parameters.

*Tags:* `users`

#### Input Parameters
* `search` - _required_ - The search query used to find posts.
* `sort_by` - _optional_ - How to sort the posts that are returned.  One of: relevance, date <br /><br /> Setting sort_by to date will sort posts from newest to oldest.

* `types` - _required_ - A comma separated list of the post types to return.  The available post types are: offer, taken, wanted, received, admin

* `sources` - _required_ - A comma separated list of the post sources to retrieve posts from. The available sources are: groups, trashnothing, open_archive_groups. The trashnothing source is for public posts that are posted on trash nothing but are not associated with any group. The open_archive_groups source provides a way to easily request posts from groups that have open_archives set to true without having to pass a group_ids parameter.  When passed, it will automatically return posts from open archive groups that are within the area specified by the latitude, longitude and radius parameters (or the current users' location if latitude, longitude and radius aren't passed). <br /><br /> NOTE: For requests using an api key instead of oauth, passing the trashnothing source or the open_archive_groups source makes the latitude, longitude and radius parameters required.

* `group_ids` - _optional_ - A comma separated list of the group IDs to retrieve posts from. This parameter is only used if the 'groups' source is passed in the sources parameter and only groups that the current user is a member of or that are open archives groups will be used (the group IDs of other groups will be silently discarded*). <br /><br /> NOTE: For requests using an api key instead of oauth, this field is required if the 'groups' source is passed. In addition, only posts from groups that have open_archives set to true will be used (the group IDS of other groups will be silently discarded*). <br /><br/> *To determine which group IDs were used and which were discarded, use the group_ids field in the response.

* `per_page` - _optional_ - The number of posts to return per page (must be >= 1 and <= 100).
* `page` - _optional_ - The page of posts to return.
* `device_pixel_ratio` - _optional_ - Client device pixel ratio used to determine thumbnail size (default 1.0).
* `latitude` - _optional_ - The latitude of a point around which to return posts.

* `longitude` - _optional_ - The longitude of a point around which to return posts.

* `radius` - _optional_ - The radius in meters of a circle centered at the point defined by the latitude and longitude parameters. When latitude, longitude and radius are passed, only posts within the circle defined by these parameters will be returned.

* `date_min` - _optional_ - Only posts newer than this UTC date and time will be returned.

* `date_max` - _optional_ - Only posts older than this UTC date and time will be returned.
* `satisfied` - _optional_ - Whether or not to return satisfied offer and wanted posts.  This does not affect posts other than offer and wanted posts. If set to '0' (the default), only posts that are not satisfied are returned. If set to '1', only satisfied posts will be returned. If set to 'all', all posts will be returned.


### List current users' profile images

*Tags:* `users`

### Resend account verification email

*Tags:* `users`

### Send password reset email

*Tags:* `users`

### Report a user

*Tags:* `users`

### Retrieve a user

*Tags:* `users`

#### Input Parameters
* `user_id` - _required_ - A user ID.

### List posts by a user

> NOTE: In order to make it easier to see all a users&#39; posts, the current users&#39; location preferences are not applied when listing or searching posts from a single user.  If location based filtering of the posts is needed, the latitude, longitude and radius parameters may be used.

*Tags:* `users`

#### Input Parameters
* `user_id` - _required_ - The user ID of the user whose posts will be retrieved. Using 'me' as the user_id will return the posts for the current user.

* `types` - _required_ - A comma separated list of the post types to return.  The available post types are: offer, taken, wanted, received, admin

* `sources` - _required_ - A comma separated list of the post sources to retrieve posts from. The available sources are: groups, trashnothing, open_archive_groups. The trashnothing source is for public posts that are posted on trash nothing but are not associated with any group. The open_archive_groups source provides a way to easily request posts from groups that have open_archives set to true without having to pass a group_ids parameter.  When passed, it will automatically return posts from open archive groups that are within the area specified by the latitude, longitude and radius parameters (or all the open archive groups the requested user has posted to if latitude, longitude and radius aren't passed). <br /><br /> NOTE: For requests using an api key instead of oauth, passing the trashnothing source or the open_archive_groups source makes the latitude, longitude and radius parameters required.

* `group_ids` - _optional_ - A comma separated list of the group IDs to retrieve posts from. This parameter is only used if the 'groups' source is passed in the sources parameter and only groups that the current user is a member of or that are open archives groups will be used (the group IDs of other groups will be silently discarded*). <br /><br /> NOTE: For requests using an api key instead of oauth, this field is required if the 'groups' source is passed. In addition, only posts from groups that have open_archives set to true will be used (the group IDS of other groups will be silently discarded*). <br /><br/> *To determine which group IDs were used and which were discarded, use the group_ids field in the response.

* `per_page` - _optional_ - The number of posts to return per page (must be >= 1 and <= 100).
* `page` - _optional_ - The page of posts to return.
* `device_pixel_ratio` - _optional_ - Client device pixel ratio used to determine thumbnail size (default 1.0).
* `latitude` - _optional_ - The latitude of a point around which to return posts.

* `longitude` - _optional_ - The longitude of a point around which to return posts.

* `radius` - _optional_ - The radius in meters of a circle centered at the point defined by the latitude and longitude parameters. When latitude, longitude and radius are passed, only posts within the circle defined by these parameters will be returned.

* `date_min` - _optional_ - Only posts newer than this UTC date and time will be returned.

* `date_max` - _optional_ - Only posts older than this UTC date and time will be returned.
* `satisfied` - _optional_ - Whether or not to return satisfied offer and wanted posts.  This does not affect posts other than offer and wanted posts. If set to '0' (the default), only posts that are not satisfied are returned. If set to '1', only satisfied posts will be returned. If set to 'all', all posts will be returned.


### Search posts by a user

> Searching posts takes the same arguments as listing posts except for the addition of the search and sort_by parameters.

*Tags:* `users`

#### Input Parameters
* `user_id` - _required_ - The user ID of the user whose posts will be retrieved. Using 'me' as the user_id will return the posts for the current user.

* `search` - _required_ - The search query used to find posts.
* `sort_by` - _optional_ - How to sort the posts that are returned.  One of: relevance, date <br /><br /> Setting sort_by to date will sort posts from newest to oldest.

* `types` - _required_ - A comma separated list of the post types to return.  The available post types are: offer, taken, wanted, received, admin

* `sources` - _required_ - A comma separated list of the post sources to retrieve posts from. The available sources are: groups, trashnothing, open_archive_groups. The trashnothing source is for public posts that are posted on trash nothing but are not associated with any group. The open_archive_groups source provides a way to easily request posts from groups that have open_archives set to true without having to pass a group_ids parameter.  When passed, it will automatically return posts from open archive groups that are within the area specified by the latitude, longitude and radius parameters (or all the open archive groups the requested user has posted to if latitude, longitude and radius aren't passed). <br /><br /> NOTE: For requests using an api key instead of oauth, passing the trashnothing source or the open_archive_groups source makes the latitude, longitude and radius parameters required.

* `group_ids` - _optional_ - A comma separated list of the group IDs to retrieve posts from. This parameter is only used if the 'groups' source is passed in the sources parameter and only groups that the current user is a member of or that are open archives groups will be used (the group IDs of other groups will be silently discarded*). <br /><br /> NOTE: For requests using an api key instead of oauth, this field is required if the 'groups' source is passed. In addition, only posts from groups that have open_archives set to true will be used (the group IDS of other groups will be silently discarded*). <br /><br/> *To determine which group IDs were used and which were discarded, use the group_ids field in the response.

* `per_page` - _optional_ - The number of posts to return per page (must be >= 1 and <= 100).
* `page` - _optional_ - The page of posts to return.
* `device_pixel_ratio` - _optional_ - Client device pixel ratio used to determine thumbnail size (default 1.0).
* `latitude` - _optional_ - The latitude of a point around which to return posts.

* `longitude` - _optional_ - The longitude of a point around which to return posts.

* `radius` - _optional_ - The radius in meters of a circle centered at the point defined by the latitude and longitude parameters. When latitude, longitude and radius are passed, only posts within the circle defined by these parameters will be returned.

* `date_min` - _optional_ - Only posts newer than this UTC date and time will be returned.

* `date_max` - _optional_ - Only posts older than this UTC date and time will be returned.
* `satisfied` - _optional_ - Whether or not to return satisfied offer and wanted posts.  This does not affect posts other than offer and wanted posts. If set to '0' (the default), only posts that are not satisfied are returned. If set to '1', only satisfied posts will be returned. If set to 'all', all posts will be returned.


### Retrieve a users' profile image

> This is designed to be used as the src attribute of an HTML &lt;img&gt; tag to show the profile image of the given user.

*Tags:* `users`

#### Input Parameters
* `user_id` - _required_ - The user ID of the user to return the profile image of.
* `default` - _optional_ - A default image URL to use when the user has no profile image. Or to use one of the Gravatar default images, you can set default to any one of (404, mm, identicon, monsterid, wavatar, retro, blank). <br /><br /> To learn how the Gravatar default images options work, see the Default Image section on the page at:<br /> https://en.gravatar.com/site/implement/images/


## License

**flow**ground :- Telekom iPaaS / trashnothing-com-connector<br/>
Copyright © 2019, [Deutsche Telekom AG](https://www.telekom.de)<br/>
contact: flowground@telekom.de

All files of this connector are licensed under the Apache 2.0 License. For details
see the file LICENSE on the toplevel directory.
