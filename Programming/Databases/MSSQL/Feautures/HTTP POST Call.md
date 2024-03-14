#mssql #database #http-post 

Use the following SQL script to create a procedure for executing HTTP JSON POST calls to an API endpoint:

``` sql
CREATE PROCEDURE dbo.http_post
    @url NVARCHAR(MAX),
    @bearer_token NVARCHAR(MAX),
    @json_body NVARCHAR(MAX),
    @response NVARCHAR(MAX) OUTPUT
AS
BEGIN
    DECLARE @Object INT;

    -- Initialize the OLE object for making HTTP requests.
    EXEC sp_OACreate 'MSXML2.XMLHTTP', @Object OUT;
    EXEC sp_OAMethod @Object, 'open', NULL, 'post', @url, 'false';
    EXEC sp_OAMethod @Object, 'setRequestHeader', NULL, 'accept', 'application/json';
    EXEC sp_OAMethod @Object, 'setRequestHeader', NULL, 'Content-Type', 'application/json';
    EXEC sp_OAMethod @Object, 'setRequestHeader', NULL, 'Authorization', CONCAT(N'Bearer ', @bearer_token);

    -- Send the HTTP POST request with the JSON body.
    EXEC sp_OAMethod @Object, 'send', NULL, @json_body;

    -- Retrieve the response.
    EXEC sp_OAMethod @Object, 'responseText', @response OUTPUT;

    -- Return the response if needed.

    -- Clean up the OLE object.
    EXEC sp_OADestroy @Object;
END;
```