% extends "layout.html" %}
{% block content %}
    <h2>HED services</h2>
    <p>HED tools are available as web services. HED uses JSON format for both
    the request parameters and the response return values. The tools are also available to
    run locally using a deployer Docker module.
    (See the GitHub <a href="https://github.com/hed-standard/hed-python">hed-python</a> repository for code
    and additional information.) Examples of calling the services in MATLAB can be found at:
    <a href="https://github.com/hed-standard/hed-python/blob/master/webtools/examples/matlab">
            https://github.com/hed-standard/hed-python/blob/master/webtools/examples/matlab</a>.
    </p>

    <p>The HED services are currently hosted on
        <a href="https://hedtools.ucsd.edu/hed">https://hedtools.ucsd.edu/hed</a>.</p>

    <h3>To perform a request:</h3>
    <ol>
    <li>Send an initial request to:
        <a href="https://hedtools.ucsd.edu/hed/services">https://hedtools.ucsd.edu/hed/services</a> to get cookie
        information and a csrf token. The
        <a href="https://github.com/hed-standard/hed-python/blob/master/webtools/examples/matlab/getSessionInfo.m">getSessionInfo</a>
        function gives an example of how to perform this initial request in MATLAB.
    </li>
    <li>Use the cookie and csrf token from Step 1 in all subsequent requests for this session. The URL for
    making actual service requests is:
        <a href="https://hedtools.ucsd.edu/hed/services_submit">https://hedtools.ucsd.edu/hed/services_submit</a>.</li>
    <li>
        The form of parameters for the request is a two-entry JSON dictionary with keys <code>"service"</code>
        and <code>"service_parameters"</code>.
        <ul>
            <li> The value associated with <code>"service"</code> is a string giving
                the name of the service.</li>
            <li> The value associated with <code>"service_parameters"</code> is a dictionary of the names of the
                required parameters as keys.</li>
            <li> All parameter values are sent as strings. Files are sent as strings.</li>
            <li> The HED services interface currently only supports tab-separated-value (tsv) files
            and JSON files.</li>
        </ul>
    </li>
    </ol>

    <h3>HED services and their parameters</h3>

        <table>
            <tr><th>Service</th><th>Service parameters</th></tr>
            <tr><td>get_services</td><td></td></tr>
            <tr><td>sidecar_to_long</td><td>json_string<br>
                                               schema_string or schema_url or schema_version</td></tr>
            <tr><td>sidecar_to_short</td><td>json_string<br>
                                               schema_string or schema_url or schema_version</td></tr>
            <tr><td>sidecar_validate</td><td>json_string<br>
                                               schema_string or schema_url or schema_version<br>
                                                check_for_warnings</td></tr>
            <tr><td>events_assemble</td>     <td>events_string<br>
                                               json_string<br>
                                               schema_string or schema_url or schema_version<br>
                                               expand_defs<br>
                                                check_for_warnings</td></tr>
            <tr><td>events_validate</td>     <td>events_string<br>
                                               json_string<br>
                                               schema_string or schema_url or schema_version<br>
                                                check_for_warnings</td></tr>
            <tr><td>spreadsheet_to_long</td><td>spreadsheet_string<br>
                                               schema_string or schema_url or schema_version</td></tr>
            <tr><td>spreadsheet_to_short</td><td>spreadsheet_string<br>
                                               schema_string or schema_url or schema_version</td></tr>
            <tr><td>spreadsheet_validate</td><td>spreadsheet_string<br>
                                               schema_string or schema_url or schema_version<br>
                                                check_for_warnings</td></tr>
            <tr><td>strings_to_long</td><td>string_list<br>
                                               schema_string or schema_url or schema_version</td></tr>
            <tr><td>strings_to_short</td><td>string_list<br>
                                               schema_string or schema_url or schema_version</td></tr>
            <tr><td>strings_validate</td><td>string_list<br>
                                               schema_string or schema_url or schema_version<br>
                                                check_for_warnings</td></tr>
        </table>

**** HED service response format

All HED services requests have the same response format. 
The response consists of a JSON dictionary with four keys (shown in the following table).
If the service successfully executed the error_type and error_msg are empty. 
In case of failure, the error_type and error_msg have an explanation of why the 
service failed --- for example there was a connection timeout.  


`````{list-table} HED web-based schema vocabulary viewers.
:header-rows: 1
:widths: 20 50

* - Response field
  - Meaning
* - service
  - Name of the requested service.
* - results 
  - Dictionary with results of service.
* - error_type
  - Type of error if the service failed.
* - error_msg
  - Explanation of the message if the service failed.  
`````   

**** Format of the `results` dictionary returned in the response

`````{list-table} HED web-based schema vocabulary viewers.
:header-rows: 1
:widths: 20 50
* - Key
  - Meaning
* - command
  - Command that was executed in response to the service request.
* - data
  - Data returned by the service.
* - msg_category
  - Success, warning, or failure depending on the result of service request.
* - msg
  - Explanation of the result of service processing.
````` 

**** HED service request parameters

`````{list-table} HED web-based schema vocabulary viewers.
:header-rows: 1
:widths: 20 50
* - Service parameter
  - Meaning
* - check_for_warnings_validation
  - If true, check for warnings when validating.
* - column_x_check
  - If present with value 'on', column number x has HED tags.
* - column_x_input
  - Prefix appended to column x if x has HED tags.
* - msg
  - Explanation of the result of service processing.
* - defs_expand
  - If true, replace def/XXX with def-expand/XXX.
* - events_string
  - A BIDS events file as a string.
* - has_column_names
  - If true, the first row of file contains column names.
* - hed_columns
  - List of column numbers (starting with 1) of HED string columns.  
    If empty, all columns are used.
* - hed_strings
  - List of HED strings to be processed.
* - json_string
  - A BIDS JSON sidecar as a string.
* - schema_string
  - HED XML schema as a string.
* - schema_url
  - URL from which a HED schema can be downloaded.
* - schema_version
  - Version of HED to used in processing.  
* - spreadsheet_string
  - A spreadsheet tsv file as a string.
````` 
