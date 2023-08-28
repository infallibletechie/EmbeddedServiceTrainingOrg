<html>
<style type='text/css'>
	.embeddedServiceHelpButton .helpButton .uiButton {
		background-color: #005290;
		font-family: "Arial", sans-serif;
	}
	.embeddedServiceHelpButton .helpButton .uiButton:focus {
		outline: 1px solid #005290;
	}
</style>

<script type='text/javascript' src='https://service.force.com/embeddedservice/5.0/esw.min.js'></script>
<script type='text/javascript'>
	var initESW = function(gslbBaseURL) {
		embedded_svc.settings.displayHelpButton = true; //Or false
		embedded_svc.settings.language = ''; //For example, enter 'en' or 'en-US'

		embedded_svc.settings.extraPrechatFormDetails = [
      {
          "label":"Text",
          "transcriptFields": [ "Text__c" ]
      },
      {
          "label":"Skill",
          "transcriptFields": [ "Skill__c" ]
      }
    ];

		embedded_svc.settings.enabledFeatures = ['LiveAgent'];
		embedded_svc.settings.entryFeature = 'LiveAgent';

		embedded_svc.init(
			'https://test-ec-dev-ed.develop.my.salesforce.com',
			'https://test-ec-dev-ed.develop.my.site.com/',
			gslbBaseURL,
			'00D3t000005YGES',
			'Embedded_Service_Chat',
			{
				baseLiveAgentContentURL: 'https://c.la1-c1-ia5.salesforceliveagent.com/content',
				deploymentId: '5723t000000DI9k',
				buttonId: '5733t00000096rS',
				baseLiveAgentURL: 'https://d.la1-c1-ia5.salesforceliveagent.com/chat',
				eswLiveAgentDevName: 'EmbeddedServiceLiveAgent_Parent04I3t000000LQzsEAG_186671c09b1',
				isOfflineSupportEnabled: false
			}
		);
	};

	if (!window.embedded_svc) {
		var s = document.createElement('script');
		s.setAttribute('src', 'https://test-ec-dev-ed.develop.my.salesforce.com/embeddedservice/5.0/esw.min.js');
		s.onload = function() {
			initESW(null);
		};
		document.body.appendChild(s);
	} else {
		initESW('https://service.force.com');
	}

  document.addEventListener(
    "setCustomField",
    function( event ) {
        console.log(
                'Inside the Custom Field Listener'
        );
        console.log(
                'Passed Text value is',
                event.detail.text
        );
        console.log(
                'Passed Skill value is',
                event.detail.skill
        );
        embedded_svc.settings.extraPrechatFormDetails[ 0 ].value = event.detail.text;
        embedded_svc.settings.extraPrechatFormDetails[ 1 ].value = event.detail.skill;
        event.detail.callback();
    },
        false
);
</script>
</html>
