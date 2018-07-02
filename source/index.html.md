---
title: Stratfor Threat Lens&trade; - API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - php

toc_footers:
  - <a href='https://lp.stratfor.com/api'>Sign Up for an API Key</a>
  - Copyright &copy;2018 Stratfor Enterprises, LLC.

includes:
  - errors

search: true
---

# Overview

Stratfor provides global awareness and guidance to individuals, governments and businesses around the world. We use a unique, intel-based approach to analyze world affairs.

This API reference provides information on available endpoints and how to interact with it.

## Content Types

[https://www.drupal.org/docs/7/understanding-drupal/content-types](https://www.drupal.org/docs/7/understanding-drupal/content-types)

*A single web site could contain many types of content, such as informational pages, news items, polls, blog posts, real estate listings, etc. In Drupal, each item of content is called a node, and each node belongs to a single content type, which defines various default settings for nodes of that type, such as whether the node is published automatically and whether comments are permitted. (Note that in previous versions of Drupal, content types were known as node types.)*

### Content types for Threat Lens:

Content type name | Machine name | Description
--- | --- | ---
Analysis | lens_analysis | Description here ...
Intelligence Update | lens_incident_report | Description here ...
Forecast | lens_forecast | Description here ...
Report | lens_report | Description here ...
Graphics | lens_graphics | Description here ...

**nid**: Node ID or Content ID

## Taxonomy

Taxonomy vocabulary name | Vocabulary machine name | Taxonomy terms
--- | --- | ---
Countries | countries | **Taxonomy terms:**<br /><ul><li>South Sudan</li><li>Angola</li><li>Benin</li><li>...</li></ul>
Threat Type | threat_type | **Taxonomy terms:**<ul><li>Terrorism and Insurgency</li><li>Criminal Activity</li><li>Business Continuity</li><li>Industrial Espionage</li></ul>
Incident Type | incident_type | **Taxonomy terms:**<ul><li>Adverse Government Actions</li><li>Adverse NGO Activities</li><li>Armed Assault</li><li>Arson</li><li>Assassination/Attempted Assassination</li><li>Attacks against First Responders</li><li>Bombing</li><li>Cargo Threats</li><li>Corruption</li><li>Crimes Targeting Expats/Tourists</li><li>Crimes Targeting Public Figures</li><li>Cyber Crimes</li><li>Cyber Espionage</li><li>Drug Trafficking</li><li>Executive Protection</li><li>Health</li><li>Intellectual Property Theft</li><li>Kidnapping/Hostage Taking</li><li>Labor Actions</li><li>Natural Disaster</li><li>Organized Crime</li><li>Other Criminal Activity</li><li>Political Unrest</li><li>Seizure/Hijacking</li><li>Stalking</li><li>Traditional Espionage</li><li>Vehicular Assault</li><li>Workplace Violence/Insider Threat</li></ul>
Incident Target | incident_target | **Taxonomy terms:**<ul><li>Aviation</li><li>Energy</li><li>Telecommunications</li><li>Business/Corporate</li><li>Diplomatic</li><li>Education</li><li>Government</li><li>Infrastructure</li><li>Law Enforcement</li><li>Maritime</li><li>Media/Journalist/Blogger</li><li>Military</li><li>NGO</li><li>Public Figures/Officials</li><li>Religious Figures/Facilities/Events</li><li>Tourists/Expats</li></ul>
Weapon | weapon | **Taxonomy terms:**<ul><li>CBRN</li><li>Explosives</li><li>Firearms</li><li>Fire/Firebomb</li><li>Knife/Blade/Sharp Object</li></ul>

**vid**: Taxonomy Vocabulary ID

**tid**: Taxonomy Term ID

# Authentication

Stratfor utilizes API keys to allow access to the API.

The API expects for the API key to be included in all API requests to the server in either:

* A header that takes the following format: **`apiKey: YOUR_API_KEY`**
* A query string parameter that takes the following format: **`?apiKey=YOUR_API_KEY`**

<aside class="notice">
You must replace <code>YOUR_API_KEY</code> with your actual API key.
</aside>

# Content API

## List all contents

```shell
curl --request POST \
  --url 'https://api.stratfor.com/api/v3/content/lens' \
  --header 'apiKey: YOUR_API_KEY' \
  --header 'Content-Type: application/json' \
  --data '{
    "lens_type": "Threat",
    "page": 0,
    "limit": 10,
    "type": [
      "lens_analysis",
      "lens_incident_report",
      "lens_forecast",
      "lens_report",
      "lens_graphics"
    ],
    "sort_by": ["created", "DESC"],
    "taxonomy": {
      "countries": {
        "type": "code",
        "data": ["JP", "DE"]
      },
      "threat_type": {
        "type": "name",
        "data": ["Terrorism and Insurgency", "Criminal Activity"]
      },
      "incident_type": {
        "type": "tid",
        "data": [428, 429, 430]
      },
      "weapon": {
        "type": "tid",
        "data": [470]
      }
    }
  }'
```

```php
<?php
$curl = curl_init();

$post_fields = array(
  "lens_type" => "Threat",
  "page" => 0,
  "limit" => 10,
  "type" => array(
    "lens_analysis",
    "lens_incident_report",
    "lens_forecast",
    "lens_report",
    "lens_graphics",
  ),
  "sort_by" => array("created", "DESC"),
  "taxonomy" => array(
    "countries" => array(
      "type" => "code",
      "data" => array("JP", "DE"),
    ),
    "threat_type" => array(
      "type" => "name",
      "data" => array("Terrorism and Insurgency", "Criminal Activity"),
    ),
    "incident_type" => array(
      "type" => "tid",
      "data" => array(428, 429, 430),
    ),
    "weapon" => array(
      "type" => "tid",
      "data" => array(470),
    ),
  ),
);

curl_setopt_array($curl, array(
  CURLOPT_CUSTOMREQUEST => "POST",
  CURLOPT_URL => "https://api.stratfor.com/api/v3/content/lens",
  CURLOPT_HTTPHEADER => array(
    "apiKey: YOUR_API_KEY",
    "Content-Type: application/json"
  ),
  CURLOPT_POSTFIELDS => json_encode($post_fields),
  CURLOPT_RETURNTRANSFER => true,
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
}
else {
  echo $response;
}
```

> Response body:

```json
{
  "total_count": "521",
  "nodes": [
    {
      "nid": "290146",
      "type": "lens_analysis",
      "title": "Understanding Businesses' Duty of Care: The Duty to Foresee",
      "field_teaser_body": "Corporations must continually work to foresee risks to their personnel to avoid legal liability.",
      "source": "",
      "promo_image": {
        "alt": "Understanding Businesses' Duty of Care: The Duty to Foresee",
        "title": "Understanding Businesses' Duty of Care: The Duty to Foresee",
        "caption": "<p>Norwegian Refugee Council employee Steven Dennis (L) on July 2, 2012, at the airport in Nairobi after having been freed the night before. (TONY KARUMBA/AFP/Getty Images)</p>",
        "sizes": {
          "thumbnail_notification": "https://www.stratfor.com/sites/default/files/styles/thumbnail_192x108/public/duty-of-care-pt1-display.png?itok=dOs9v9iO",
          "thumbnail": "https://www.stratfor.com/sites/default/files/styles/9x6_280x187/public/duty-of-care-pt1-display.png?itok=pCpTD5SN",
          "medium": "https://www.stratfor.com/sites/default/files/styles/medium_640x200/public/duty-of-care-pt1-display.png?itok=1zS3CIid",
          "large": "https://www.stratfor.com/sites/default/files/styles/large_1504x470/public/duty-of-care-pt1-display.png?itok=tSIfMkds",
          "16x9": "https://www.stratfor.com/sites/default/files/styles/16x9_640x360/public/duty-of-care-pt1-display.png?itok=jgD4m-GL",
          "9x6": "https://www.stratfor.com/sites/default/files/styles/9x6_720x480/public/duty-of-care-pt1-display.png?itok=26OQ-0LJ",
          "full": "https://www.stratfor.com/sites/default/files/duty-of-care-pt1-display.png"
        }
      },
      "graphics_type": "",
      "graphics_image": "",
      "youtube_video_url": "",
      "taxonomy": [
        {
          "tid": "90",
          "vid": "5",
          "v_name": "countries",
          "name": "Norway",
          "code": "NO",
          "path_alias": "/region/europe/norway"
        },
        {
          "tid": "421",
          "vid": "21",
          "v_name": "threat_type",
          "name": "Terrorism and Insurgency",
          "path_alias": "/taxonomy/term/421"
        },
        {
          "tid": "430",
          "vid": "22",
          "v_name": "incident_type",
          "name": "Armed Assault",
          "path_alias": "/taxonomy/term/430"
        },
        {
          "tid": "434",
          "vid": "22",
          "v_name": "incident_type",
          "name": "Bombing",
          "path_alias": "/taxonomy/term/434"
        },
        {
          "tid": "453",
          "vid": "23",
          "v_name": "incident_target",
          "name": "Business/Corporate",
          "path_alias": "/taxonomy/term/453"
        },
        {
          "tid": "755",
          "vid": "26",
          "v_name": "series",
          "name": "Understanding Businesses' Duty of Care",
          "path_alias": "/taxonomy/term/755"
        },
        {
          "tid": "470",
          "vid": "24",
          "v_name": "weapon",
          "name": "Firearms",
          "path_alias": "/taxonomy/term/470"
        }
      ],
      "created": "1530210979",
      "created_formatted": "June 28, 2018 | 18:36 GMT",
      "changed": "1530217550",
      "changed_formatted": "June 28, 2018 | 20:25 GMT",
      "path_alias": "content/understanding-businesses-duty-care-duty-foresee",
      "label": "Analysis"
    },
    ... another node object ...
  ]
}
```

This endpoint lists all Threat Lens contents.

### HTTP Request

<a href="#list-all-contents" class="method post">POST</a> `/api/v3/content/lens`

### Request body parameters

Parameter | Default | Description
--- | --- | ---
lens_type<br />*`string, required`* | | Type of Stratfor Lens product.<br />**Available options:**<br />Threat<br />...
page<br />*`integer, optional`* | 0 |The page number to start with.<br />0 = First page<br />1 = Second page<Br />and, so on.
limit<br />*`integer, optional`* | 10 | The number of items to return in the response.
type<br />*`array, optional`* | | Lens content types.<br />**Available Threat Lens content types:**<ul><li>lens_analysis</li><li>lens_incident_report</li><li>lens_forecast</li><li>lens_report</li><li>lens_graphics</li></ul>**Note:** If not specified, it returns contents from all available content types.<br />[Click here](#content-types) to get more details about content types.
sort_by<br />*`array, optional`* | ["created", "DESC"] | Sort the list of contents.<br />**Available options:**<br />["created", "DESC"]<br />["created", "ASC"]<br />["changed", "DESC"]<br />["changed", "ASC"]<br />["nid", "DESC"]<br />["nid", "ASC"]
taxonomy<br />*`object, optional`* | | Filter by taxonomy terms.<br />[Click here](#taxonomy) to get more details about taxonomy vocabulary and terms.

### Format of "taxonomy" filter:

<img src="images/threatlens-taxonomy-filter-diagram.png" />

If **type**=**tid**, we have to pass an array of *Taxonomy Term ID* in **data** field.

If **type**=**name**, we have to pass an array of *Taxonomy Term Name* in **data** field.

If **type**=**code**, we have to pass an array of *Country Code* in **data** field. This is valid for "**countries**" vocabulary only.

## Retrieve full content

```shell
curl --request GET \
  --url 'https://api.stratfor.com/api/v3/content/290146?site=threatlens' \
  --header 'apiKey: YOUR_API_KEY' \
  --header 'Content-Type: application/json'
```

```php
<?php
$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_CUSTOMREQUEST => "GET",
  CURLOPT_URL => "https://api.stratfor.com/api/v3/content/290146?site=threatlens",
  CURLOPT_HTTPHEADER => array(
    "apiKey: YOUR_API_KEY",
    "Content-Type: application/json"
  ),
  CURLOPT_RETURNTRANSFER => true,
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
}
else {
  echo $response;
}
```

> Response body:

```json
{
  "nid": "290146",
  "type": "lens_analysis",
  "title": "Understanding Businesses' Duty of Care: The Duty to Foresee",
  "field_teaser_body": "Corporations must continually work to foresee risks to their personnel to avoid legal liability.",
  "summary": "<ul><li>The risk of lawsuits means companies must understand the duty of care &mdash; or the reasonable actions a person or entity must take to protect those under their care from injury or death &mdash; they owe their employees.</li><li>One of the three elements of the duty of care is the duty to foresee, or the expectation that companies remain aware of the reasonably foreseeable threats, both common and uncommon, to their personnel.</li><li>This can be tricky for multinational organizations where risk can vary drastically from country to country and may not always be fully understood &mdash; especially if the company lacks a global security department to monitor and evaluate threats.</li><li>We believe it is possible to identify trends and incidents to foresee many issues and problems before they crop up using protective intelligence.</li></ul>",
  "pov": "",
  "body": "<p><strong>Editor&#39;s Note:</strong> <em>This is the first in a three-part series on the three components of the duty of care.</em></p><p>In 2012, Steve Dennis was kidnapped while working for the Norwegian Refugee Council in a Kenyan refugee camp. After his release, he successfully sued his employer in Norwegian court for gross negligence and failing to properly exercise its duty of care to him in a case known as Steven Patrick Dennis v. Norwegian Refugee Council. Not only does Dennis seem to have been deployed without proper training, post-incident care apparently was also lacking. Dennis recovered over $500,000 in damages from the council due to its poor field security decisions and for ignoring its own duty of care regarding the protection of its personnel.</p><p>In today&#39;s global and virtually connected marketplace, employers like the Norwegian Refugee Council will continue to face increased scrutiny when their workers are injured or killed during the course of their company duties. An understanding of the need to meet one&#39;s duty of care is gaining traction among security personnel, particularly in the United States. Costly and embarrassing media reports and court cases involving employers&#39; failures to protect their workforce have brought many companies into line. In some countries, including the United Kingdom, duty of care laws mandate certain procedures when personnel are sent outside of their home country. As a result, companies are wisely choosing to adopt certain standards to help protect their personnel and limit their liability to lawsuits that can arise from sending employees into dangerous situations.</p><p>Employers are generally expected to meet industry standards regarding the duty of care. Companies that lack basic duty of care mechanisms are accordingly at greater risk of legal liability. The Norwegian court in the Dennis case described the issues as follows: &quot;The central issue pursuant to the fault-based liability standard is whether the NRC&#39;s employees should have acted differently to avert the risk of kidnapping. Central elements of this assessment include the degree of the risk, the nature of the risk, and whether the risk of injury was visible or foreseeable, and whether effective and practicable alternative courses of action existed. In addition, it may be of relevance whether or not industry standards were violated. On the basis of the said elements, the Court is to perform a concrete overall assessment of whether the NRC&#39;s course of action was negligent.&quot;</p><p>Duty of care can mean various things depending on context and the profession in question. In general, and for the purposes of this analysis, we see duty of care as the reasonable actions that a person or entity should take in order to protect others under their care from injury or death. We will examine the duty of care in relation to international personnel security and explore how protective intelligence aids security practitioners in meeting duty of care standards. This article is written from the perspective of protective intelligence and security practitioners, and is not intended as legal advice. You should consult with your legal counsel regarding the issues related to your specific situation.</p><p>The duty of care concept generally incorporates three duties: the duty to foresee, the duty to warn and the duty to protect.</p><h3>The Duty to Foresee</h3><p>The duty to foresee includes the expectation for companies to remain aware of the reasonably foreseeable threats, both common and uncommon, to their personnel. In many roles, these risks are easier to foresee than others. For example, a skydiving company can be expected to understand that the greatest risk to its clients exists after its aircraft leave the ground. Chief among these risks, of course, is an accident or injury resulting from the jump, whether caused by user error or parachute malfunction. These risks are fairly easy to foresee based on the limited scope of what a skydiving company actually does.</p><p>Things get trickier, however, for multinational organizations with international operations. Risk can vary drastically from country to country and may not always be fully understood &mdash; especially if the company lacks a global security department to monitor and evaluate threats. As the exposure threshold dramatically increases when the company is deploying personnel to these locales, hiring locals, building infrastructure (factories, warehouses, offices), and storing or transmitting proprietary data through these facilities, so does the difficulty in forecasting risks.</p><p>The question of foreseeability was debated after the 2007 Virginia Tech massacre. Relatives of the victims sued, arguing that university personnel should have recognized the risk of a mass shooting as soon as police officers became aware that two people had been shot in what turned out to have been a prelude to the main massacre. The plaintiffs argued that had law enforcement immediately placed the campus on lockdown, lives could have been saved.</p><p>Many companies use free and paid services to assist them with foreseeing such threats. Programs like the Overseas Security Advisory Council (better known as OSAC) and other open-source monitoring platforms can help. Many corporations, however, pay for services that offer enhanced capabilities, increasing their ability to collect and analyze trends and breaking events. A key consideration should be the size and experience level of your security team in relation to the footprint of your company&#39;s operations and personnel deployed around the world. Too many large companies that have operations in a multitude of countries have far too few security professionals &mdash; in extreme cases, one person may be tasked with covering the entire world.</p><p>Convincing a court that a company with just one security specialist in charge of monitoring the globe&nbsp;was adequately staffed to foresee threats&nbsp;would likely prove challenging. Offsetting the costs of these efforts by hiring only junior-level employees would also be unlikely to impress a court: Competency and training often play central roles in lawsuits. For this reason, security teams must have a diverse blend of seasoned professionals who understand the dynamics of threat recognition.</p><p>Protective intelligence can play a tremendously helpful role in this leg of the duty-of-care triad. A vast amount of security services are in the business of alerting. Once the package explodes, the gunman shoots, the crowd protests or the waves come ashore, those services send a message advising that the incident occurred in what is essentially an expensive wire service.</p><p>While such services can play an important role in advising personnel about risk, thus helping satisfy the duty to warn, they typically lack the analytical and predictive component that helps one foresee dangers. We believe it is possible to identify trends and incidents to foresee issues and problems before they crop up. Services like Threat Lens not only alert users to incidents, they help them spot trends, allowing security managers to foresee risk and take actions to protect their personnel, assets and intellectual property &mdash; and also to reduce their legal liability.</p><p><em>Next: The Duty to Warn</em></p>",
  "lens_type": [
    {
      "tid": "473",
      "vid": "27",
      "name": "Threat"
    }
  ],
  "source": "",
  "taxonomy": [
    {
      "tid": "90",
      "vid": "5",
      "v_name": "countries",
      "name": "Norway",
      "code": "NO",
      "path_alias": "/region/europe/norway"
    },
    {
      "tid": "421",
      "vid": "21",
      "v_name": "threat_type",
      "name": "Terrorism and Insurgency",
      "path_alias": "/taxonomy/term/421"
    },
    {
      "tid": "430",
      "vid": "22",
      "v_name": "incident_type",
      "name": "Armed Assault",
      "path_alias": "/taxonomy/term/430"
    },
    {
      "tid": "434",
      "vid": "22",
      "v_name": "incident_type",
      "name": "Bombing",
      "path_alias": "/taxonomy/term/434"
    },
    {
      "tid": "453",
      "vid": "23",
      "v_name": "incident_target",
      "name": "Business/Corporate",
      "path_alias": "/taxonomy/term/453"
    },
    {
      "tid": "755",
      "vid": "26",
      "v_name": "series",
      "name": "Understanding Businesses' Duty of Care",
      "path_alias": "/taxonomy/term/755"
    },
    {
      "tid": "470",
      "vid": "24",
      "v_name": "weapon",
      "name": "Firearms",
      "path_alias": "/taxonomy/term/470"
    }
  ],
  "location": "",
  "promo_image": {
    "alt": "Understanding Businesses' Duty of Care: The Duty to Foresee",
    "title": "Understanding Businesses' Duty of Care: The Duty to Foresee",
    "caption": "<p>Norwegian Refugee Council employee Steven Dennis (L) on July 2, 2012, at the airport in Nairobi after having been freed the night before. (TONY KARUMBA/AFP/Getty Images)</p>",
    "sizes": {
      "thumbnail_notification": "https://www.stratfor.com/sites/default/files/styles/thumbnail_192x108/public/duty-of-care-pt1-display.png?itok=dOs9v9iO",
      "thumbnail": "https://www.stratfor.com/sites/default/files/styles/9x6_280x187/public/duty-of-care-pt1-display.png?itok=pCpTD5SN",
      "medium": "https://www.stratfor.com/sites/default/files/styles/medium_640x200/public/duty-of-care-pt1-display.png?itok=1zS3CIid",
      "large": "https://www.stratfor.com/sites/default/files/styles/large_1504x470/public/duty-of-care-pt1-display.png?itok=tSIfMkds",
      "16x9": "https://www.stratfor.com/sites/default/files/styles/16x9_640x360/public/duty-of-care-pt1-display.png?itok=jgD4m-GL",
      "9x6": "https://www.stratfor.com/sites/default/files/styles/9x6_720x480/public/duty-of-care-pt1-display.png?itok=26OQ-0LJ",
      "full": "https://www.stratfor.com/sites/default/files/duty-of-care-pt1-display.png"
    }
  },
  "graphics_type": "",
  "graphics_image": "",
  "youtube_video_url": "",
  "pdf_file": "",
  "created": "1530210979",
  "created_formatted": "June 28, 2018 | 18:36 GMT",
  "changed": "1530217550",
  "path_alias": "content/understanding-businesses-duty-care-duty-foresee",
  "status": "1",
  "forecast_type": "",
  "lens_sections": [],
  "forecast": "",
  "thumbnail_url": "",
  "thumbnail_caption": "",
  "thumbnail_credit": "",
  "organizations": [],
  "forecast_child_nodes": [],
  "content_reference": [],
  "label": "Analysis"
}
```

This endpoint retrieves a full content details.

### HTTP Request

<a href="#retrieve-full-content" class="method get">GET</a> `/api/v3/content/{nid}?site=threatlens`

### Path parameters

Parameter | Type | Default | Required | Description
--- | --- | --- | --- | ---
nid | integer | | Yes | Node ID. Also called as "Content ID".

### Query parameters

Parameter | Type | Default | Required | Description
--- | --- | --- | --- | ---
site | string | threatlens | Yes | "**site**" parameter must be set to "**threatlens**" for Threat Lens site.

## Get maps content

```shell
curl --request POST \
  --url 'https://api.stratfor.com/api/v3/content/maps_content' \
  --header 'apiKey: YOUR_API_KEY' \
  --header 'Content-Type: application/json' \
  --data '{
    "lens_type":"Threat",
    "location":{
      "left": -98.4375,
      "top": 43.548548110912854,
      "right": 127.96875,
      "bottom": -25.20494115356912
    },
    "type": [
      "lens_analysis",
      "lens_incident_report",
      "lens_forecast",
      "lens_report",
      "lens_graphics"
    ],
    "date_range":{
      "start":1526500260,
      "end": 1526600260
    },
    "taxonomy": {
      "countries": {
        "type": "code",
        "data": ["JP", "DE"]
      }
    }
  }'
```

```php
<?php
$curl = curl_init();

$post_fields = array(
  "lens_type" => "Threat",
  "location" => array(
    "left" => -98.4375,
    "top" => 43.548548110912854,
    "right" => 127.96875,
    "bottom" => -25.20494115356912
  ),
  "type" => array(
    "lens_analysis",
    "lens_incident_report",
    "lens_forecast",
    "lens_report",
    "lens_graphics"
  ),
  "date_range" => array(
    "start" => 1526500260,
    "end" => 1526600260
  ),
  "taxonomy" => array(
    "countries" => array(
      "type" => "code",
      "data" => array("JP", "DE")
    )
  )
);

curl_setopt_array($curl, array(
  CURLOPT_CUSTOMREQUEST => "POST",
  CURLOPT_URL => "https://api.stratfor.com/api/v3/content/maps_content",
  CURLOPT_HTTPHEADER => array(
    "apiKey: YOUR_API_KEY",
    "Content-Type: application/json"
  ),
  CURLOPT_POSTFIELDS => json_encode($post_fields),
  CURLOPT_RETURNTRANSFER => true,
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
}
else {
  echo $response;
}
```

> Response body:

```json
{
  "total_count": 3,
  "nodes": [
    {
      "nid": "289934",
      "type": "lens_incident_report",
      "title": "China: Foreign Airline Resistance to Taiwan Designation Risks Retaliation From Beijing",
      "countries": [
        {
          "tid": "59",
          "vid": "5",
          "name": "United States",
          "code": "US"
        },
        {
          "tid": "195",
          "vid": "5",
          "name": "China",
          "code": "CN"
        },
        {
          "tid": "200",
          "vid": "5",
          "name": "Japan",
          "code": "JP"
        },
        {
          "tid": "215",
          "vid": "5",
          "name": "South Korea",
          "code": "KR"
        },
        {
          "tid": "221",
          "vid": "5",
          "name": "Vietnam",
          "code": "VN"
        },
        {
          "tid": "118",
          "vid": "5",
          "name": "India",
          "code": "IN"
        }
      ],
      "location": {
        "geom": "POINT (104.195397 35.86166)",
        "geo_type": "point",
        "lat": "35.861660000000",
        "lon": "104.195397000000",
        "left": "104.195397000000",
        "top": "35.861660000000",
        "right": "104.195397000000",
        "bottom": "35.861660000000",
        "geohash": "wq6h502v29zn"
      },
      "created": "1529002292",
      "label": "Intelligence Update"
    },
    {
      "nid": "289819",
      "type": "lens_incident_report",
      "title": "Singapore: Suspicious Activity Highlights Espionage Threat Ahead of Korea Summit",
      "countries": [
        {
          "tid": "59",
          "vid": "5",
          "name": "United States",
          "code": "US"
        },
        {
          "tid": "195",
          "vid": "5",
          "name": "China",
          "code": "CN"
        },
        {
          "tid": "200",
          "vid": "5",
          "name": "Japan",
          "code": "JP"
        },
        {
          "tid": "209",
          "vid": "5",
          "name": "North Korea",
          "code": "KP"
        },
        {
          "tid": "213",
          "vid": "5",
          "name": "Singapore",
          "code": "SG"
        },
        {
          "tid": "215",
          "vid": "5",
          "name": "South Korea",
          "code": "KR"
        },
        {
          "tid": "110",
          "vid": "5",
          "name": "Russia",
          "code": "RU"
        }
      ],
      "location": {
        "geom": "POINT (103.819836 1.352083)",
        "geo_type": "point",
        "lat": "1.352083000000",
        "lon": "103.819836000000",
        "left": "103.819836000000",
        "top": "1.352083000000",
        "right": "103.819836000000",
        "bottom": "1.352083000000",
        "geohash": "w21zdqpk3w89"
      },
      "created": "1528475707",
      "label": "Intelligence Update"
    },
    {
      "nid": "289573",
      "type": "lens_analysis",
      "title": "What Businesses Need to Know About Trump's North Korean Summit Cancellation",
      "countries": [
        {
          "tid": "59",
          "vid": "5",
          "name": "United States",
          "code": "US"
        },
        {
          "tid": "195",
          "vid": "5",
          "name": "China",
          "code": "CN"
        },
        {
          "tid": "200",
          "vid": "5",
          "name": "Japan",
          "code": "JP"
        },
        {
          "tid": "209",
          "vid": "5",
          "name": "North Korea",
          "code": "KP"
        },
        {
          "tid": "215",
          "vid": "5",
          "name": "South Korea",
          "code": "KR"
        }
      ],
      "location": {
        "geom": "POINT (127.510093 40.339852)",
        "geo_type": "point",
        "lat": "40.339852000000",
        "lon": "127.510093000000",
        "left": "127.510093000000",
        "top": "40.339852000000",
        "right": "127.510093000000",
        "bottom": "40.339852000000",
        "geohash": "wz4tmxdh8t2w"
      },
      "created": "1527180332",
      "label": "Analysis"
    }
  ]
}
```

Get list of contents with in the map boundary.

### HTTP Request

<a href="#get-maps-content" class="method post">POST</a> `/api/v3/content/maps_content`

### Request body parameters

Parameter | Default | Description
--- | --- | ---
lens_type<br />*`string, required`* | | Type of Stratfor Lens product.<br />**Available options:**<br />Threat<br />...
location<br />*`object, required`* | | Filter contents by left, top, right, bottom coordinates of a map.<br />**Format:**<br />`{"left": ..., "top": ..., "right": ..., "bottom": ...}`
type<br />*`array, optional`* | | Lens content types.<br />**Available Threat Lens content types:**<ul><li>lens_analysis</li><li>lens_incident_report</li><li>lens_forecast</li><li>lens_report</li><li>lens_graphics</li></ul>**Note:** If not specified, it returns contents from all available content types.<br />[Click here](#content-types) to get more details about content types.
date_range<br />*`object, optional`* | | Filter content by content published date.<br />`{"start": X}` <= Load all contents whose published date is greater than **X** timestamp.<br />`{"start": X, "end": Y}` <= Load all contents whose published date is between **X and Y** timestamp.<br />If not specified, it loads all published contents.
taxonomy<br />*`object, optional`* | | Filter by taxonomy terms.<br />[Click here](#taxonomy) to get more details about taxonomy vocabulary and terms.<br />Check [List all contents API](#list-all-contents) to get more details about taxonomy filter.

## Get country stats

```shell
curl --request POST \
  --url 'https://api.stratfor.com/api/v3/content/maps_content' \
  --header 'apiKey: YOUR_API_KEY' \
  --header 'Content-Type: application/json' \
  --data '{
    "lens_type": "Threat",
    "country": {
      "code": "MA"
    },
    "timestamp": 1483392086
  }'
```

```php
<?php
$curl = curl_init();

$post_fields = array(
  "lens_type" => "Threat",
  "country" => array(
    "code" => "MA"
  ),
  "timestamp" => 1483392086
);

curl_setopt_array($curl, array(
  CURLOPT_CUSTOMREQUEST => "POST",
  CURLOPT_URL => "https://api.stratfor.com/api/v3/content/maps_content",
  CURLOPT_HTTPHEADER => array(
    "apiKey: YOUR_API_KEY",
    "Content-Type: application/json"
  ),
  CURLOPT_POSTFIELDS => json_encode($post_fields),
  CURLOPT_RETURNTRANSFER => true,
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
}
else {
  echo $response;
}
```

> Response body:

```json
{
  "lens_type": "Threat",
  "country": {
    "name": "Morocco",
    "tid": "170"
  },
  "stats": {
    "lens_analysis": 1,
    "lens_forecast": 0,
    "lens_incident_report": 1,
    "lens_item_of_interest": 22,
    "lens_report": 1
  }
}
```

Get total number of contents published for particular country.

### HTTP Request

<a href="#get-country-stats" class="method post">POST</a> `/api/v3/content/country_stats`

### Request body parameters

Parameter | Default | Description
--- | --- | ---
lens_type<br />*`string, required`* | | Type of Stratfor Lens product.<br />**Available options:**<br />Threat<br />...
country<br />*`object, required`* | | **Format:**<br />`{"code": "MA"}` or,<br />`{"tid": 170}` or,<br />`{"name": "Morocco"}`
timestamp<br />*`integer, optional`* | | If timestamp is specified, it returns country stats for contents whose published date is greater than specified timestamp.

# Taxonomy API

## List taxonomy

> Example 1: List all "Threat Type" taxonomies.

```shell
curl --request GET \
  --url 'https://api.stratfor.com/api/v3/taxonomy?vocabulary[type]=machine_name&vocabulary[data][0]=threat_type' \
  --header 'apiKey: YOUR_API_KEY' \
  --header 'Content-Type: application/json' \
  --globoff
```

```php
<?php
$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_CUSTOMREQUEST => "GET",
  CURLOPT_URL => "https://api.stratfor.com/api/v3/taxonomy?vocabulary[type]=machine_name&vocabulary[data][0]=threat_type",
  CURLOPT_HTTPHEADER => array(
    "apiKey: YOUR_API_KEY",
    "Content-Type: application/json"
  ),
  CURLOPT_RETURNTRANSFER => true,
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
}
else {
  echo $response;
}
```

> Example 2: List all "Threat Type" taxonomies ordered by weight in descending order.

```shell
curl --request GET \
  --url 'https://api.stratfor.com/api/v3/taxonomy?vocabulary[type]=machine_name&vocabulary[data][0]=threat_type&sort_by[0]=weight&sort_by[1]=DESC' \
  --header 'apiKey: YOUR_API_KEY' \
  --header 'Content-Type: application/json' \
  --globoff
```

```php
<?php
$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_CUSTOMREQUEST => "GET",
  CURLOPT_URL => "https://api.stratfor.com/api/v3/taxonomy?vocabulary[type]=machine_name&vocabulary[data][0]=threat_type&sort_by[0]=weight&sort_by[1]=DESC",
  CURLOPT_HTTPHEADER => array(
    "apiKey: YOUR_API_KEY",
    "Content-Type: application/json"
  ),
  CURLOPT_RETURNTRANSFER => true,
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
}
else {
  echo $response;
}
```

> Example 3: List all "Threat Type" and "Incident Type" taxonomies.

```shell
curl --request GET \
  --url 'https://api.stratfor.com/api/v3/taxonomy?vocabulary[type]=machine_name&vocabulary[data][0]=threat_type&vocabulary[data][1]=incident_type' \
  --header 'apiKey: YOUR_API_KEY' \
  --header 'Content-Type: application/json' \
  --globoff
```

```php
<?php
$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_CUSTOMREQUEST => "GET",
  CURLOPT_URL => "https://api.stratfor.com/api/v3/taxonomy?vocabulary[type]=machine_name&vocabulary[data][0]=threat_type&vocabulary[data][1]=incident_type",
  CURLOPT_HTTPHEADER => array(
    "apiKey: YOUR_API_KEY",
    "Content-Type: application/json"
  ),
  CURLOPT_RETURNTRANSFER => true,
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
}
else {
  echo $response;
}
```

> Example 4: List all "Threat Type" and "Weapon" taxonomies grouped by vocabulary.

```shell
curl --request GET \
  --url 'https://api.stratfor.com/api/v3/taxonomy?vocabulary[type]=machine_name&vocabulary[data][0]=threat_type&vocabulary[data][1]=weapon&options[group_by_vocabulary]=1' \
  --header 'apiKey: YOUR_API_KEY' \
  --header 'Content-Type: application/json' \
  --globoff
```

```php
<?php
$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_CUSTOMREQUEST => "GET",
  CURLOPT_URL => "https://api.stratfor.com/api/v3/taxonomy?vocabulary[type]=machine_name&vocabulary[data][0]=threat_type&vocabulary[data][1]=weapon&options[group_by_vocabulary]=1",
  CURLOPT_HTTPHEADER => array(
    "apiKey: YOUR_API_KEY",
    "Content-Type: application/json"
  ),
  CURLOPT_RETURNTRANSFER => true,
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
}
else {
  echo $response;
}
```

> Example 5: List all "Threat Type" and "Weapon" taxonomies by Vocabulary ID.

```shell
curl --request GET \
  --url 'https://api.stratfor.com/api/v3/taxonomy?vocabulary[type]=vid&vocabulary[data][0]=21&vocabulary[data][1]=24' \
  --header 'apiKey: YOUR_API_KEY' \
  --header 'Content-Type: application/json' \
  --globoff
```

```php
<?php
$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_CUSTOMREQUEST => "GET",
  CURLOPT_URL => "https://api.stratfor.com/api/v3/taxonomy?vocabulary[type]=vid&vocabulary[data][0]=21&vocabulary[data][1]=24",
  CURLOPT_HTTPHEADER => array(
    "apiKey: YOUR_API_KEY",
    "Content-Type: application/json"
  ),
  CURLOPT_RETURNTRANSFER => true,
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
}
else {
  echo $response;
}
```

> Response body (not grouped by vocabulary):

```json
[
  {
    "tid": "421",
    "vid": "21",
    "vocabulary_machine_name": "threat_type",
    "term_name": "Terrorism and Insurgency",
    "path_alias": "/taxonomy/term/421",
    "description": "",
    "synopsis": "",
    "image": []
  },
  {
    "tid": "422",
    "vid": "21",
    "vocabulary_machine_name": "threat_type",
    "term_name": "Criminal Activity",
    "path_alias": "/taxonomy/term/422",
    "description": "",
    "synopsis": "",
    "image": []
  },
  {
    "tid": "423",
    "vid": "21",
    "vocabulary_machine_name": "threat_type",
    "term_name": "Business Continuity",
    "path_alias": "/taxonomy/term/423",
    "description": "",
    "synopsis": "",
    "image": []
  },
  {
    "tid": "424",
    "vid": "21",
    "vocabulary_machine_name": "threat_type",
    "term_name": "Industrial Espionage",
    "path_alias": "/taxonomy/term/424",
    "description": "",
    "synopsis": "",
    "image": []
  }
]
```

> Response body (grouped by vocabulary):

```json
[
  {
    "vid": "21",
    "vocabulary_name": "Threat Type",
    "vocabulary_machine_name": "threat_type",
    "terms": [
      {
        "tid": "421",
        "term_name": "Terrorism and Insurgency",
        "path_alias": "/taxonomy/term/421",
        "description": "",
        "synopsis": "",
        "image": []
      },
      {
        "tid": "422",
        "term_name": "Criminal Activity",
        "path_alias": "/taxonomy/term/422",
        "description": "",
        "synopsis": "",
        "image": []
      },
      {
        "tid": "423",
        "term_name": "Business Continuity",
        "path_alias": "/taxonomy/term/423",
        "description": "",
        "synopsis": "",
        "image": []
      },
      {
        "tid": "424",
        "term_name": "Industrial Espionage",
        "path_alias": "/taxonomy/term/424",
        "description": "",
        "synopsis": "",
        "image": []
      }
    ]
  },
  {
    "vid": "24",
    "vocabulary_name": "Weapon",
    "vocabulary_machine_name": "weapon",
    "terms": [
      {
        "tid": "468",
        "term_name": "CBRN",
        "path_alias": "/taxonomy/term/468",
        "description": "",
        "synopsis": "",
        "image": []
      },
      {
        "tid": "738",
        "term_name": "Vehicle",
        "path_alias": "/taxonomy/term/738",
        "description": "",
        "synopsis": "",
        "image": []
      },
      {
        "tid": "469",
        "term_name": "Explosives",
        "path_alias": "/taxonomy/term/469",
        "description": "",
        "synopsis": "",
        "image": []
      },
      {
        "tid": "470",
        "term_name": "Firearms",
        "path_alias": "/taxonomy/term/470",
        "description": "",
        "synopsis": "",
        "image": []
      },
      {
        "tid": "471",
        "term_name": "Fire/Firebomb",
        "path_alias": "/taxonomy/term/471",
        "description": "",
        "synopsis": "",
        "image": []
      },
      {
        "tid": "472",
        "term_name": "Knife/Blade/Sharp Object",
        "path_alias": "/taxonomy/term/472",
        "description": "",
        "synopsis": "",
        "image": []
      }
    ]
  }
]
```

This endpoint returns a list of taxonomy terms in a vocabulary.

### HTTP Request

<a href="#list-taxonomy" class="method get">GET</a> `/api/v3/taxonomy`

### Query parameters

Parameter | Default | Description
--- | --- | --- | --- | ---
vocabulary<br />`array, required` | | Load taxonomy terms of a vocabulary<br /><br />**Format:**<br />vocabulary[type]=`vid` or `machine_name`<br />vocabulary[data][0]=threat_type<br />vocabulary[data][1]=countries<br />...<br /><br />If vocabulary[type] = machine_name, add an array of vocabulary machine names in vocabulary[data].<br /><br />If vocabulary[type] = vid, add an array of vocabulary IDs in vocabulary[data].
sort_by<br />`array, optional` | sort_by[0]=weight<br />sort_by[1]=ASC | Sort the taxonomy list. <br />Available options for sort_by[0]:<br /><ul><li>created</li><li>changed</li><li>weight</li></ul>Available options for sort_by[1]:<br /><ul><li>ASC</li><li>DESC</li></ul>
options<br />`array, optional` | | Additional options

### Additional options

options[group_by_vocabulary]=1 <= Group taxonomy terms by vocabulary.

## Get country synopsis

```shell
curl --request POST \
  --url 'https://api.stratfor.com/api/v3/content/country_synopsis' \
  --header 'apiKey: YOUR_API_KEY' \
  --header 'Content-Type: application/json' \
  --data '{
    "country_code": "MA"
  }'
```

```php
<?php
$curl = curl_init();

$post_fields = array(
  "country_code" => "MA"
);

curl_setopt_array($curl, array(
  CURLOPT_CUSTOMREQUEST => "POST",
  CURLOPT_URL => "https://api.stratfor.com/api/v3/content/country_synopsis",
  CURLOPT_HTTPHEADER => array(
    "apiKey: YOUR_API_KEY",
    "Content-Type: application/json"
  ),
  CURLOPT_POSTFIELDS => json_encode($post_fields),
  CURLOPT_RETURNTRANSFER => true,
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
}
else {
  echo $response;
}
```

> Response body:

```json
{
  "name": "Morocco",
  "tid": "170",
  "vid": "5",
  "synopsis": "Criminal Activity - Medium\r\nThere is a moderate amount of nonviolent crime in urban areas of Morocco, and violent crime is rare. The most serious crime foreigners face is theft at knifepoint, which typically occurs in the country’s main tourist areas. Crime victimizing foreigners is more common in Marrakech and Casablanca than in the capital, Rabat. Petty theft, including pickpocketing and bag snatching, is also relatively common in major urban areas, though such crimes rarely turn violent.\r\n \r\nTerrorism - Medium\r\nMorocco has recently been home to a number of militant arrests and uncovered plots. The country has a demonstrable history of attacks, however, and both the Islamic State and al Qaeda in the Islamic Maghreb have called for more. Militant groups want to target foreigners in major population areas, including the U.N. mission and popular tourist destinations. Moroccan security forces are highly competent, and few plots have been successful, but in 2011 bombings in Marrakech killed 17 people, mostly foreigners. Many of the recent attacks in Europe have had connections to Morocco, indicating there may be increased radicalization in the country. Morocco also faces elevated risk from the high number of nationals who have traveled to fight with the Islamic State in Iraq and Syria and who may try to return home. Security issues in Tunisia and Libya have necessitated more cooperation with Algeria at the border.\r\n \r\nIndustrial Espionage - Low\r\nThere is little evidence that Moroccan or other national intelligence services have the capability or interest to engage in industrial espionage in the country.\r\n \r\nBusiness Continuity - Low\r\nCorruption and a heavily bureaucratic system are the biggest challenges foreign businesses are likely to face. The government has sought to decrease the complexity of the country’s regulatory environment, with varying success. Protest activity is not a substantial problem in most of Morocco, though the risk varies from sector to sector -- teacher’s unions are quite active, for example. Though protests can sometimes be large, Moroccan security forces typically quell them before they escalate to violence. Businesses attempting to invest in the Western Sahara region are likely to face additional complications: Negotiations about the status of the region restarted in 2007, and a ceasefire has been in effect since 1991. Security forces are more likely to react swiftly against significant protest activity in Western Sahara, particularly if related to Moroccan control of the territory. Though there’s not much risk the situation will deteriorate, there might be short-term business disruptions."
}
```

Get country synopsis.

### HTTP Request

<a href="#get-threat-score" class="method post">POST</a> `/api/v3/content/country_synopsis`

### Request body parameters

Parameter | Default | Description
--- | --- | ---
country_code<br />*`string, required`* | | Country code

# Threat Score API

## Get threat score

```shell
curl --request POST \
  --url 'https://api.stratfor.com/api/v3/content/threat_score' \
  --header 'apiKey: YOUR_API_KEY' \
  --header 'Content-Type: application/json' \
  --data '{
    "timestamp": 1483392086
  }'
```

```php
<?php
$curl = curl_init();

$post_fields = array(
  "timestamp" => 1483392086,
);

curl_setopt_array($curl, array(
  CURLOPT_CUSTOMREQUEST => "POST",
  CURLOPT_URL => "https://api.stratfor.com/api/v3/content/threat_score",
  CURLOPT_HTTPHEADER => array(
    "apiKey: YOUR_API_KEY",
    "Content-Type: application/json"
  ),
  CURLOPT_POSTFIELDS => json_encode($post_fields),
  CURLOPT_RETURNTRANSFER => true,
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
}
else {
  echo $response;
}
```

> Response body:

```json
{
  "countries": [
    {
      "country_name": "Afghanistan",
      "tid": 115,
      "code": "AF",
      "scores": {
        "terror": {
          "label": "Terrorism and Insurgency",
          "current_score": {
            "value": 9,
            "created": 1506116356
          },
          "last_score": {
            "value": 9,
            "created": 1505761554
          },
          "trend_ranking": "increasing"
        },
        "crime": {
          "label": "Criminal Activity",
          "current_score": {
            "value": 9,
            "created": 1506116356
          },
          "last_score": {
            "value": 9,
            "created": 1505761554
          },
          "trend_ranking": "increasing"
        },
        "business": {
          "label": "Business Continuity",
          "current_score": {
            "value": 9,
            "created": 1506116356
          },
          "last_score": {
            "value": 9,
            "created": 1505761554
          },
          "trend_ranking": "stable"
        },
        "espionage": {
          "label": "Industrial Espionage",
          "current_score": {
            "value": 3,
            "created": 1506116356
          },
          "last_score": {
            "value": 3,
            "created": 1505761554
          },
          "trend_ranking": "stable"
        },
        "overall": {
          "label": "Overall Threat Score",
          "current_score": {
            "value": 9,
            "created": 1506116356
          },
          "last_score": {
            "value": 9,
            "created": 1505761554
          },
          "trend_ranking": "increasing"
        }
      }
    },
    {
      "country_name": "Albania",
      "tid": 62,
      "code": "AL",
      "scores": {
        "terror": {
          "label": "Terrorism and Insurgency",
          "current_score": {
            "value": 5,
            "created": 1503528169
          },
          "last_score": {
            "value": 5,
            "created": 1503528045
          },
          "trend_ranking": "stable"
        },
        "crime": {
          "label": "Criminal Activity",
          "current_score": {
            "value": 7,
            "created": 1503528169
          },
          "last_score": {
            "value": 7,
            "created": 1503528045
          },
          "trend_ranking": "stable"
        },
        "business": {
          "label": "Business Continuity",
          "current_score": {
            "value": 7,
            "created": 1503528169
          },
          "last_score": {
            "value": 7,
            "created": 1503528045
          },
          "trend_ranking": "stable"
        },
        "espionage": {
          "label": "Industrial Espionage",
          "current_score": {
            "value": 3,
            "created": 1503528169
          },
          "last_score": {
            "value": 3,
            "created": 1503528045
          },
          "trend_ranking": "stable"
        },
        "overall": {
          "label": "Overall Threat Score",
          "current_score": {
            "value": 7,
            "created": 1503528169
          },
          "last_score": {
            "value": 7,
            "created": 1503528045
          },
          "trend_ranking": "stable"
        }
      }
    },
    ... threat score data for another country ...
  ]
}
```

Get last and current threat scores of countries.

### HTTP Request

<a href="#get-threat-score" class="method post">POST</a> `/api/v3/content/threat_score`

### Request body parameters

Parameter | Default | Description
--- | --- | ---
timestamp<br />*`string, optional`* | {current-timestamp} - (60*60*24*30) | If the timestamp is specified, the last_score will be set to one at passed in timestamp.

# Search API

## Get search results

```shell
curl --request POST \
  --url 'https://api.stratfor.com/api/v3/search/param' \
  --header 'apiKey: YOUR_API_KEY' \
  --header 'Content-Type: application/json' \
  --data '{
    "lens_type": "Threat",  
    "page": 0,
    "limit": 5,
    ...
  }'
```

```php
<?php
$curl = curl_init();

$post_fields = array(
);

curl_setopt_array($curl, array(
  CURLOPT_CUSTOMREQUEST => "POST",
  CURLOPT_URL => "https://api.stratfor.com/api/v3/search/param",
  CURLOPT_HTTPHEADER => array(
    "apiKey: YOUR_API_KEY",
    "Content-Type: application/json"
  ),
  CURLOPT_POSTFIELDS => json_encode($post_fields),
  CURLOPT_RETURNTRANSFER => true,
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
}
else {
  echo $response;
}
```

> Response body:

```json
{
    "total_count": 889,
    "facet_counts": {
        "facet_queries": {},
        "facet_fields": {
            "sm_vid_WV_Topics": {},
            "sm_vid_WV_Themes": {},
            "sm_vid_Countries": {
                "Europe": 236,
                "France": 112,
                "Germany": 103,
                "Middle East and North Africa": 81,
                "Americas": 73,
                "Turkey": 71,
                "Spain": 63,
                "United Kingdom": 58,
                "Italy": 52,
                "United States": 52,
                "_empty_": 51,
                "Belgium": 47,
                "Greece": 45,
                "Eurasia": 39,
                "Russia": 37,
                "Asia-Pacific": 31,
                "Libya": 27,
                "Netherlands": 23,
                "Morocco": 20,
                "Sweden": 20,
                "Ukraine": 19,
                "Colombia": 17,
                "Iran": 17,
                "Sub-Saharan Africa": 17,
                "Israel": 16,
                "Austria": 15,
                "Iraq": 14,
                "Syria": 13,
                "Thailand": 11,
                "Brazil": 10,
                "China": 10,
                "Switzerland": 10,
                "Denmark": 9,
                "Philippines": 9,
                "Venezuela": 9,
                "Hungary": 8,
                "Mexico": 8,
                "Pakistan": 8,
                "Egypt": 7,
                "Nigeria": 7,
                "Poland": 7,
                "South Asia": 7,
                "Lebanon": 6,
                "South Korea": 6,
                "Tunisia": 6,
                "Bulgaria": 5,
                "Indonesia": 5,
                "Macedonia": 5,
                "North Korea": 5,
                "Serbia": 5,
                "Slovakia": 5,
                "Somalia": 5,
                "Albania": 4,
                "Australia": 4,
                "Jordan": 4,
                "Malaysia": 4,
                "Mali": 4,
                "Montenegro": 4,
                "Palestinian Territories": 4,
                "Portugal": 4,
                "Saudi Arabia": 4,
                "Yemen": 4,
                "Afghanistan": 3,
                "Algeria": 3,
                "Argentina": 3,
                "Bosnia and Herzegovina": 3,
                "Croatia": 3,
                "Czech Republic": 3,
                "Czechia": 3,
                "Ecuador": 3,
                "Ghana": 3,
                "India": 3,
                "Kenya": 3,
                "Kosovo": 3,
                "Kyrgyzstan": 3,
                "Romania": 3,
                "Bahrain": 2,
                "Bosnia-Herzegovina": 2,
                "Cambodia": 2,
                "Chad": 2,
                "Cyprus": 2,
                "Finland": 2,
                "Gambia": 2,
                "Guinea Bissau": 2,
                "Honduras": 2,
                "Iceland": 2,
                "Ireland": 2,
                "Ivory Coast": 2,
                "Kazakhstan": 2,
                "Lithuania": 2,
                "Malta": 2,
                "Niger": 2,
                "Norway": 2,
                "Paraguay": 2,
                "Peru": 2,
                "Senegal": 2,
                "Sierra Leone": 2,
                "Slovenia": 2,
                "Armenia": 1,
                "Azerbaijan": 1
            },
            "sm_vid_Article_Type": {},
            "sm_vid_Analysis_type": {},
            "sm_vid_Column_Type": {},
            "sm_vid_Video_Type": {},
            "sm_vid_Forecast_Type": {
                "Quarterly": 6,
                "Annual": 2
            },
            "sm_vid_Global_Perspectives_Type": {},
            "bundle": {
                "ioi": 524,
                "lens_item_of_interest": 167,
                "lens_incident_report": 92,
                "lens_analysis": 84,
                "lens_forecast": 8,
                "lens_perspective": 8,
                "lens_report": 6
            },
            "sm_opencalais_name": {},
            "ss_threatlens_content_label": {
                "Item of Interest": 525,
                "Intelligence Update": 234,
                "Analysis": 92,
                "Forecast": 8,
                "Report": 5
            },
            "sm_vid_Threat_Type": {
                "Criminal Activity": 378,
                "Business Continuity": 304,
                "Terrorism and Insurgency": 234,
                "Other": 57,
                "Industrial Espionage": 27
            }
        },
        "facet_dates": {
            "ds_created": {
                "2008-07-01T00:00:00Z": 1,
                "2012-02-01T00:00:00Z": 1,
                "2013-02-01T00:00:00Z": 1,
                "2014-04-01T00:00:00Z": 1,
                "2014-08-01T00:00:00Z": 1,
                "2014-09-01T00:00:00Z": 3,
                "2014-11-01T00:00:00Z": 1,
                "2015-02-01T00:00:00Z": 1,
                "2015-04-01T00:00:00Z": 1,
                "2015-06-01T00:00:00Z": 2,
                "2015-07-01T00:00:00Z": 1,
                "2015-08-01T00:00:00Z": 3,
                "2015-09-01T00:00:00Z": 1,
                "2015-11-01T00:00:00Z": 8,
                "2016-01-01T00:00:00Z": 6,
                "2016-02-01T00:00:00Z": 16,
                "2016-03-01T00:00:00Z": 14,
                "2016-04-01T00:00:00Z": 39,
                "2016-05-01T00:00:00Z": 17,
                "2016-06-01T00:00:00Z": 20,
                "2016-07-01T00:00:00Z": 34,
                "2016-08-01T00:00:00Z": 33,
                "2016-09-01T00:00:00Z": 35,
                "2016-10-01T00:00:00Z": 37,
                "2016-11-01T00:00:00Z": 48,
                "2016-12-01T00:00:00Z": 40,
                "2017-01-01T00:00:00Z": 25,
                "2017-02-01T00:00:00Z": 24,
                "2017-03-01T00:00:00Z": 36,
                "2017-04-01T00:00:00Z": 25,
                "2017-05-01T00:00:00Z": 37,
                "2017-06-01T00:00:00Z": 29,
                "2017-07-01T00:00:00Z": 41,
                "2017-08-01T00:00:00Z": 38,
                "2017-09-01T00:00:00Z": 26,
                "2017-10-01T00:00:00Z": 30,
                "2017-11-01T00:00:00Z": 20,
                "2017-12-01T00:00:00Z": 39,
                "2018-01-01T00:00:00Z": 27,
                "2018-02-01T00:00:00Z": 27,
                "2018-03-01T00:00:00Z": 21,
                "2018-04-01T00:00:00Z": 23,
                "2018-05-01T00:00:00Z": 30,
                "2018-06-01T00:00:00Z": 27,
                "gap": "+1MONTH",
                "start": "2008-07-01T00:00:00Z",
                "end": "2018-08-01T00:00:00Z"
            }
        },
        "facet_ranges": {},
        "facet_intervals": {},
        "facet_dates_years": {
            "ds_created": {
                "gap": "+1YEAR",
                "start": "2008-07-01T00:00:00Z",
                "end": "2018-08-01T00:00:00Z",
                "2008-01-01T00:00:00Z": 1,
                "2012-01-01T00:00:00Z": 1,
                "2013-01-01T00:00:00Z": 1,
                "2014-01-01T00:00:00Z": 6,
                "2015-01-01T00:00:00Z": 17,
                "2016-01-01T00:00:00Z": 339,
                "2017-01-01T00:00:00Z": 370,
                "2018-01-01T00:00:00Z": 155
            }
        }
    },
    "nodes": [
        {
            "id": "hak4nf/ioi/8aebf853-90cb-40f5-812c-7040d6d80aef",
            "bundle": "ioi",
            "label": "Migrants continue entering France along alpine routes in Pian del Colle",
            "ds_created": "2018-06-30T23:06:00Z",
            "ds_changed": "2018-07-02T07:07:25Z",
            "tid": [
                80,
                422
            ],
            "ss_reportedby_name": "",
            "zs_detail": "<p>The latest route into France used by migrants is increasingly coming to the attention of populist Right-wing political groups that have risen to prominence on the back of Europe's migrant crisis.</p>",
            "zs_summary": "Migrants continue entering France along alpine routes in Pian del Colle",
            "ss_threatlens_content_label": "Item of Interest",
            "score": 1.4512062,
            "taxonomy": [
                {
                    "tid": "80",
                    "vid": "5",
                    "v_name": "countries",
                    "name": "Italy",
                    "code": "IT",
                    "path_alias": "/region/europe/italy"
                },
                {
                    "tid": "422",
                    "vid": "21",
                    "v_name": "threat_type",
                    "name": "Criminal Activity",
                    "path_alias": "/taxonomy/term/422"
                }
            ]
        }
    ]
}
```

Search Threat Lens contents.

### HTTP Request

<a href="#get-search-result" class="method post">POST</a> `/api/v3/search/param`

### Request body parameters

Parameter | Default | Description
--- | --- | ---
lens_type<br />*`string, required`* | | Type of Stratfor Lens product.<br />**Available options:**<br />Threat<br />...
page<br />*`integer, optional`* | 0 |The page number to start with.<br />0 = First page<br />1 = Second page<Br />and, so on.
limit<br />*`integer, optional`* | 10 | The number of items to return in the response.
... | ... | ...
