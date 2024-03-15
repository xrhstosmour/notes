#mssql #database #http-post #ole #http-functionality

### Prerequisites

Before starting, ensure you have configured the below:
1. [[Enable Functionality]]
2. [[Grant OLE Execution Permissions]]
### Create Store Procedure

Use the following SQL script to create a procedure for executing HTTP JSON POST calls to an API endpoint:

``` sql
CREATE PROCEDURE dbo.http_post
    @url NVARCHAR(MAX),
    @bearer_token NVARCHAR(MAX) = NULL, -- Default to NULL if not provided.
    @json_body NVARCHAR(MAX) = NULL, -- Default to NULL if not provided.
    @response VARCHAR(8000) OUTPUT
AS
BEGIN

    -- Declare the OLE object.
    DECLARE @Object INT;

    -- Declare a variable for the full authorization header.
    DECLARE @authorization_header NVARCHAR(MAX);

    -- Initialize the OLE object for making HTTP requests.
    EXEC sp_OACreate 'MSXML2.XMLHTTP', @Object OUT;
    EXEC sp_OAMethod @Object, 'open', NULL, 'post', @url, 'false';
    EXEC sp_OAMethod @Object, 'setRequestHeader', NULL, 'accept', 'application/json';
    EXEC sp_OAMethod @Object, 'setRequestHeader', NULL, 'Content-Type', 'application/json';

    -- Include the Authorization header only if a bearer token is provided.
    IF @bearer_token IS NOT NULL
    BEGIN
        SET @authorization_header = CONCAT(N'Bearer ', @bearer_token);
        EXEC sp_OAMethod @Object, 'setRequestHeader', NULL, 'Authorization', @authorization_header;
    END

    -- Send the HTTP POST request with the JSON body if provided.
    IF @json_body IS NOT NULL
    BEGIN
        EXEC sp_OAMethod @Object, 'send', NULL, @json_body;
    END

    -- Retrieve the response.
    EXEC sp_OAMethod @Object, 'responseText', @response OUTPUT;

    -- Clean up the OLE object.
    EXEC sp_OADestroy @Object;

	-- Return the response.
	SELECT @response
END;
```

### Example Usage

``` sql
-- Declare variables needed for the HTTP POST call.
DECLARE @url NVARCHAR(MAX) = N'<endpoint_url>';
DECLARE @bearer_token NVARCHAR(MAX) = N'<bearer_token>';
DECLARE @json_body NVARCHAR(MAX) = N'<json_body>';
DECLARE @response NVARCHAR(MAX);

-- Make the HTTP POST call.
EXEC dbo.http_post @url, @bearer_token, @json_body, @response OUTPUT;
```
