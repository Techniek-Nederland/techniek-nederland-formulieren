Get forms for an installation
-------------------------------------

Once you've determined the ETIM Product Class for you installation, you can query the Forms API for relevant forms.

Get a list of relevant forms
++++++++++++++++++++++++++++

.. http:get:: https://api.fgoplus.nl/api/v1/Fgo/Forms/Latest

   Returns a list of forms relevant for you installation

   **Example request**:

   .. sourcecode:: http

      GET /api/v1/Fgo/Forms/All?classCode=EC010232 HTTP/1.1
      Host: api.fgoplus.nl
      Accept: application/json
      Authorization: OAuth token to authenticate


   **Example response (excerpt)**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: text/javascript

      [
        {
            "code": "FGO00002",
            "version": 3,
            "title": "Melding onveilige situatie gas",
            "formCode": "MBO_GAS",
            "publisher": "Techniek Nederland",
            "publisherLink": "https://www.technieknederland.nl"
        }
      ]

   :reqheader Authorization: OAuth token to authenticate
   :query string classCode: The ETIM Class to filter forms for


Get the form itself
++++++++++++++++++++++++++++

.. http:get:: https://api.fgoplus.nl/api/v1/Fgo/Form/[code]/[version]/

   Returns the requested form

   **Example request**:

   .. sourcecode:: http

      GET /api/v1/Fgo/Forms/Form/FGO00002/2/ HTTP/1.1
      Host: api.fgoplus.nl
      Accept: application/json
      Authorization: OAuth token to authenticate


   **Example response (excerpt)**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: text/javascript

        {
            "form": {
                "display": "form",
                "components": [
                    {
                        "input": true,
                        "optionsLabelPosition": "right",
                        "inline": false,
                        "type": "radio",
                        "values": [
                            {
                                "value": "direct",
                                "label": "Direct gevaar"
                            },
                            {
                                "value": "in_time",
                                "label": "Gevaar op termijn"
                            },
                            {
                                "value": "possible",
                                "label": "Mogelijk gevaar"
                            }
                        ],
                        "key": "seriousness",
                        "label": "Wat is de ernst van de situatie?"
                    },
                    {
                        "input": true,
                        "type": "textarea",
                        "key": "situation",
                        "label": "Beschrijf de situatie"
                    },
                    {
                        "label": "Voeg foto's van de situatie toe",
                        "itemLabel": "Foto",
                        "reorder": false,
                        "addAnotherPosition": "bottom",
                        "defaultOpen": false,
                        "layoutFixed": false,
                        "enableRowGroups": false,
                        "initEmpty": false,
                        "defaultValue": [
                            {}
                        ],
                        "key": "photos",
                        "type": "datagrid",
                        "input": true,
                        "components": [
                            {
                                "label": "Foto",
                                "tableView": true,
                                "key": "photoId",
                                "type": "photo",
                                "input": true
                            },
                            {
                                "label": "Toelichting",
                                "tableView": true,
                                "key": "description",
                                "type": "textarea",
                                "input": true
                            }
                        ]
                    },
                    {
                        "input": true,
                        "type": "textarea",
                        "key": "performed_emergency_operation",
                        "label": "Verrichtte noodhandeling"
                    },
                    {
                        "input": true,
                        "type": "textarea",
                        "key": "possible_causer",
                        "label": "Mogelijke veroorzaker"
                    },
                    {
                        "input": true,
                        "optionsLabelPosition": "right",
                        "inline": true,
                        "type": "radio",
                        "values": [
                            {
                                "label": "Ja",
                                "value": "ja"
                            },
                            {
                                "label": "Nee",
                                "value": "nee"
                            }
                        ],
                        "key": "reporter_keep_up_to_date",
                        "label": "Wilt u op de hoogte gehouden worden?"
                    },
                    {
                        "input": true,
                        "optionsLabelPosition": "right",
                        "inline": true,
                        "type": "radio",
                        "values": [
                            {
                                "label": "Ja",
                                "value": "ja"
                            },
                            {
                                "label": "Nee",
                                "value": "nee"
                            }
                        ],
                        "key": "eigenaar-op-de-hoogte-houden",
                        "label": "Eigenaar op de hoogte houden?"
                    }
                ]
            },
            "code": "FGO00002",
            "version": 3,
            "title": "Melding onveilige situatie gas",
            "formCode": "MBO_GAS",
            "publisher": "Techniek Nederland",
            "publisherLink": "https://www.technieknederland.nl"
        }

   :reqheader Authorization: OAuth token to authenticate

