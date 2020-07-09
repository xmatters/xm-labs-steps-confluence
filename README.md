# Confluence Steps

This step allows you to post content to Confluence.


---------

<kbd>
  <img src="https://github.com/xmatters/xMatters-Labs/raw/master/media/disclaimer.png">
</kbd>

---------

# Files

* [ConfluenceSteps.zip](ConfluenceSteps.zip) - Workflow zip file with the step and example flow
* [confluence.png](/confluence.png) - Confluence logo

# How it works
This step posts content to Confluence. By default, it posts content as the **storage** type. It uses [this](https://developer.atlassian.com/cloud/confluence/rest/#api-api-content-post) API call.

The Post Content step can be used for both making pages and comments, as well as other types.

# Installation

## Confluence Setup
1. Create an API Token [here](https://id.atlassian.com/manage-profile/security/api-tokens), this will be used in xMatters later.
2. Find the Key of the space you want to use. This can be found in the URL after `/spaces/` or in the space's settings.


## xMatters Setup
1. Download the [ConfluenceSteps.zip](ConfluenceSteps.zip) file onto your local computer
2. Navigate to the Workflows tab of your xMatters instance
3. Click Import, and select the zip file you just downloaded
4. Create an endpoint for confluence. (e.g. `https://demo.atlassian.net`). The endpoint authentication should be **Basic** with your email as the username, and API Token as the password.


## Usage
The **Confluence - Create Page**, **Confluence - Post Comment**, and **Confluence - Get Content** steps are now available in your custom steps. So navigate to the appropriate canvas so you can add the step there. If you'd like to experiment with it, the **Post Content** workflow has a canvas that can be triggered via HTTP call. 

Confluence supports markdown. It can be used in the **Body** input when creating a new page. For more information on the syntax check out [this](https://confluence.atlassian.com/doc/confluence-wiki-markup-251003035.html) document.

## Confluence - Create Page [/wiki/rest/api/content](https://developer.atlassian.com/cloud/confluence/rest/#api-api-content-post)

### Inputs
| Name  | Required? | Min | Max | Help Text | Default Value | Multiline |
| ----- | ----------| --- | --- | --------- | ------------- | --------- |
| Title | Yes | 0 | 255 | Title of content | | No |
| Space Key | Yes | 0 | 2000 | Key of Space. Found in Space Settings or in the URL. | | No |
| Body | Yes | 0 | 20000 | The body of the new content. | | Yes |
| Status | No | 0 | 2000 | The status of the new content. | | No |
| Ancestor ID | No | 0 | 2000 | The parent content id of the new content. | | No |
| Draft ID | No | 0 | 2000 | The ID of the draft content. Required when publishing a draft. | | No |
| Raw Body | No | 0 | 20000 | Overrides Body input. Gives more freedom over the contents of the body. | | Yes |

An example of using the `Raw Body` input would be: `{"storage": {"value":"hello world", "representation":"storage"}}`

### Outputs

| Name | Description |
| ---- | ----------  |
| Success | Success of step, either (true) or (false) |
| json | JSON output from API Call |
| ID | ID of content |


## Confluence - Get Page [/wiki/rest/api/content/{id}](https://developer.atlassian.com/cloud/confluence/rest/#api-api-content-id-get) or [/wiki/rest/api/content](https://developer.atlassian.com/cloud/confluence/rest/#api-api-content-get)

### Inputs

| Name  | Required? | Min | Max | Help Text | Default Value | Multiline |
| ----- | ----------| --- | --- | --------- | ------------- | --------- |
| ID | No | 0 | 20000 | The ID of the content to be returned. If this is unknown, use the Title and Space inputs. | | Yes |
| Space | No | 0 | 2000 | Key of Space. Found in Space Settings or in the URL. | | No |
| Title | No | 0 | 255 | Title of content | | No |

Either the ID or both Space and Title inputs are required for the step to succeed.

### Outputs

| Name | Description |
| ---- | ----------  |
| Success | Success of step, either (true) or (false) |
| json | JSON output from API Call |
| URL | URL to content |
| ID | ID of content |
| body | body of content |


## Confluence - Post Comment [/wiki/rest/api/content](https://developer.atlassian.com/cloud/confluence/rest/#api-api-content-post)

### Inputs

| Name  | Required? | Min | Max | Help Text | Default Value | Multiline |
| ----- | ----------| --- | --- | --------- | ------------- | --------- |
| Parent ID | Yes | 0 | 20000 | ID of content that comment is on | | Yes |
| Body | Yes | 0 | 255 | Comment Body | | No |

### Outputs

| Name | Description |
| ---- | ----------  |
| Success | Success of step, either (true) or (false) |
| json | JSON output from API Call |
| ID | ID of comment |


## Example
This is an example of the **Confluence - Post Content** step being run after an HTTP trigger is called.

<kbd>
	<img src="/media/ExampleFlow.png">
</kbd>

