![](./images/ahlsbanner.png)

# A-HLS Product Grid Documentation 

## Overview

insOsGridProductSelection LWC is designed for underwriters, brokers, and sales executives who select, compare and add products to a cart for final purchase or quoting.

A complex LWC called [insOsGridProductSelection](https://help.salesforce.com/s/articleView?id=ind.v_health_t_use_the_insosgridproductselection_lwc_482515.htm&type=5)  is used to provide this functionality as part of the Vlocity Insurance package (vlocity_ins). This Accelerator is a sample configuration of this LWC with detailed configuration documentation.

This accelerator does not cover how to create products. Before you use this Accelerator, it is recommended that you configure your products. We have provided a separate Accelerator that contains sample product templates for your use: https://github.com/healthcare-and-life-sciences/ins-products 

We have created sample pricing engines that show how to use [Expression sets](https://help.salesforce.com/s/articleView?id=sf.expression_sets.htm&type=5) for pricing but these are example EP's that are not real pricing engines. Again the idea here is to show how the data is passed between the product grid and expression set, not to implement an actual pricing engine. 

The following is an example of the product grid with sample product data. 



![Sample](./images/sample.png)



When you look at the sample, you will see that depending on the type of insurance (Small Group, Invidual, Medicare), a user can input different data which is passed to the expression set. The following values show different data which is captured based on the type of insurance. 



![Small Group](./images/smallgroup.png)



![individual](./images/individual.png)



![Medicare](./images/medicare.png)



### JSON Configuration . 

Configuration steps for the JSON are found here: [insOsGridProductSelection](https://help.salesforce.com/s/articleView?id=ind.v_health_t_use_the_insosgridproductselection_lwc_482515.htm&type=5). Please refer to the below for the detailed break-down of the configuration options.





``` json
{
  "bStandalone": false,
  "conditionType": "Hide if False",
  "controlWidth": 12,
  "customAttributes": [
    {
      "name": "pre-filter",
      "source": "%medicalFilters%"
    },
    {
      "name": "census-json",
      "source": ""
    },
    {
      "name": "concurrent-batch-request",
      "source": "3"
    },
    {
      "name": "load-batch-size",
      "source": "1"
    },
    {
      "name": "max-compare-products",
      "source": "4"
    },
    {
      "name": "sort-field",
      "source": "GroupPremiumEmployer:Premium"
    },
    {
      "name": "show-product-tile",
      "source": "true"
    }
  ],
  "disOnTplt": false,
  "filtersConfig": {
    "inPageFilters": [
      "SG_annualOOP_INN:Out of Pocket",
      "SG_primaryCare_INN:Office Visit",
      "SG_annualDed_INN:Deductible",
      "SG_coinsurance_INN:Coinsurance"
    ],
    "serviceFilters": {
      "SubType__c": {
        "attributeLabel": "Sub Type",
        "attributeName": "SubType__c",
        "attributeObject": "vlocity_ins__SubType__c",
        "listOfValues": [
          {
            "label": "HMO",
            "value": "HMO"
          },
          {
            "label": "PPO",
            "value": "PPO"
          }
        ]
      },
      "Tier__c": {
        "attributeLabel": "Tier",
        "attributeName": "Tier__c",
        "attributeObject": "vlocity_ins__Tier__c",
        "listOfValues": [
          {
            "label": "Gold",
            "value": "Gold"
          },
          {
            "label": "Silver",
            "value": "Silver"
          },
          {
            "label": "Bronze",
            "value": "Bronze"
          }
        ]
      }
    }
  },
  "hide": false,
  "initAction": {
    "className": "InsProductService",
    "inputMap": {
      "userInputs": {
        "VH-SG-Census-RF.SG_empOnlyCount": "%SmallGroup:EmpOnlyCount%",
        "VH-SG-Census-RF.SG_empChildrenCount": "%SmallGroup:EempChildrenCount%",
        "VH-SG-Census-RF.SG_empSpouseCount": "%SmallGroup:EmpSpouseCount%",
        "VH-SG-Census-RF.SG_empFamilyCount": "%SmallGroup:EmpFamilyCount%",
        "VH-SG-Census-RF.SG_CM_Age": 40,
        "VH-SG-Census-RF.SG_CA_RatingType": "Average",
        "VH-SG-Census-RF.VisContribution": 50,
        "VH-SG-Census-RF.MedContribution": 75,
        "VH-SG-Census-RF.DenContribution": 50,
        "VH-SG-Census-RF.SG_totalDependents": "0",
        "VH-SG-Census-RF.SG_primaryMember": "true"
      }
    },
    "methodName": "getEligibleProducts",
    "optionsMap": {
      "filters": "vlocity_ins__Type__c:%InsuranceType%,vlocity_ins__MarketSegment__c:%InsurancePlan%",
      "rootPricingOnly": true,
      "ruleAttributeSetValues": false
    }
  },
  "label": "LWCinsOsGridProductSelectionMedicalTile",
  "lwcName": "vlocity_ins__insOsGridProductSelection",
  "productConfig": {
    "config": {
      "None": {
        "attributes": [
          {
            "fields": [
              "GroupPremiumEmployer"
            ],
            "label": "Employer Cost",
            "width": 1
          },
          {
            "fields": [
              "GroupPremiumEmployee"
            ],
            "label": "Employee Cost",
            "width": 1
          },
          {
            "fields": [
              "SG_annualDed_INN"
            ],
            "label": "Deductible",
            "width": 1
          },
          {
            "fields": [
              "SG_coinsurance_INN"
            ],
            "label": "Coinsurance",
            "width": 1
          },
          {
            "fields": [
              "SG_annualOOP_INN"
            ],
            "label": "Out of Pocket",
            "width": 1
          },
          {
            "fields": [
              "SG_primaryCare_INN"
            ],
            "label": "Office Visit",
            "width": 1
          }
        ]
      }
    },
    "fieldKeyName": "Family",
    "placeholders": [
      {
        "isHidden": false,
        "label": "Find A Dentist",
        "url": "https://www.google.com/"
      },
      {
        "isHidden": false,
        "label": "Summary of Benefits",
        "url": "https://www.yahoo.com/"
      },
      {
        "isHidden": false,
        "label": "Find A Dentist In San Francisco",
        "url": "https://www.google.com/"
      }
    ]
  },
  "rePriceAction": {
    "className": "InsProductService",
    "methodName": "rePriceProduct",
    "optionsMap": {
      "evalOptionalCoverageRelationship": true,
      "includeRawCalculationResult": true
    },
    "vlocityAsync": true
  },
  "show": null
}
```



Now, we will go through each part of the JSON and explain what each root node does. 

**ProductConfig** 

The following JSON

```json
"productConfig": {
    "config": {
      "None": {
        "attributes": [
          {
            "fields": [
              "GroupPremiumEmployer"
            ],
            "label": "Employer Cost",
            "width": 1
          },
          {
            "fields": [
              "GroupPremiumEmployee"
            ],
            "label": "Employee Cost",
            "width": 1
          },
          {
            "fields": [
              "SG_annualDed_INN"
            ],
            "label": "Deductible",
            "width": 1
          },
          {
            "fields": [
              "SG_coinsurance_INN"
            ],
            "label": "Coinsurance",
            "width": 1
          },
          {
            "fields": [
              "SG_annualOOP_INN"
            ],
            "label": "Out of Pocket",
            "width": 1
          },
          {
            "fields": [
              "SG_primaryCare_INN"
            ],
            "label": "Office Visit",
            "width": 1
          }
        ]
      }
    }
```



Is used to display Standout Features on the LWC

![standoutfeatures](./images/standoutfeatures.png)





------

## Package Includes:

### **OmniScript**

You will find 2 OS in the /Omnistudio folder

**productGrid**

This OS shows how to display different insurance groups and different products. Primary purpose of this OS is to show how data is passed to the backend. 

**productGridNoConfig**

This OS shows how to hide the config Panel. 

![](./images/HideConfigPlan.png)

This is done by adding the follwing manual over ride css



```
.vloc-ins-action-container
	.vloc-ins-product-actions
	button.slds-button_neutral {
	display: none;
}
```



as a static resource, lets call it hidenInsConfigBtn then on the OS setup you will add the css reousrce name in "Custom Lightning Stylesheet File Name"





------

## Configuration Requirements

### Pre-Install Configuration Steps:

#### Install the Data Pack

1. Follow the download steps presented on the Accelerate HLS website for this Accelerator. 

2. 1. Alternatively, you may download the Data Pack folder in the following GitHub repository: **https://github.com/healthcare-and-life-sciences/ins-products-grid**

3. Then, complete the following steps to import them into your Salesforce org.

4. 1. To Import, in your destination Salesforce org, Click on **App Launcher** → Search for '**OmniStudio DataPacks**' and click on it.
   2. Click on '**Installed**' and on the right side click on '**Import from**'.
   3. Select '**From File**' - When the window opens, select the Data Pack file that you downloaded and stored on your machine. 
      1. productGrid.json
      2. productGridConfig.json
   4. Click '**Install**'.
   5. When prompted to Activate the OmniScript, choose **Not Now**.

### Post-Install Configuration Steps:

1. Install Vlocity Insurance (vlocity_ins)

2. Please make sure you have installed sample HLS Insurance products https://github.com/healthcare-and-life-sciences/ins-products

3. **[IF YOUR DATAPACK HAS OMNISCRIPTS - INCLUDE THE FOLLOWING STEPS]** 

4. Click on **App Launcher** → Search for “OmniScripts”

5. 1. Navigate to the recently installed OmniScript in the list view
   2. Click on the dropdown at the right of the OmniScript and select **Activate**.
   3. For more information regarding activating Omniscripts, please see this article: https://help.salesforce.com/s/articleView?id=sf.os_activating_omniscripts.htm&type=5

6. Add the installed OmniScript to the lightning page layout of your choosing. 

7. 1. Refer to this article for more information regarding adding OmniScripts to a Lightning Page: https://help.salesforce.com/s/articleView?id=sf.os_add_a_standard_omniscript_component_to_a_lighting_page_20263.htm&type=5
   2. Refer to this article for more information regarding adding OmniScripts to an Experience Cloud Page: https://help.salesforce.com/s/articleView?id=sf.os_add_a_standard_omniscript_component_to_an_experience_page_20341.htm&type=5

8. **[IF YOUR DATAPACK HAS FLEXCARDS - INCLUDE THE FOLLOWING STEPS]**

9. Click on **App Launcher** → Search for “FlexCards”

10. 1. Navigate to the recently installed FlexCard in the list view

   11. Open the FlexCard

   12. Click **Activate** and select the appropriate Publish Options

   4. For more information regarding activating FlexCards, please see this article: https://help.salesforce.com/s/articleView?id=sf.os_activateconfigureand_publish_flexcards_24744.htm&type=5

11. Add the installed FlexCard to the lightning page layout of your choosing.

15. 1. Refer to the following articles for more information regarding adding FlexCards to a Lightning or Experience page: 

    2. 1. https://docs.vlocity.com/en/Add-a-FlexCard-to-a-Lightning-Page.html
       2. https://docs.vlocity.com/en/Add-a-FlexCard-to-an-Experience-Page.html

    

------

## Assumptions

1. Install products from https://github.com/healthcare-and-life-sciences/ins-products
2. A customer has licenses for Health Cloud, and the HINS Managed Package with OmniStudio. These solutions have all been installed and are functional.
3. A customer is assuming Salesforce Lightning Experience — not Classic.
4. Data Model elements that are part of the HINS (Vlocity) Managed package and Health Cloud are all available.
5. The Accelerator uses the Lightning Design System standards and look. Customers may want to apply their own branding which can be achieved.

------

- ## Revision History

  * **December 23, 2022**
  * Initial check in with support for Small Group, Invidiual and Medicare
