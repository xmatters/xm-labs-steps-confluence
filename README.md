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
The **Confluence - Post Content** step is now available in your custom steps. So navigate to the appropriate canvas so you can add the step there. If you'd like to experiment with it, the **Post Content** workflow has a canvas that can be triggered via HTTP call. 

### Inputs
| Name  | Required? | Min | Max | Help Text | Default Value | Multiline |
| ----- | ----------| --- | --- | --------- | ------------- | --------- |
| Title | Yes | 0 | 255 | Title of content | | No |
| Type | Yes | 0 | 2000 | The type of the new content. Custom content types defined by apps are also supported. Typical values: page, blogpost, comment, attachment | page | No |
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



## Example
This is an example of the **Confluence - Post Content** step being run after an HTTP trigger is called.

<kbd>
	<img src="/media/ExampleFlow.png">
</kbd>

