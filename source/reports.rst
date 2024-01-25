Reports
=======

The Techniek Nederland service facilitates the generation of reports through the provided API. To initiate the report
generation process, use the same authentication token employed for form requests and make a call to the
/api/v1/third-party-reports/generate_report_template/ endpoint. Similar to form requests, specify the `form_code`
to identify the desired report template.

Additionally, utilize the `data` field to supply the necessary information to be entered into the form. If the data
field is omitted, the result will be an empty form, available for completion as a digital PDF. An optional feature is
the `add_defaults_fields`-parameter, which allows users to control the inclusion of default fields such as
'contact person' details and 'installation' information. Toggle this option by setting it to false if you prefer
to exclude these default fields from the generated report.

For a comprehensive understanding of available parameters and endpoint functionalities, refer to the
Swagger documentation. It provides a detailed definition and specification of the API, guiding users through the
process of generating reports seamlessly.

Example call:

.. http:post:: https://formulierenappbeheer.technieknederland.nl/api/v1/third-party-reports/generate_report_template/

    :reqheader Authorization: Access token provided by IDP

    **Example request**

    .. sourcecode:: http

        GET /api/v1/Fgo/Product/Search?SearchString=boiler&Size=10&From=0 HTTP/1.1
        Host: api.fgoplus.nl
        Authorization: Bearer <INSERT ACCESS TOKEN>
        Content-Type: application/json
        Accept: application/pdf; charset=utf-8

        {
            "form_code": "FGO00003",
            "data": {
                "client": {
                    "contact_person": "Pete Peterson"
                },
                "report_info": {
                    "report_visit_date": "2024-01-02"
                }
            },
            "add_default_fields": false
        }



For users with additional permissions, the Techniek Nederland service offers the flexibility to generate custom forms
by providing their own `form_json` through the API. In this scenario, the traditional `form_code` is omitted,
allowing users to define the structure and content of the form according to their specific requirements. This feature
empowers users to create tailored forms that align precisely with their needs. Below is an example illustrating the process:

.. http:post:: https://formulierenappbeheer.technieknederland.nl/api/v1/third-party-reports/generate_report_template/

    :reqheader Authorization: Access token provided by IDP

    **Example request**

    .. sourcecode:: http

        GET /api/v1/Fgo/Product/Search?SearchString=boiler&Size=10&From=0 HTTP/1.1
        Host: api.fgoplus.nl
        Authorization: Bearer <INSERT ACCESS TOKEN>
        Content-Type: application/json
        Accept: application/pdf; charset=utf-8

        {
            "form_json": {
                "form": {
                    "display": "form",
                    "components": [
                        {
                            "key": "A-01",
                            "label": "A-01 Watercircuit",
                            "tooltip": "Controleer de druk in het watercircuit",
                            "type": "radio",
                            "values": [
                                {
                                    "label": "Ja",
                                    "value": "ja"
                                },
                                {
                                    "label": "Nee",
                                    "value": "nee"
                                },
                                {
                                    "label": "Nvt",
                                    "value": "n.v.t."
                                }
                            ]
                        }
                    ]
                }
            },
            "data": {
                "client": {
                    "contact_person": "Pete Peterson"
                },
                "report_info": {
                    "report_visit_date": "2024-01-02"
                },
                "A-01": "ja"
            },
            "add_default_fields": false
        }


In this example, the `form_json` parameter allows users to define custom fields and sections within the form.
The `add_defaults_fields` option remains available for users who wish to include default fields like
contact person details, installation information, etc. Adjust the value to `false` if these defaults should be omitted.

Refer to the Swagger documentation for a comprehensive guide on utilizing this functionality.
