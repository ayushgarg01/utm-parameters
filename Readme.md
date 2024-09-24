<h1>How to add UTM Parameters in cf7:</h1>

<strong>Step 1:</strong> Open contact form in which you want to add the utm parameters.

<strong>Step 2:</strong> You have to add the hidden elements with name to the fields.

e.g: [hidden utmSource ""] <br>
[hidden utmMedium ""] <br>
[hidden utmCampaign ""] <br>
[hidden utmId ""] <br>
[hidden utmTerm ""]  <br>
[hidden utmContent ""] <br>

<strong>Step 3:</strong> You have to add the script in header or footer. You can place the code in theme header.php and footer.php or you can install the plugin for this. (WPCode Lite by WPCode)

<script>
document.addEventListener('DOMContentLoaded', function() {
    // Function to get a specific URL parameter
    function getUrlParameter(name) {
        name = name.replace(/[\[]/, '\\[').replace(/[\]]/, '\\]');
        var regex = new RegExp('[\\?&]' + name + '=([^&#]*)');
        var results = regex.exec(location.search);
        return results === null ? '' : decodeURIComponent(results[1].replace(/\+/g, ' '));
    }

    // Mapping of GET parameters to hidden field names
    var paramMapping = {
        'utm_source': 'utmSource',
        'utm_medium': 'utmMedium',
        'utm_campaign': 'utmCampaign',
        'utm_id': 'utmId',
        'utm_term': 'utmTerm',
        'utm_content': 'utmContent'
    };

    // Find all Contact Form 7 forms on the page
    var forms = document.querySelectorAll('.wpcf7-form');

    forms.forEach(function(form) {
        // For each parameter in the mapping
        Object.keys(paramMapping).forEach(function(param) {
            // Get the parameter value from the URL
            var value = getUrlParameter(param);

            // Find the corresponding hidden field in the form using the mapped name
            var field = form.querySelector('input[name="' + paramMapping[param] + '"]');

            // If the field exists and we have a value, set it
            if (field && value) {
                field.value = value;
            }
        });
    });
});
</script>


