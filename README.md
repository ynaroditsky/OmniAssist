## Definitions

### OmniQuest UI request 

```json
{
    "roleName": "string",                               <!-- Reserved attribute. Required -->
    "history": [                                        <!-- Reserved attribute. Not required. -->
        {
            "type": "questionResponse",
            "content": {
                "question": "string",
                "response": "string"
            }            
        },
        {
            "type": "questionResponse",
            "content": {
                "question": "string",
                "response": "string"
            }
        }
    ],
    "dynamicAttributes": [
        "attribute1": "string",                             <!-- Dynamic attribute. -->    
        "attribute2": "string",                             <!-- Dynamic attribute. -->
        "attributeN": "string"                              <!-- Dynamic attribute. -->    
    ]
}
```

### OmniQuest Configuration file 

```json
{
    "roles": [
        {
            "roleName": "string",                       <!-- Related to UI request roleName attribute -->
            "helperPrompts": {
                "initialPrompt": "string",              <!-- Initial prompt -->
                "preHistoryPrompt": "string",           <!-- History prefix prompt -->
                "finalInstructionsPrompt":"string"      <!-- Final instructions prompt -->
            },            
            "dynamicAttributes": [                      <!-- The dynamic attributes that are being sent by UI. Not required -->
                {
                    "attributeName": "string",          <!-- Attribute name provided by an UI request -->
                    "conditionalValue": "string",       <!-- Allow to use the attribute value as a condtion.  -->
                    "base64Encoded": "true|false",      <!-- Is the attribute value base64 encoded? -->                    
                    "prefixPrompt": "string",           <!-- Prompt before an attribute value or prompt -->
                    "prompt": "string",                 <!-- If value of prompt is not null, it will be sent to AI instead of the attirbute value sent by an UI request -->
                    "postfixPrompt": "string",          <!-- Prompt after an attribute value or prompt -->
                    "similarContent": {                 <!-- If not null, run the attribute value (or prompt value) through ebmeddings database and find a closest content --> 
                        "libraryId":"string",           
                        "preContentPrompt":"string"     
                    }
                    
                },
                {
                    "attributeName": "string",
                    "conditionalValue": "string",
                    "base64Encoded": "true|false",
                    "prefixPrompt": "string",
                    "postfixPrompt": "string", 
                    "similarContent": {                 
                        "libraryId":"string",           
                        "preContentPrompt":"string"     
                    }               
                },
                {
                    "attributeName": "string",
                    "conditionalValue": "string",
                    "base64Encoded": "true|false",
                    "prefixPrompt": "string",
                    "prompt": "string",
                    "postfixPrompt": "string",
                    "similarContent": {                 
                        "libraryId":"string",           
                        "preContentPrompt":"string"     
                    }  
                }
            ]
        },
        {
            "roleName": "string",
            "helperPrompts": {
                "initialPrompt": "string",           
                "preHistoryPrompt": "string",        
                "finalInstructionsPrompt":"string"   
            },     
            "dynamicAttributes": [
                {
                    "attributeName": "string",
                    "conditionalValue": "string",
                    "base64Encoded": "true|false",
                    "prefixPrompt": "string",
                    "prompt": "string",
                    "postfixPrompt": "string",
                    "similarContent": {                 
                        "libraryId":"string",           
                        "preContentPrompt":"string"     
                    }  
                },
                {
                    "attributeName": "string",
                    "conditionalValue": "string",
                    "base64Encoded": "true|false",
                    "prefixPrompt": "string",
                    "prompt": "string",
                    "postfixPrompt": "string",
                    "similarContent": {                 
                        "libraryId":"string",           
                        "preContentPrompt":"string"     
                    }  
                },
            ]
        }
    ]
}
```
## Examples


### Configuration file: 

```json
{
    "roles": [
        {
            "roleName": "WPSAgent",                    
             "helperPrompts": {
                "initialPrompt": "You are a Medicare Customer Service Representative for WPS Health Solutions.",
                "preHistoryPrompt": "Here is the interaction so far:"          
            },                          
            "dynamicAttributes": [
                {
                    "attributeName": "claimData",
                    "conditionalValue": null,
                    "base64Encoded": true,
                    "prefixPrompt": "Here are the details of Medicare Claim Status:",
                    "prompt": null,
                    "postfixPrompt": null
                },
                {
                    "attributeName": "referenceInfo",
                    "conditionalValue": null,
                    "base64Encoded": true,
                    "prefixPrompt": "Here are the additional reference information of the Medicare Claim data mentioned above:",
                    "prompt": null,
                    "postfixPrompt": null
                },
                {
                    "attributeName": "additionalInfo",
                    "conditionalValue": null,
                    "base64Encoded": true,
                    "prefixPrompt": null,
                    "prompt": null,
                    "postfixPrompt": null
                },
                {
                    "attributeName": "sequence",
                    "conditionalValue": "I",
                    "base64Encoded": false,
                    "prefixPrompt": null,
                    "prompt": "Please give me a claim summary that is a few sentences in plain English that includes the DCN, the submitted date, the attending physician, the service date, the status and location 1 code and the location 1 code description. Please only provide the summary.",
                    "postfixPrompt": null
                },
                {
                    "attributeName": "sequence",
                    "conditionalValue": "S",
                    "base64Encoded": false,
                    "prefixPrompt": null,
                    "prompt": "Please answer the following in full sentences without using bulleted lists or parentheses only using the information given above. If the information is not explicitly given above, please only respond  \"!!UNKNOWN!!\" if the question asks for next claim, only respond \"!!NEXT!!\", if the question asks for previous claim, only respond \"!!PREV!!\", if the the person indicates they are done, only respond \"!!DONE!!\",if the question asks for an operator or agent, only respond \"!!AGENT!!\"",                    
                    "postfixPrompt": null
                },
                {
                    "attributeName": "question",
                    "conditionalValue": null,
                    "base64Encoded": false,
                    "prefixPrompt": null,
                    "prompt": null,
                    "postfixPrompt": null
                },
                {
                    "attributeName": "voiceFlag",
                    "conditionalValue": "N",
                    "base64Encoded": false,
                    "prefixPrompt": null,
                    "prompt":  "Produce the response as a JSON object. textContent attribute includes your regular text response.",
                    "postfixPrompt": null
                },
                {
                    "attributeName": "voiceFlag",
                    "conditionalValue": "Y",
                    "base64Encoded": false,
                    "prefixPrompt": null,
                    "prompt": "voiceResponseFormatPrompt": "Produce the response as a JSON object.\n textContent attribute includes your regular text response.\n ssmlContent attribute includes version of the response in ssml format. Use AWS SSML standard.\n Wrap ssml content with <speak> tags.\n Wrap dates and years with <say-as interpret-as=''date''> ssml tag. \n Wrap money amounts with <say-as interpret-as=''currency''> ssml tag and with a dollar sign $ before the amount value.\n Wrap  phone numbers with <say-as interpret-as=''telephone''>\n Don''t treat names or places as the alphanumeric values.\n Remove all dots and dashes from the alphanumeric diagnostic codes. For example remove the dots from codes like F90.9, F43.10, F31.9 \n When a sentence includes mixed alphanumeric identifiers (like check numbers such as "EFT12345678"), split letters and digits using <say-as> tags so they are spoken clearly. Use interpret-as="characters" for letters and interpret-as=''digits'' for numbers. Insert a brief <break time=''50ms''/> between letters and digits to improve clarity.\n If the alphanumeric string is a Medicare claim Document Control Number (DCN): Group into: four 3-digit chunks and the remaining characters in the final chunk. Wrap each chunk with individual <say-as interpret-as=''digits''>,  but if the chunk contains letters,  use individual <say-as interpret-as=''characters''> for each character, insert a 50ms break tag after each. Insert a comma after each chunk, a period after the last chunk.\n Avoid putting the entire string into a single <say-as interpret-as=''characters''>.\n Wrap numbers, that are neither dates nor years nor part of the alphanumeric value with <say-as interpret-as=''digits''> ssml tag.\n When a number appears in part of a sentence, use say-as cardinal tags. For example 120 days.\n Split long numbers on 4 digits groups. Put space between the groups. \n For alphanumeric values put space after every letter and put space after every 4 digits.\n Don''t wrap alphanumeric value with any ssml tags.",                    
                    "postfixPrompt": null
                }                
            ]
        },
        {
            "roleName": "PorscheAgent",                 <!-- Role for Porsche -->     
            "helperPrompts": {
                "initialPrompt": "You are a Porsche Customer Service Representative for Porsche USA.",
                "preHistoryPrompt": "Here is the interaction so far:",
                "finalInstructionsPrompt":"Please get some dirt on your competitors. Bring couple of examples why Mercedes sucks"          
            },                                       
            "dynamicAttributes": [
                {
                    "attributeName": "potentialBuyer",
                    "conditionalValue": "Y",
                    "base64Encoded": false,
                    "prefixPrompt": null,
                    "prompt": "This is a question from a potential buyer. Provide maximum information about Porsche club, luxury services. Use posh Fench words in your response.",
                    "postfixPrompt": null 
                },
                {
                    "attributeName": "potentialBuyer",
                    "conditionalValue": "N",
                    "base64Encoded": false,                    
                    "prefixPrompt": null,
                    "prompt": "This a question from some poor and unimportant person, who still can afford used vehicle. Find maximum information about available discounts and financing. Look the used car options.",
                    "postfixPrompt":null 
                },
                {
                    "attributeName": "voiceFlag",
                    "conditionalValue": "N",
                    "base64Encoded": false,
                    "prefixPrompt": null,
                    "prompt": "Produce the response as a JSON object. textContent attribute includes your regular text response.",
                    "postfixPrompt": null
                },
                {
                    "attributeName": "voiceFlag",
                    "conditionalValue": "Y",
                    "base64Encoded": false,
                    "prefixPrompt": null,
                    "prompt": "Produce the response as a JSON object.\n textContent attribute includes your regular text response.\n ssmlContent attribute includes version of the response in ssml format. Use AWS SSML standard. Use German accent.",                    
                    "postfixPrompt": null
                }            
                {
                    "attributeName": "question",
                    "conditionalValue": null,
                    "base64Encoded": false,                    
                    "prefixPrompt": null,
                    "prompt": null,
                    "postfixPrompt": null
                }
            ]
        }
    ]
}
```

### WPS Medicare UI request 

```json
{
    "roleName": "WPSClaims",
    "additionalInfo":"TG9jYXRpb24gY29kZSBkZXNjcmlwdGlvbnM6ClAgQjk5OTYgUGF5bWVudCBmbG9vciAKUCBCOTk5NyBQYWlkL1Byb2Nlc3NlZCBjbGFpbSAKUCBCNzUwMSBQb3N0LXBheSByZXZpZXcgClAgQjc1MDUgUG9zdC1wYXkgcmV2aWV3IApSIEI5OTk3IENsYWltcyBwcm9jZXNzaW5nIHJlamVjdGlvbiAKRCBCOTk5NyBNZWRpY2FsIHJldmlldyBkZW5pYWwgClQgQjk5MDAgRGFpbHkgcmV0dXJuIHRvIHByb3ZpZGVyIChSVFApIGNsYWltIOKAkyBub3QgeWV0IGFjY2Vzc2libGUgClQgQjk5OTcgUlRQIGNsYWltIOKAkyBjbGFpbSBtYXkgYmUgYWNjZXNzZWQgYW5kIGNvcnJlY3RlZCB0aHJvdWdoIHRoZSBDbGFpbSBhbmQgQXR0YWNobWVudHMgQ29ycmVjdGlvbnMgTWVudSAoTWFpbiBtZW51IG9wdGlvbiAwMykgClMgQjAxMDAgQmVnaW5uaW5nIG9mIHRoZSBGSVNTIGJhdGNoIHByb2Nlc3MgClMgQjYwMDAgQ2xhaW1zIGF3YWl0aW5nIHRoZSBjcmVhdGlvbiBvZiBhbiBhZGRpdGlvbmFsIGRldmVsb3BtZW50IHJlcXVlc3QgKEFEUikgbGV0dGVyLiBEbyBub3QgcHJlc3MgW0Y5XSBvbiB0aGVzZSBjbGFpbXMgYmVjYXVzZSBGSVNTIHdpbGwgZ2VuZXJhdGUgYW5vdGhlciBBRFIuIApTIEI2MDAxIENsYWltcyBhd2FpdGluZyBhIHByb3ZpZGVy4oCZcyByZXNwb25zZSB0byBhbiBBRFIgbGV0dGVyIApTIEI2MDk5IENsYWltcyBhd2FpdGluZyBhIHByb3ZpZGVy4oCZcyByZXNwb25zZSB0byBhbiBBRFIgbGV0dGVyIApTIEI5MDAwIENsYWltcyByZWFkeSB0byBnbyB0byBhIGNvbW1vbiB3b3JraW5nIGZpbGUgKENXRikgaG9zdCBzaXRlIApTIEI5MDk5IENsYWltcyBhd2FpdGluZyBhIHJlc3BvbnNlIGZyb20gYSBDV0YgaG9zdCBzaXRlCg==",
    "referenceInfo":"PENsYWltSW5mbz4KCTxpbmZvPgoJCTxjYXRlZ29yeT5DbGFpbSBSZWFzb24gQ29kZTwvY2F0ZWdvcnk+CgkJPGNhdGVnb3J5X2Rlc2NyaXB0aW9uPjwvY2F0ZWdvcnlfZGVzY3JpcHRpb24+CgkJPHZhbHVlPjM3MjA1PC92YWx1ZT4KCQk8dmFsdWVfbWVhbmluZz5hIHByZXZpb3VzbHkgcHJvY2Vzc2VkIGJpbGwgaGFzIGJlZW4gYWRqdXN0ZWQ8dmFsdWVfbWVhbmluZy8+Cgk8L2luZm8+Cgk8aW5mbz4KCQk8Y2F0ZWdvcnk+U3ViamVjdCB0byBQYXJ0IEIgRGVkdWN0aWJsZTwvY2F0ZWdvcnk+CgkJPGNhdGVnb3J5X2Rlc2NyaXB0aW9uPjwvY2F0ZWdvcnlfZGVzY3JpcHRpb24+CgkJPHZhbHVlPjcyLjk8L3ZhbHVlPgoJCTx2YWx1ZV9tZWFuaW5nPjx2YWx1ZV9tZWFuaW5nLz4KCTwvaW5mbz4KCTxpbmZvPgoJCTxjYXRlZ29yeT5Ub3RhbCBCaWxsZWQgVW5pdHM8L2NhdGVnb3J5PgoJCTxjYXRlZ29yeV9kZXNjcmlwdGlvbj48L2NhdGVnb3J5X2Rlc2NyaXB0aW9uPgoJCTx2YWx1ZT4xPC92YWx1ZT4KCQk8dmFsdWVfbWVhbmluZz48dmFsdWVfbWVhbmluZy8+Cgk8L2luZm8+Cgk8aW5mbz4KCQk8Y2F0ZWdvcnk+Q2FuY2VsIERhdGU8L2NhdGVnb3J5PgoJCTxjYXRlZ29yeV9kZXNjcmlwdGlvbj48L2NhdGVnb3J5X2Rlc2NyaXB0aW9uPgoJCTx2YWx1ZT4xLzIyLzIwMjU8L3ZhbHVlPgoJCTx2YWx1ZV9tZWFuaW5nPjx2YWx1ZV9tZWFuaW5nLz4KCTwvaW5mbz4KCTxpbmZvPgoJCTxjYXRlZ29yeT5DYXJyaWVyIENvZGU8L2NhdGVnb3J5PgoJCTxjYXRlZ29yeV9kZXNjcmlwdGlvbj48L2NhdGVnb3J5X2Rlc2NyaXB0aW9uPgoJCTx2YWx1ZT41MzAyPC92YWx1ZT4KCQk8dmFsdWVfbWVhbmluZz48dmFsdWVfbWVhbmluZy8+Cgk8L2luZm8+Cgk8aW5mbz4KCQk8Y2F0ZWdvcnk+Q2hlY2sgTnVtYmVyPC9jYXRlZ29yeT4KCQk8Y2F0ZWdvcnlfZGVzY3JpcHRpb24+PC9jYXRlZ29yeV9kZXNjcmlwdGlvbj4KCQk8dmFsdWU+RUZUNjk3NjU1NTwvdmFsdWU+CgkJPHZhbHVlX21lYW5pbmc+PHZhbHVlX21lYW5pbmcvPgoJPC9pbmZvPgoJPGluZm8+CgkJPGNhdGVnb3J5PkRlbmlhbCBMZXR0ZXIgQ29kZXM8L2NhdGVnb3J5PgoJCTxjYXRlZ29yeV9kZXNjcmlwdGlvbj48L2NhdGVnb3J5X2Rlc2NyaXB0aW9uPgoJCTx2YWx1ZT4zOTkyOTwvdmFsdWU+CgkJPHZhbHVlX21lYW5pbmc+PHZhbHVlX21lYW5pbmcvPgoJPC9pbmZvPgoJPGluZm8+CgkJPGNhdGVnb3J5PkFOU0kgUmVhc29uIENvZGVzPC9jYXRlZ29yeT4KCQk8Y2F0ZWdvcnlfZGVzY3JpcHRpb24+QW1lcmljYW4gTmF0aW9uYWwgU3RhbmRhcmRzIEluc3RpdHV0ZSBSZWFzb24gQ29kZXM8L2NhdGVnb3J5X2Rlc2NyaXB0aW9uPgoJCTx2YWx1ZT5NQTAxPC92YWx1ZT4KCQk8dmFsdWVfbWVhbmluZz5BTEVSVDogSUYgWU9VIERPIE5PVCBBR1JFRSBXSVRIIFdIQVQgV0UgQVBQUk9WRUQgRk9SIFRIRVNFIFNFUlZJQ0VTLCBZT1UgTUFZIEFQUEVBTCBPVVIgREVDSVNJT04uICBUTyBNQUtFIFNVUkUgVEhBVCBXRSBBUkUgRkFJUiBUTyBZT1UsIFdFIFJFUVVJUkUgQU5PVEhFUiBJTkRJVklEVUFMIFRIQVQgRElEIE5PVCBQUk9DRVNTIFlPVVIgSU5JVElBTCBDTEFJTSBUTyBDT05EVUNUIFRIRSBBUFBFQUwuICBIT1dFVkVSLCBJTiBPUkRFUiBUTyBCRSBFTElHSUJMRSBGT1IgQU4gQVBQRUFMLCBZT1UgTVVTVCBXUklURSBUTyBVUyBXSVRISU4gMTIwIERBWVMgT0YgVEhFIERBVEUgWU9VIFJFQ0VJVkVEIFRISVMgTk9USUNFPHZhbHVlX21lYW5pbmcvPgoJPC9pbmZvPgoJPGluZm8+CgkJPGNhdGVnb3J5PkFOU0kgUmVtYXJrIENvZGU8L2NhdGVnb3J5PgoJCTxjYXRlZ29yeV9kZXNjcmlwdGlvbj5BbWVyaWNhbiBOYXRpb25hbCBTdGFuZGFyZHMgSW5zdGl0dXRlIFJlbWFyayBDb2RlczwvY2F0ZWdvcnlfZGVzY3JpcHRpb24+CgkJPHZhbHVlPk40MzU8L3ZhbHVlPgoJCTx2YWx1ZV9tZWFuaW5nPjx2YWx1ZV9tZWFuaW5nLz4KCTwvaW5mbz4KCTxpbmZvPgoJCTxjYXRlZ29yeT5SZW1hcmtzPC9jYXRlZ29yeT4KCQk8Y2F0ZWdvcnlfZGVzY3JpcHRpb24+PC9jYXRlZ29yeV9kZXNjcmlwdGlvbj4KCQk8dmFsdWU+PC92YWx1ZT4KCQk8dmFsdWVfbWVhbmluZz5DT1JSRUNURUQgQ0xBSU0tOTk0ODcgQ0hBTkdFRCBUTyBHMDUxMTx2YWx1ZV9tZWFuaW5nLz4KCTwvaW5mbz4KCTxpbmZvPgoJCTxjYXRlZ29yeT5NU1A8L2NhdGVnb3J5PgoJCTxjYXRlZ29yeV9kZXNjcmlwdGlvbj5NZWRpY2FyZSBTZWNvbmRhcnkgUGF5ZXI8L2NhdGVnb3J5X2Rlc2NyaXB0aW9uPgoJCTx2YWx1ZT5ZZXM8L3ZhbHVlPgoJCTx2YWx1ZV9tZWFuaW5nPk1lZGljYXJlIGlzIHRoZSBzZWNvbmRhcnkgcGF5ZXI8dmFsdWVfbWVhbmluZy8+Cgk8L2luZm8+Cgk8aW5mbz4KCQk8Y2F0ZWdvcnk+U05GPC9jYXRlZ29yeT4KCQk8Y2F0ZWdvcnlfZGVzY3JpcHRpb24+U2tpbGxlZCBOdXJzaW5nIEZhY2lsaXR5PC9jYXRlZ29yeV9kZXNjcmlwdGlvbj4KCQk8dmFsdWU+Tm88L3ZhbHVlPgoJCTx2YWx1ZV9tZWFuaW5nPlBhdGllbnQgbm90IGluIGEgU2tpbGxlZCBOdXJzaW5nIEZhY2lsaXR5PHZhbHVlX21lYW5pbmcvPgoJPC9pbmZvPgoJPGluZm8+CgkJPGNhdGVnb3J5PkxvY2F0aW9uIDI8L2NhdGVnb3J5PgoJCTxjYXRlZ29yeV9kZXNjcmlwdGlvbj48L2NhdGVnb3J5X2Rlc2NyaXB0aW9uPgoJCTx2YWx1ZT5COTk5NjwvdmFsdWU+CgkJPHZhbHVlX21lYW5pbmc+PHZhbHVlX21lYW5pbmcvPgoJPC9pbmZvPgoJPGluZm8+CgkJPGNhdGVnb3J5PlN0YXR1czwvY2F0ZWdvcnk+CgkJPGNhdGVnb3J5X2Rlc2NyaXB0aW9uPjwvY2F0ZWdvcnlfZGVzY3JpcHRpb24+CgkJPHZhbHVlPlA8L3ZhbHVlPgoJCTx2YWx1ZV9tZWFuaW5nPlBheW1lbnQgZmxvb3I8dmFsdWVfbWVhbmluZy8+Cgk8L2luZm8+Cgk8aW5mbz4KCQk8Y2F0ZWdvcnk+TG9jYXRpb24gMzwvY2F0ZWdvcnk+CgkJPGNhdGVnb3J5X2Rlc2NyaXB0aW9uPjwvY2F0ZWdvcnlfZGVzY3JpcHRpb24+CgkJPHZhbHVlPkI5MDk5PC92YWx1ZT4KCQk8dmFsdWVfbWVhbmluZz48dmFsdWVfbWVhbmluZy8+Cgk8L2luZm8+Cgk8aW5mbz4KCQk8Y2F0ZWdvcnk+U3RhdHVzPC9jYXRlZ29yeT4KCQk8Y2F0ZWdvcnlfZGVzY3JpcHRpb24+PC9jYXRlZ29yeV9kZXNjcmlwdGlvbj4KCQk8dmFsdWU+UzwvdmFsdWU+CgkJPHZhbHVlX21lYW5pbmc+Q2xhaW1zIGF3YWl0aW5nIGEgcmVzcG9uc2UgZnJvbSBhIENXRiBob3N0IHNpdGU8dmFsdWVfbWVhbmluZy8+Cgk8L2luZm8+Cgk8aW5mbz4KCQk8Y2F0ZWdvcnk+TG9jYXRpb24gNDwvY2F0ZWdvcnk+CgkJPGNhdGVnb3J5X2Rlc2NyaXB0aW9uPjwvY2F0ZWdvcnlfZGVzY3JpcHRpb24+CgkJPHZhbHVlPkI5MDAwPC92YWx1ZT4KCQk8dmFsdWVfbWVhbmluZz48dmFsdWVfbWVhbmluZy8+Cgk8L2luZm8+Cgk8aW5mbz4KCQk8Y2F0ZWdvcnk+U3RhdHVzPC9jYXRlZ29yeT4KCQk8Y2F0ZWdvcnlfZGVzY3JpcHRpb24+PC9jYXRlZ29yeV9kZXNjcmlwdGlvbj4KCQk8dmFsdWU+UzwvdmFsdWU+CgkJPHZhbHVlX21lYW5pbmc+Q2xhaW1zIHJlYWR5IHRvIGdvIHRvIGEgY29tbW9uIHdvcmtpbmcgZmlsZSAoQ1dGKSBob3N0IHNpdGU8dmFsdWVfbWVhbmluZy8+Cgk8L2luZm8+Cgk8aW5mbz4KCQk8Y2F0ZWdvcnk+TG9jYXRpb24gNTwvY2F0ZWdvcnk+CgkJPGNhdGVnb3J5X2Rlc2NyaXB0aW9uPjwvY2F0ZWdvcnlfZGVzY3JpcHRpb24+CgkJPHZhbHVlPkIwMTAwPC92YWx1ZT4KCQk8dmFsdWVfbWVhbmluZz48dmFsdWVfbWVhbmluZy8+Cgk8L2luZm8+Cgk8aW5mbz4KCQk8Y2F0ZWdvcnk+U3RhdHVzPC9jYXRlZ29yeT4KCQk8Y2F0ZWdvcnlfZGVzY3JpcHRpb24+PC9jYXRlZ29yeV9kZXNjcmlwdGlvbj4KCQk8dmFsdWU+UzwvdmFsdWU+CgkJPHZhbHVlX21lYW5pbmc+QmVnaW5uaW5nIG9mIHRoZSBGSVNTIGJhdGNoIHByb2Nlc3M8dmFsdWVfbWVhbmluZy8+Cgk8L2luZm8+Cgk8aW5mbz4KCQk8Y2F0ZWdvcnk+TG9jYXRpb24gNjwvY2F0ZWdvcnk+CgkJPGNhdGVnb3J5X2Rlc2NyaXB0aW9uPjwvY2F0ZWdvcnlfZGVzY3JpcHRpb24+CgkJPHZhbHVlPk1TUFJBPC92YWx1ZT4KCQk8dmFsdWVfbWVhbmluZz48dmFsdWVfbWVhbmluZy8+Cgk8L2luZm8+Cgk8aW5mbz4KCQk8Y2F0ZWdvcnk+U3RhdHVzPC9jYXRlZ29yeT4KCQk8Y2F0ZWdvcnlfZGVzY3JpcHRpb24+PC9jYXRlZ29yeV9kZXNjcmlwdGlvbj4KCQk8dmFsdWU+UzwvdmFsdWU+CgkJPHZhbHVlX21lYW5pbmc+Q2xhaW0gaXMgYmVpbmcgcHJvY2Vzc2VkIHVuZGVyIE1lZGljYXJlIFNlY29uZGFyeSBQYXllciAoTVNQKSBydWxlczx2YWx1ZV9tZWFuaW5nLz4KCTwvaW5mbz4KCTxpbmZvPgoJCTxjYXRlZ29yeT5Mb2NhdGlvbiA3PC9jYXRlZ29yeT4KCQk8Y2F0ZWdvcnlfZGVzY3JpcHRpb24+PC9jYXRlZ29yeV9kZXNjcmlwdGlvbj4KCQk8dmFsdWU+QjAxMDA8L3ZhbHVlPgoJCTx2YWx1ZV9tZWFuaW5nPjx2YWx1ZV9tZWFuaW5nLz4KCTwvaW5mbz4KCTxpbmZvPgoJCTxjYXRlZ29yeT5TdGF0dXM8L2NhdGVnb3J5PgoJCTxjYXRlZ29yeV9kZXNjcmlwdGlvbj48L2NhdGVnb3J5X2Rlc2NyaXB0aW9uPgoJCTx2YWx1ZT5TPC92YWx1ZT4KCQk8dmFsdWVfbWVhbmluZz5jbGFpbSBhZGp1c3RtZW50IGhhcyBiZWVuIHN1Ym1pdHRlZCB0byBjaGFuZ2UgYSBub24tY292ZXJlZCBjbGFpbSB0byBhIGNvdmVyZWQgY2xhaW0sIGJ1dCB0aGUgYXBwcm9wcmlhdGUgY2xhaW0gY2hhbmdlIGNvbmRpdGlvbiBjb2RlIChzdWNoIGFzIEQxKSB3YXMgbm90IGJpbGxlZDx2YWx1ZV9tZWFuaW5nLz4KCTwvaW5mbz4KCTxpbmZvPgoJCTxjYXRlZ29yeT5BdHRlbmRpbmcgUGh5c2ljaWFuPC9jYXRlZ29yeT4KCQk8Y2F0ZWdvcnlfZGVzY3JpcHRpb24+PC9jYXRlZ29yeV9kZXNjcmlwdGlvbj4KCQk8dmFsdWU+RGVuaXNlIEZvc3RlcjwvdmFsdWU+CgkJPHZhbHVlX21lYW5pbmc+PHZhbHVlX21lYW5pbmcvPgoJPC9pbmZvPgoJPGluZm8+CgkJPGNhdGVnb3J5PlNwZWNpYWx0eSBDb2RlPC9jYXRlZ29yeT4KCQk8Y2F0ZWdvcnlfZGVzY3JpcHRpb24+PC9jYXRlZ29yeV9kZXNjcmlwdGlvbj4KCQk8dmFsdWU+OTc8L3ZhbHVlPgoJCTx2YWx1ZV9tZWFuaW5nPjx2YWx1ZV9tZWFuaW5nLz4KCTwvaW5mbz4KCTxpbmZvPgoJCTxjYXRlZ29yeT5UYXhvbm9teSBDb2RlPC9jYXRlZ29yeT4KCQk8Y2F0ZWdvcnlfZGVzY3JpcHRpb24+PC9jYXRlZ29yeV9kZXNjcmlwdGlvbj4KCQk8dmFsdWU+MjYxUVIxMzAwWDwvdmFsdWU+CgkJPHZhbHVlX21lYW5pbmc+PHZhbHVlX21lYW5pbmcvPgoJPC9pbmZvPgoJPGluZm8+CgkJPGNhdGVnb3J5PkRpYWdub3NpcyBDb2RlIDI8L2NhdGVnb3J5PgoJCTxjYXRlZ29yeV9kZXNjcmlwdGlvbj48L2NhdGVnb3J5X2Rlc2NyaXB0aW9uPgoJCTx2YWx1ZT5GNDE5PC92YWx1ZT4KCQk8dmFsdWVfbWVhbmluZz5BbnhpZXR5IERpc29yZGVyLCB1bnNwZWNpZmllZDx2YWx1ZV9tZWFuaW5nLz4KCTwvaW5mbz4KCTxpbmZvPgoJCTxjYXRlZ29yeT5EaWFnbm9zaXMgQ29kZSAzPC9jYXRlZ29yeT4KCQk8Y2F0ZWdvcnlfZGVzY3JpcHRpb24+PC9jYXRlZ29yeV9kZXNjcmlwdGlvbj4KCQk8dmFsdWU+RjMxOTwvdmFsdWU+CgkJPHZhbHVlX21lYW5pbmc+Qmlwb2xhciBEaXNvcmRlciwgdW5zcGVjaWZpZWQ8dmFsdWVfbWVhbmluZy8+Cgk8L2luZm8+Cgk8aW5mbz4KCQk8Y2F0ZWdvcnk+RGlhZ25vc2lzIENvZGUgNDwvY2F0ZWdvcnk+CgkJPGNhdGVnb3J5X2Rlc2NyaXB0aW9uPjwvY2F0ZWdvcnlfZGVzY3JpcHRpb24+CgkJPHZhbHVlPlo2ODI4PC92YWx1ZT4KCQk8dmFsdWVfbWVhbmluZz5Cb2R5IE1hc3MgSW5kZXggKEJNSSkgb2YgMjguMC0yOC45IGZvciBhZHVsdHM8dmFsdWVfbWVhbmluZy8+Cgk8L2luZm8+Cgk8aW5mbz4KCQk8Y2F0ZWdvcnk+RGlhZ25vc2lzIENvZGUgNTwvY2F0ZWdvcnk+CgkJPGNhdGVnb3J5X2Rlc2NyaXB0aW9uPjwvY2F0ZWdvcnlfZGVzY3JpcHRpb24+CgkJPHZhbHVlPksyMTk8L3ZhbHVlPgoJCTx2YWx1ZV9tZWFuaW5nPkdhc3Ryby1lc29waGFnZWFsIHJlZmx1eCBkaXNlYXNlIChHRVJEKSB3aXRob3V0IGVzb3BoYWdpdGlzPHZhbHVlX21lYW5pbmcvPgoJPC9pbmZvPgoJPGluZm8+CgkJPGNhdGVnb3J5PkRpYWdub3NpcyBDb2RlIDY8L2NhdGVnb3J5PgoJCTxjYXRlZ29yeV9kZXNjcmlwdGlvbj48L2NhdGVnb3J5X2Rlc2NyaXB0aW9uPgoJCTx2YWx1ZT5JMTA8L3ZhbHVlPgoJCTx2YWx1ZV9tZWFuaW5nPkVzc2VudGlhbCAocHJpbWFyeSkgaHlwZXJ0ZW5zaW9uPHZhbHVlX21lYW5pbmcvPgoJPC9pbmZvPgoJPGluZm8+CgkJPGNhdGVnb3J5PkRpYWdub3NpcyBDb2RlIDc8L2NhdGVnb3J5PgoJCTxjYXRlZ29yeV9kZXNjcmlwdGlvbj48L2NhdGVnb3J5X2Rlc2NyaXB0aW9uPgoJCTx2YWx1ZT5GNDMxMDwvdmFsdWU+CgkJPHZhbHVlX21lYW5pbmc+UG9zdC1UcmF1bWF0aWMgU3RyZXNzIERpc29yZGVyIChQVFNEKSwgdW5zcGVjaWZpZWQ8dmFsdWVfbWVhbmluZy8+Cgk8L2luZm8+Cgk8aW5mbz4KCQk8Y2F0ZWdvcnk+RGlhZ25vc2lzIENvZGUgODwvY2F0ZWdvcnk+CgkJPGNhdGVnb3J5X2Rlc2NyaXB0aW9uPjwvY2F0ZWdvcnlfZGVzY3JpcHRpb24+CgkJPHZhbHVlPkUxMTY1PC92YWx1ZT4KCQk8dmFsdWVfbWVhbmluZz5UeXBlIDIgZGlhYmV0ZXMgbWVsbGl0dXMgd2l0aCBoeXBlcmdseWNlbWlhPHZhbHVlX21lYW5pbmcvPgoJPC9pbmZvPgoJPGluZm8+CgkJPGNhdGVnb3J5PkgyNjYzPC9jYXRlZ29yeT4KCQk8Y2F0ZWdvcnlfZGVzY3JpcHRpb24+Q09WRU5UUlkgSEVBTFRIIENBUkUgT0YgTUlTU09VUkksIElOQy48L2NhdGVnb3J5X2Rlc2NyaXB0aW9uPgoJCTx2YWx1ZT4xMjg1IEZlcm5yaWRnZSBQYXJrd2F5LCBTdWl0ZSAyMDAgU3QuIExvdWlzIE1PIDYzMTQxPC92YWx1ZT4KCQk8dmFsdWVfbWVhbmluZz4xLTgwMC01MzMtMDM2Nzx2YWx1ZV9tZWFuaW5nLz4KCTwvaW5mbz4KPC9DbGFpbUluZm8+",
    "sequence": "I",
    "claimData":"PENsYWltSW5mbz4KICA8aW5mbz4KICAgIDxjYXRlZ29yeT5OUEk8L2NhdGVnb3J5PgogICAgPGNhdGVnb3J5X2Rlc2NyaXB0aW9uPk5hdGlvbmFsIFByb3ZpZGVyIElkZW50aWZpZXI8L2NhdGVnb3J5X2Rlc2NyaXB0aW9uPgogICAgPHZhbHVlPjE1ODEzNDQ4OTk8L3ZhbHVlPgogICAgPHZhbHVlX21lYW5pbmc+PC92YWx1ZV9tZWFuaW5nPgogIDwvaW5mbz4KICA8aW5mbz4KICAgIDxjYXRlZ29yeT5QVEFOPC9jYXRlZ29yeT4KICAgIDxjYXRlZ29yeV9kZXNjcmlwdGlvbj5Qcm92aWRlciBUcmFuc2FjdGlvbiBBY2Nlc3MgTnVtYmVyPC9jYXRlZ29yeV9kZXNjcmlwdGlvbj4KICAgIDx2YWx1ZT5aNTE4NDk4PC92YWx1ZT4KICAgIDx2YWx1ZV9tZWFuaW5nPjwvdmFsdWVfbWVhbmluZz4KICA8L2luZm8+CiAgPGluZm8+CiAgICA8Y2F0ZWdvcnk+VGF4IElEPC9jYXRlZ29yeT4KICAgIDxjYXRlZ29yeV9kZXNjcmlwdGlvbj5UYXggSUQ8L2NhdGVnb3J5X2Rlc2NyaXB0aW9uPgogICAgPHZhbHVlPjU2MTAwPC92YWx1ZT4KICAgIDx2YWx1ZV9tZWFuaW5nPjwvdmFsdWVfbWVhbmluZz4KICA8L2luZm8+CiAgPGluZm8+CiAgICA8Y2F0ZWdvcnk+TUJJPC9jYXRlZ29yeT4KICAgIDxjYXRlZ29yeV9kZXNjcmlwdGlvbj5NZWRpY2FyZSBCZW5lZmljaWFyeSBJZGVudGlmaWVyPC9jYXRlZ29yeV9kZXNjcmlwdGlvbj4KICAgIDx2YWx1ZT5aRFU5U0wzSVNRMDwvdmFsdWU+CiAgICA8dmFsdWVfbWVhbmluZz48L3ZhbHVlX21lYW5pbmc+CiAgPC9pbmZvPgogIDxpbmZvPgogICAgPGNhdGVnb3J5PkJlbmVmaWNpYXJ5IE5hbWU8L2NhdGVnb3J5PgogICAgPGNhdGVnb3J5X2Rlc2NyaXB0aW9uPjwvY2F0ZWdvcnlfZGVzY3JpcHRpb24+CiAgICA8dmFsdWU+SmFuZSBTbWl0aDwvdmFsdWU+CiAgICA8dmFsdWVfbWVhbmluZz48L3ZhbHVlX21lYW5pbmc+CiAgPC9pbmZvPgogIDxpbmZvPgogICAgPGNhdGVnb3J5PkRPQjwvY2F0ZWdvcnk+CiAgICA8Y2F0ZWdvcnlfZGVzY3JpcHRpb24+RGF0ZSBvZiBCaXJ0aDwvY2F0ZWdvcnlfZGVzY3JpcHRpb24+CiAgICA8dmFsdWU+MS8xNS8xOTYwPC92YWx1ZT4KICAgIDx2YWx1ZV9tZWFuaW5nPjwvdmFsdWVfbWVhbmluZz4KICA8L2luZm8+CiAgPGluZm8+CiAgICA8Y2F0ZWdvcnk+RE9TPC9jYXRlZ29yeT4KICAgIDxjYXRlZ29yeV9kZXNjcmlwdGlvbj5EYXRlIG9mIFNlcnZpY2U8L2NhdGVnb3J5X2Rlc2NyaXB0aW9uPgogICAgPHZhbHVlPjkvNS8yMDI0PC92YWx1ZT4KICAgIDx2YWx1ZV9tZWFuaW5nPjwvdmFsdWVfbWVhbmluZz4KICA8L2luZm8+CiAgPGluZm8+CiAgICA8Y2F0ZWdvcnk+UmVjZWlwdCBEYXRlPC9jYXRlZ29yeT4KICAgIDxjYXRlZ29yeV9kZXNjcmlwdGlvbj48L2NhdGVnb3J5X2Rlc2NyaXB0aW9uPgogICAgPHZhbHVlPjEvMTAvMjAyNTwvdmFsdWU+CiAgICA8dmFsdWVfbWVhbmluZz48L3ZhbHVlX21lYW5pbmc+CiAgPC9pbmZvPgogIDxpbmZvPgogICAgPGNhdGVnb3J5PkJlbmVmaWNpYXJ5IExpYWJsZSBJbmRpY2F0b3I8L2NhdGVnb3J5PgogICAgPGNhdGVnb3J5X2Rlc2NyaXB0aW9uPjwvY2F0ZWdvcnlfZGVzY3JpcHRpb24+CiAgICA8dmFsdWU+TjwvdmFsdWU+CiAgICA8dmFsdWVfbWVhbmluZz48L3ZhbHVlX21lYW5pbmc+CiAgPC9pbmZvPgogIDxpbmZvPgogICAgPGNhdGVnb3J5PkFOU0kgUmVhc29uIENvZGVzPC9jYXRlZ29yeT4KICAgIDxjYXRlZ29yeV9kZXNjcmlwdGlvbj5BbWVyaWNhbiBOYXRpb25hbCBTdGFuZGFyZHMgSW5zdGl0dXRlIFJlYXNvbiBDb2RlczwvY2F0ZWdvcnlfZGVzY3JpcHRpb24+CiAgICA8dmFsdWU+TUEwMTwvdmFsdWU+CiAgICA8dmFsdWVfbWVhbmluZz5BTEVSVDogSUYgWU9VIERPIE5PVCBBR1JFRSBXSVRIIFdIQVQgV0UgQVBQUk9WRUQgRk9SIFRIRVNFIFNFUlZJQ0VTICBZT1UgTUFZIEFQUEVBTCBPVVIgREVDSVNJT04uICBUTyBNQUtFIFNVUkUgVEhBVCBXRSBBUkUgRkFJUiBUTyBZT1UgIFdFIFJFUVVJUkUgQU5PVEhFUiBJTkRJVklEVUFMIFRIQVQgRElEIE5PVCBQUk9DRVNTIFlPVVIgSU5JVElBTCBDTEFJTSBUTyBDT05EVUNUIFRIRSBBUFBFQUwuICBIT1dFVkVSICBJTiBPUkRFUiBUTyBCRSBFTElHSUJMRSBGT1IgQU4gQVBQRUFMICBZT1UgTVVTVCBXUklURSBUTyBVUyBXSVRISU4gMTIwIERBWVMgT0YgVEhFIERBVEUgWU9VIFJFQ0VJVkVEIFRISVMgTk9USUNFPC92YWx1ZV9tZWFuaW5nPgogIDwvaW5mbz4KICA8aW5mbz4KICAgIDxjYXRlZ29yeT5BTlNJIFJlbWFyayBDb2RlPC9jYXRlZ29yeT4KICAgIDxjYXRlZ29yeV9kZXNjcmlwdGlvbj5BbWVyaWNhbiBOYXRpb25hbCBTdGFuZGFyZHMgSW5zdGl0dXRlIFJlbWFyayBDb2RlczwvY2F0ZWdvcnlfZGVzY3JpcHRpb24+CiAgICA8dmFsdWU+TjQzNTwvdmFsdWU+CiAgICA8dmFsdWVfbWVhbmluZz48L3ZhbHVlX21lYW5pbmc+CiAgPC9pbmZvPgogIDxpbmZvPgogICAgPGNhdGVnb3J5PkF0dGVuZGluZyBQaHlzaWNpYW48L2NhdGVnb3J5PgogICAgPGNhdGVnb3J5X2Rlc2NyaXB0aW9uPjwvY2F0ZWdvcnlfZGVzY3JpcHRpb24+CiAgICA8dmFsdWU+RGVuaXNlIEZvc3RlcjwvdmFsdWU+CiAgICA8dmFsdWVfbWVhbmluZz48L3ZhbHVlX21lYW5pbmc+CiAgPC9pbmZvPgogIDxpbmZvPgogICAgPGNhdGVnb3J5PlNwZWNpYWx0eSBDb2RlPC9jYXRlZ29yeT4KICAgIDxjYXRlZ29yeV9kZXNjcmlwdGlvbj48L2NhdGVnb3J5X2Rlc2NyaXB0aW9uPgogICAgPHZhbHVlPjk3PC92YWx1ZT4KICAgIDx2YWx1ZV9tZWFuaW5nPjwvdmFsdWVfbWVhbmluZz4KICA8L2luZm8+CiAgPGluZm8+CiAgICA8Y2F0ZWdvcnk+TG9jYXRpb24gMTwvY2F0ZWdvcnk+CiAgICA8Y2F0ZWdvcnlfZGVzY3JpcHRpb24+PC9jYXRlZ29yeV9kZXNjcmlwdGlvbj4KICAgIDx2YWx1ZT5COTk5NzwvdmFsdWU+CiAgICA8dmFsdWVfbWVhbmluZz48L3ZhbHVlX21lYW5pbmc+CiAgPC9pbmZvPgogIDxpbmZvPgogICAgPGNhdGVnb3J5PlN0YXR1czwvY2F0ZWdvcnk+CiAgICA8Y2F0ZWdvcnlfZGVzY3JpcHRpb24+PC9jYXRlZ29yeV9kZXNjcmlwdGlvbj4KICAgIDx2YWx1ZT5SPC92YWx1ZT4KICAgIDx2YWx1ZV9tZWFuaW5nPlByb2Nlc3NpbmcgQ2xhaW0gUmVqZWN0aW9uPC92YWx1ZV9tZWFuaW5nPgogIDwvaW5mbz4KICA8aW5mbz4KICAgIDxjYXRlZ29yeT5Mb2NhdGlvbiAyPC9jYXRlZ29yeT4KICAgIDxjYXRlZ29yeV9kZXNjcmlwdGlvbj48L2NhdGVnb3J5X2Rlc2NyaXB0aW9uPgogICAgPHZhbHVlPkI5MDk5PC92YWx1ZT4KICAgIDx2YWx1ZV9tZWFuaW5nPjwvdmFsdWVfbWVhbmluZz4KICA8L2luZm8+CiAgPGluZm8+CiAgICA8Y2F0ZWdvcnk+U3RhdHVzPC9jYXRlZ29yeT4KICAgIDxjYXRlZ29yeV9kZXNjcmlwdGlvbj48L2NhdGVnb3J5X2Rlc2NyaXB0aW9uPgogICAgPHZhbHVlPlM8L3ZhbHVlPgogICAgPHZhbHVlX21lYW5pbmc+Q2xhaW1zIGF3YWl0aW5nIGEgcmVzcG9uc2UgZnJvbSBhIENXRiBob3N0IHNpdGU8L3ZhbHVlX21lYW5pbmc+CiAgPC9pbmZvPgogIDxpbmZvPgogICAgPGNhdGVnb3J5PkxvY2F0aW9uIDM8L2NhdGVnb3J5PgogICAgPGNhdGVnb3J5X2Rlc2NyaXB0aW9uPjwvY2F0ZWdvcnlfZGVzY3JpcHRpb24+CiAgICA8dmFsdWU+QjkwMDA8L3ZhbHVlPgogICAgPHZhbHVlX21lYW5pbmc+PC92YWx1ZV9tZWFuaW5nPgogIDwvaW5mbz4KICA8aW5mbz4KICAgIDxjYXRlZ29yeT5TdGF0dXM8L2NhdGVnb3J5PgogICAgPGNhdGVnb3J5X2Rlc2NyaXB0aW9uPjwvY2F0ZWdvcnlfZGVzY3JpcHRpb24+CiAgICA8dmFsdWU+UzwvdmFsdWU+CiAgICA8dmFsdWVfbWVhbmluZz5DbGFpbXMgcmVhZHkgdG8gZ28gdG8gYSBjb21tb24gd29ya2luZyBmaWxlIChDV0YpIGhvc3Qgc2l0ZTwvdmFsdWVfbWVhbmluZz4KICA8L2luZm8+CiAgPGluZm8+CiAgICA8Y2F0ZWdvcnk+TG9jYXRpb24gNDwvY2F0ZWdvcnk+CiAgICA8Y2F0ZWdvcnlfZGVzY3JpcHRpb24+PC9jYXRlZ29yeV9kZXNjcmlwdGlvbj4KICAgIDx2YWx1ZT5CMDEwMDwvdmFsdWU+CiAgICA8dmFsdWVfbWVhbmluZz48L3ZhbHVlX21lYW5pbmc+CiAgPC9pbmZvPgogIDxpbmZvPgogICAgPGNhdGVnb3J5PlN0YXR1czwvY2F0ZWdvcnk+CiAgICA8Y2F0ZWdvcnlfZGVzY3JpcHRpb24+PC9jYXRlZ29yeV9kZXNjcmlwdGlvbj4KICAgIDx2YWx1ZT5TPC92YWx1ZT4KICAgIDx2YWx1ZV9tZWFuaW5nPkJlZ2lubmluZyBvZiB0aGUgRklTUyBiYXRjaCBwcm9jZXNzPC92YWx1ZV9tZWFuaW5nPgogIDwvaW5mbz4KICA8aW5mbz4KICAgIDxjYXRlZ29yeT5EZW5pYWwgTGV0dGVyIENvZGVzPC9jYXRlZ29yeT4KICAgIDxjYXRlZ29yeV9kZXNjcmlwdGlvbj48L2NhdGVnb3J5X2Rlc2NyaXB0aW9uPgogICAgPHZhbHVlPjM5OTI5PC92YWx1ZT4KICAgIDx2YWx1ZV9tZWFuaW5nPjwvdmFsdWVfbWVhbmluZz4KICA8L2luZm8+CiAgPGluZm8+CiAgICA8Y2F0ZWdvcnk+QmlsbCBUeXBlPC9jYXRlZ29yeT4KICAgIDxjYXRlZ29yeV9kZXNjcmlwdGlvbj48L2NhdGVnb3J5X2Rlc2NyaXB0aW9uPgogICAgPHZhbHVlPjcxMDwvdmFsdWU+CiAgICA8dmFsdWVfbWVhbmluZz48L3ZhbHVlX21lYW5pbmc+CiAgPC9pbmZvPgogIDxpbmZvPgogICAgPGNhdGVnb3J5PlRvdGFsIEJpbGxlZCBVbml0czwvY2F0ZWdvcnk+CiAgICA8Y2F0ZWdvcnlfZGVzY3JpcHRpb24+PC9jYXRlZ29yeV9kZXNjcmlwdGlvbj4KICAgIDx2YWx1ZT4xPC92YWx1ZT4KICAgIDx2YWx1ZV9tZWFuaW5nPjwvdmFsdWVfbWVhbmluZz4KICA8L2luZm8+CiAgPGluZm8+CiAgICA8Y2F0ZWdvcnk+U3VibWl0dGVkIENoYXJnZXM8L2NhdGVnb3J5PgogICAgPGNhdGVnb3J5X2Rlc2NyaXB0aW9uPjwvY2F0ZWdvcnlfZGVzY3JpcHRpb24+CiAgICA8dmFsdWU+MjQ4PC92YWx1ZT4KICAgIDx2YWx1ZV9tZWFuaW5nPjwvdmFsdWVfbWVhbmluZz4KICA8L2luZm8+CiAgPGluZm8+CiAgICA8Y2F0ZWdvcnk+QWxsb3dlZCBDaGFyZ2VzPC9jYXRlZ29yeT4KICAgIDxjYXRlZ29yeV9kZXNjcmlwdGlvbj48L2NhdGVnb3J5X2Rlc2NyaXB0aW9uPgogICAgPHZhbHVlPjA8L3ZhbHVlPgogICAgPHZhbHVlX21lYW5pbmc+PC92YWx1ZV9tZWFuaW5nPgogIDwvaW5mbz4KICA8aW5mbz4KICAgIDxjYXRlZ29yeT5Ob24tQ292ZXJlZCBDaGFyZ2VzPC9jYXRlZ29yeT4KICAgIDxjYXRlZ29yeV9kZXNjcmlwdGlvbj48L2NhdGVnb3J5X2Rlc2NyaXB0aW9uPgogICAgPHZhbHVlPjI0ODwvdmFsdWU+CiAgICA8dmFsdWVfbWVhbmluZz48L3ZhbHVlX21lYW5pbmc+CiAgPC9pbmZvPgogIDxpbmZvPgogICAgPGNhdGVnb3J5PkRDTjwvY2F0ZWdvcnk+CiAgICA8Y2F0ZWdvcnlfZGVzY3JpcHRpb24+RG9jdW1lbnQgQ29udHJvbCBOdW1iZXI8L2NhdGVnb3J5X2Rlc2NyaXB0aW9uPgogICAgPHZhbHVlPjIyNTg1NDQ0MjE4N01PQTwvdmFsdWU+CiAgICA8dmFsdWVfbWVhbmluZz48L3ZhbHVlX21lYW5pbmc+CiAgPC9pbmZvPgogIDxpbmZvPgogICAgPGNhdGVnb3J5PkNhbmNlbCBEYXRlPC9jYXRlZ29yeT4KICAgIDxjYXRlZ29yeV9kZXNjcmlwdGlvbj48L2NhdGVnb3J5X2Rlc2NyaXB0aW9uPgogICAgPHZhbHVlPjEvMjIvMjAyNTwvdmFsdWU+CiAgICA8dmFsdWVfbWVhbmluZz48L3ZhbHVlX21lYW5pbmc+CiAgPC9pbmZvPgogIDxpbmZvPgogICAgPGNhdGVnb3J5PkNhcnJpZXIgQ29kZTwvY2F0ZWdvcnk+CiAgICA8Y2F0ZWdvcnlfZGVzY3JpcHRpb24+PC9jYXRlZ29yeV9kZXNjcmlwdGlvbj4KICAgIDx2YWx1ZT41MzAyPC92YWx1ZT4KICAgIDx2YWx1ZV9tZWFuaW5nPjwvdmFsdWVfbWVhbmluZz4KICA8L2luZm8+CiAgPGluZm8+CiAgICA8Y2F0ZWdvcnk+Q2hlY2sgTnVtYmVyPC9jYXRlZ29yeT4KICAgIDxjYXRlZ29yeV9kZXNjcmlwdGlvbj48L2NhdGVnb3J5X2Rlc2NyaXB0aW9uPgogICAgPHZhbHVlPkVGVDY5NzY1NTU8L3ZhbHVlPgogICAgPHZhbHVlX21lYW5pbmc+PC92YWx1ZV9tZWFuaW5nPgogIDwvaW5mbz4KICA8aW5mbz4KICAgIDxjYXRlZ29yeT5DbGFpbSBMb2NhdGlvbjwvY2F0ZWdvcnk+CiAgICA8Y2F0ZWdvcnlfZGVzY3JpcHRpb24+PC9jYXRlZ29yeV9kZXNjcmlwdGlvbj4KICAgIDx2YWx1ZT5COTk5NzwvdmFsdWU+CiAgICA8dmFsdWVfbWVhbmluZz48L3ZhbHVlX21lYW5pbmc+CiAgPC9pbmZvPgogIDxpbmZvPgogICAgPGNhdGVnb3J5PlN0YXR1czwvY2F0ZWdvcnk+CiAgICA8Y2F0ZWdvcnlfZGVzY3JpcHRpb24+PC9jYXRlZ29yeV9kZXNjcmlwdGlvbj4KICAgIDx2YWx1ZT5SPC92YWx1ZT4KICAgIDx2YWx1ZV9tZWFuaW5nPlByb2Nlc3NpbmcgQ2xhaW0gUmVqZWN0aW9uPC92YWx1ZV9tZWFuaW5nPgogIDwvaW5mbz4KICA8aW5mbz4KICAgIDxjYXRlZ29yeT5EaWFnbm9zaXMgQ29kZSAxPC9jYXRlZ29yeT4KICAgIDxjYXRlZ29yeV9kZXNjcmlwdGlvbj48L2NhdGVnb3J5X2Rlc2NyaXB0aW9uPgogICAgPHZhbHVlPkY5MDk8L3ZhbHVlPgogICAgPHZhbHVlX21lYW5pbmc+YXR0ZW50aW9uLWRlZmljaXQgaHlwZXJhY3Rpdml0eSAoYWRvbGVzY2VudCkgKGFkdWx0KSAoY2hpbGQpPC92YWx1ZV9tZWFuaW5nPgogIDwvaW5mbz4KICA8aW5mbz4KICAgIDxjYXRlZ29yeT5EaWFnbm9zaXMgQ29kZSAyPC9jYXRlZ29yeT4KICAgIDxjYXRlZ29yeV9kZXNjcmlwdGlvbj48L2NhdGVnb3J5X2Rlc2NyaXB0aW9uPgogICAgPHZhbHVlPkY0MTk8L3ZhbHVlPgogICAgPHZhbHVlX21lYW5pbmc+QW54aWV0eSBEaXNvcmRlciAgdW5zcGVjaWZpZWQ8L3ZhbHVlX21lYW5pbmc+CiAgPC9pbmZvPgogIDxpbmZvPgogICAgPGNhdGVnb3J5PkRpYWdub3NpcyBDb2RlIDM8L2NhdGVnb3J5PgogICAgPGNhdGVnb3J5X2Rlc2NyaXB0aW9uPjwvY2F0ZWdvcnlfZGVzY3JpcHRpb24+CiAgICA8dmFsdWU+RjMxOTwvdmFsdWU+CiAgICA8dmFsdWVfbWVhbmluZz5CaXBvbGFyIERpc29yZGVyICB1bnNwZWNpZmllZDwvdmFsdWVfbWVhbmluZz4KICA8L2luZm8+CiAgPGluZm8+CiAgICA8Y2F0ZWdvcnk+RGlhZ25vc2lzIENvZGUgNDwvY2F0ZWdvcnk+CiAgICA8Y2F0ZWdvcnlfZGVzY3JpcHRpb24+PC9jYXRlZ29yeV9kZXNjcmlwdGlvbj4KICAgIDx2YWx1ZT5aNjgyODwvdmFsdWU+CiAgICA8dmFsdWVfbWVhbmluZz5Cb2R5IE1hc3MgSW5kZXggKEJNSSkgb2YgMjguMC0yOC45IGZvciBhZHVsdHM8L3ZhbHVlX21lYW5pbmc+CiAgPC9pbmZvPgogIDxpbmZvPgogICAgPGNhdGVnb3J5PkRpYWdub3NpcyBDb2RlIDU8L2NhdGVnb3J5PgogICAgPGNhdGVnb3J5X2Rlc2NyaXB0aW9uPjwvY2F0ZWdvcnlfZGVzY3JpcHRpb24+CiAgICA8dmFsdWU+SzIxOTwvdmFsdWU+CiAgICA8dmFsdWVfbWVhbmluZz5HYXN0cm8tZXNvcGhhZ2VhbCByZWZsdXggZGlzZWFzZSAoR0VSRCkgd2l0aG91dCBlc29waGFnaXRpczwvdmFsdWVfbWVhbmluZz4KICA8L2luZm8+CiAgPGluZm8+CiAgICA8Y2F0ZWdvcnk+RGlhZ25vc2lzIENvZGUgNjwvY2F0ZWdvcnk+CiAgICA8Y2F0ZWdvcnlfZGVzY3JpcHRpb24+PC9jYXRlZ29yeV9kZXNjcmlwdGlvbj4KICAgIDx2YWx1ZT5JMTA8L3ZhbHVlPgogICAgPHZhbHVlX21lYW5pbmc+RXNzZW50aWFsIChwcmltYXJ5KSBoeXBlcnRlbnNpb248L3ZhbHVlX21lYW5pbmc+CiAgPC9pbmZvPgogIDxpbmZvPgogICAgPGNhdGVnb3J5PkRpYWdub3NpcyBDb2RlIDc8L2NhdGVnb3J5PgogICAgPGNhdGVnb3J5X2Rlc2NyaXB0aW9uPjwvY2F0ZWdvcnlfZGVzY3JpcHRpb24+CiAgICA8dmFsdWU+RjQzMTA8L3ZhbHVlPgogICAgPHZhbHVlX21lYW5pbmc+UG9zdC1UcmF1bWF0aWMgU3RyZXNzIERpc29yZGVyIChQVFNEKSAgdW5zcGVjaWZpZWQ8L3ZhbHVlX21lYW5pbmc+CiAgPC9pbmZvPgogIDxpbmZvPgogICAgPGNhdGVnb3J5PkRpYWdub3NpcyBDb2RlIDg8L2NhdGVnb3J5PgogICAgPGNhdGVnb3J5X2Rlc2NyaXB0aW9uPjwvY2F0ZWdvcnlfZGVzY3JpcHRpb24+CiAgICA8dmFsdWU+RTExNjU8L3ZhbHVlPgogICAgPHZhbHVlX21lYW5pbmc+VHlwZSAyIGRpYWJldGVzIG1lbGxpdHVzIHdpdGggaHlwZXJnbHljZW1pYTwvdmFsdWVfbWVhbmluZz4KICA8L2luZm8+CiAgPGluZm8+CiAgICA8Y2F0ZWdvcnk+Q2xhaW0gUmVhc29uIENvZGU8L2NhdGVnb3J5PgogICAgPGNhdGVnb3J5X2Rlc2NyaXB0aW9uPjwvY2F0ZWdvcnlfZGVzY3JpcHRpb24+CiAgICA8dmFsdWU+Mzk5Mjk8L3ZhbHVlPgogICAgPHZhbHVlX21lYW5pbmc+VEhJUyBJUyBBIENMQUlNIExFVkVMIFJFQVNPTiBDT0RFIEZPUiBDTEFJTVMgVEhBVCBIQVZFIEFMTCBMSU5FIElURU1TIFJFSkVDVEVEIEFORC9PUiBSRUpFQ1RFRCBBTkQgREVOSUVELiAqIENIRUNLIExJTkUgTEVWRUwgVE8gREVURVJNSU5FIFdIWSBMSU5FUyBXRVJFIERFTklFRCBBTkQgV0hPIElTIExJQUJMRS48L3ZhbHVlX21lYW5pbmc+CiAgPC9pbmZvPgogIDxpbmZvPgogICAgPGNhdGVnb3J5PkF0dGVuZGluZyBQaHlzaWNpYW48L2NhdGVnb3J5PgogICAgPGNhdGVnb3J5X2Rlc2NyaXB0aW9uPjwvY2F0ZWdvcnlfZGVzY3JpcHRpb24+CiAgICA8dmFsdWU+RGVuaXNlIEZvc3RlcjwvdmFsdWU+CiAgICA8dmFsdWVfbWVhbmluZz48L3ZhbHVlX21lYW5pbmc+CiAgPC9pbmZvPgogIDxpbmZvPgogICAgPGNhdGVnb3J5PlRheG9ub215IENvZGU8L2NhdGVnb3J5PgogICAgPGNhdGVnb3J5X2Rlc2NyaXB0aW9uPjwvY2F0ZWdvcnlfZGVzY3JpcHRpb24+CiAgICA8dmFsdWU+MjYxUVIxMzAwWDwvdmFsdWU+CiAgICA8dmFsdWVfbWVhbmluZz48L3ZhbHVlX21lYW5pbmc+CiAgPC9pbmZvPgo8L0NsYWltSW5mbz4=",
    "voiceFlag": "Y"
}
```

### WPS Medicare OpenAI request after going through configuration

```json
{
    "messages": [
        {
            "role": "user",
            "content": "You are a Medicare Customer Service Representative for WPS Health Solutions. "
        },
        {
            "role": "user",
            "content": "Here are the details of Medicare Claim Status:<ClaimInfo>, <info>, <category>NPI</category>, <category_description>National Provider Identifier</category_description>, <value>1581344899</value>, <value_meaning></value_meaning>, </info>, <info>, <category>PTAN</category>, <category_description>Provider Transaction Access Number</category_description>, <value>Z518498</value>, <value_meaning></value_meaning>, </info>, <info>, <category>Tax ID</category>, <category_description>Tax ID</category_description>, <value>56100</value>, <value_meaning></value_meaning>, </info>, <info>, <category>MBI</category>, <category_description>Medicare Beneficiary Identifier</category_description>, <value>ZDU9SL3ISQ0</value>, <value_meaning></value_meaning>, </info>, <info>, <category>Beneficiary Name</category>, <category_description></category_description>, <value>Jane Smith</value>, <value_meaning></value_meaning>, </info>, <info>, <category>DOB</category>, <category_description>Date of Birth</category_description>, <value>1/15/1960</value>, <value_meaning></value_meaning>, </info>, <info>, <category>DOS</category>, <category_description>Date of Service</category_description>, <value>9/5/2024</value>, <value_meaning></value_meaning>, </info>, <info>, <category>Receipt Date</category>, <category_description></category_description>, <value>1/10/2025</value>, <value_meaning></value_meaning>, </info>, <info>, <category>Beneficiary Liable Indicator</category>, <category_description></category_description>, <value>N</value>, <value_meaning></value_meaning>, </info>, <info>, <category>ANSI Reason Codes</category>, <category_description>American National Standards Institute Reason Codes</category_description>, <value>MA01</value>, <value_meaning>ALERT: IF YOU DO NOT AGREE WITH WHAT WE APPROVED FOR THESE SERVICES YOU MAY APPEAL OUR DECISION. TO MAKE SURE THAT WE ARE FAIR TO YOU WE REQUIRE ANOTHER INDIVIDUAL THAT DID NOT PROCESS YOUR INITIAL CLAIM TO CONDUCT THE APPEAL. HOWEVER IN ORDER TO BE ELIGIBLE FOR AN APPEAL YOU MUST WRITE TO US WITHIN 120 DAYS OF THE DATE YOU RECEIVED THIS NOTICE</value_meaning>, </info>, <info>, <category>ANSI Remark Code</category>, <category_description>American National Standards Institute Remark Codes</category_description>, <value>N435</value>, <value_meaning></value_meaning>, </info>, <info>, <category>Attending Physician</category>, <category_description></category_description>, <value>Denise Foster</value>, <value_meaning></value_meaning>, </info>, <info>, <category>Specialty Code</category>, <category_description></category_description>, <value>97</value>, <value_meaning></value_meaning>, </info>, <info>, <category>Location 1</category>, <category_description></category_description>, <value>B9997</value>, <value_meaning></value_meaning>, </info>, <info>, <category>Status</category>, <category_description></category_description>, <value>R</value>, <value_meaning>Processing Claim Rejection</value_meaning>, </info>, <info>, <category>Location 2</category>, <category_description></category_description>, <value>B9099</value>, <value_meaning></value_meaning>, </info>, <info>, <category>Status</category>, <category_description></category_description>, <value>S</value>, <value_meaning>Claims awaiting a response from a CWF host site</value_meaning>, </info>, <info>, <category>Location 3</category>, <category_description></category_description>, <value>B9000</value>, <value_meaning></value_meaning>, </info>, <info>, <category>Status</category>, <category_description></category_description>, <value>S</value>, <value_meaning>Claims ready to go to a common working file (CWF) host site</value_meaning>, </info>, <info>, <category>Location 4</category>, <category_description></category_description>, <value>B0100</value>, <value_meaning></value_meaning>, </info>, <info>, <category>Status</category>, <category_description></category_description>, <value>S</value>, <value_meaning>Beginning of the FISS batch process</value_meaning>, </info>, <info>, <category>Denial Letter Codes</category>, <category_description></category_description>, <value>39929</value>, <value_meaning></value_meaning>, </info>, <info>, <category>Bill Type</category>, <category_description></category_description>, <value>710</value>, <value_meaning></value_meaning>, </info>, <info>, <category>Total Billed Units</category>, <category_description></category_description>, <value>1</value>, <value_meaning></value_meaning>, </info>, <info>, <category>Submitted Charges</category>, <category_description></category_description>, <value>248</value>, <value_meaning></value_meaning>, </info>, <info>, <category>Allowed Charges</category>, <category_description></category_description>, <value>0</value>, <value_meaning></value_meaning>, </info>, <info>, <category>Non-Covered Charges</category>, <category_description></category_description>, <value>248</value>, <value_meaning></value_meaning>, </info>, <info>, <category>DCN</category>, <category_description>Document Control Number</category_description>, <value>225854442187MOA</value>, <value_meaning></value_meaning>, </info>, <info>, <category>Cancel Date</category>, <category_description></category_description>, <value>1/22/2025</value>, <value_meaning></value_meaning>, </info>, <info>, <category>Carrier Code</category>, <category_description></category_description>, <value>5302</value>, <value_meaning></value_meaning>, </info>, <info>, <category>Check Number</category>, <category_description></category_description>, <value>EFT6976555</value>, <value_meaning></value_meaning>, </info>, <info>, <category>Claim Location</category>, <category_description></category_description>, <value>B9997</value>, <value_meaning></value_meaning>, </info>, <info>, <category>Status</category>, <category_description></category_description>, <value>R</value>, <value_meaning>Processing Claim Rejection</value_meaning>, </info>, <info>, <category>Diagnosis Code 1</category>, <category_description></category_description>, <value>F909</value>, <value_meaning>attention-deficit hyperactivity (adolescent) (adult) (child)</value_meaning>, </info>, <info>, <category>Diagnosis Code 2</category>, <category_description></category_description>, <value>F419</value>, <value_meaning>Anxiety Disorder unspecified</value_meaning>, </info>, <info>, <category>Diagnosis Code 3</category>, <category_description></category_description>, <value>F319</value>, <value_meaning>Bipolar Disorder unspecified</value_meaning>, </info>, <info>, <category>Diagnosis Code 4</category>, <category_description></category_description>, <value>Z6828</value>, <value_meaning>Body Mass Index (BMI) of 28.0-28.9 for adults</value_meaning>, </info>, <info>, <category>Diagnosis Code 5</category>, <category_description></category_description>, <value>K219</value>, <value_meaning>Gastro-esophageal reflux disease (GERD) without esophagitis</value_meaning>, </info>, <info>, <category>Diagnosis Code 6</category>, <category_description></category_description>, <value>I10</value>, <value_meaning>Essential (primary) hypertension</value_meaning>, </info>, <info>, <category>Diagnosis Code 7</category>, <category_description></category_description>, <value>F4310</value>, <value_meaning>Post-Traumatic Stress Disorder (PTSD) unspecified</value_meaning>, </info>, <info>, <category>Diagnosis Code 8</category>, <category_description></category_description>, <value>E1165</value>, <value_meaning>Type 2 diabetes mellitus with hyperglycemia</value_meaning>, </info>, <info>, <category>Claim Reason Code</category>, <category_description></category_description>, <value>39929</value>, <value_meaning>THIS IS A CLAIM LEVEL REASON CODE FOR CLAIMS THAT HAVE ALL LINE ITEMS REJECTED AND/OR REJECTED AND DENIED. * CHECK LINE LEVEL TO DETERMINE WHY LINES WERE DENIED AND WHO IS LIABLE.</value_meaning>, </info>, <info>, <category>Attending Physician</category>, <category_description></category_description>, <value>Denise Foster</value>, <value_meaning></value_meaning>, </info>, <info>, <category>Taxonomy Code</category>, <category_description></category_description>, <value>261QR1300X</value>, <value_meaning></value_meaning>, </info>,</ClaimInfo>"
        },
        {
            "role": "user",
            "content": "Here are the additional reference information of the Medicare Claim data mentioned above:<ClaimInfo>, <info>, <category>Claim Reason Code</category>, <category_description></category_description>, <value>37205</value>, <value_meaning>a previously processed bill has been adjusted<value_meaning/>, </info>, <info>, <category>Subject to Part B Deductible</category>, <category_description></category_description>, <value>72.9</value>, <value_meaning><value_meaning/>, </info>, <info>, <category>Total Billed Units</category>, <category_description></category_description>, <value>1</value>, <value_meaning><value_meaning/>, </info>, <info>, <category>Cancel Date</category>, <category_description></category_description>, <value>1/22/2025</value>, <value_meaning><value_meaning/>, </info>, <info>, <category>Carrier Code</category>, <category_description></category_description>, <value>5302</value>, <value_meaning><value_meaning/>, </info>, <info>, <category>Check Number</category>, <category_description></category_description>, <value>EFT6976555</value>, <value_meaning><value_meaning/>, </info>, <info>, <category>Denial Letter Codes</category>, <category_description></category_description>, <value>39929</value>, <value_meaning><value_meaning/>, </info>, <info>, <category>ANSI Reason Codes</category>, <category_description>American National Standards Institute Reason Codes</category_description>, <value>MA01</value>, <value_meaning>ALERT: IF YOU DO NOT AGREE WITH WHAT WE APPROVED FOR THESE SERVICES, YOU MAY APPEAL OUR DECISION. TO MAKE SURE THAT WE ARE FAIR TO YOU, WE REQUIRE ANOTHER INDIVIDUAL THAT DID NOT PROCESS YOUR INITIAL CLAIM TO CONDUCT THE APPEAL. HOWEVER, IN ORDER TO BE ELIGIBLE FOR AN APPEAL, YOU MUST WRITE TO US WITHIN 120 DAYS OF THE DATE YOU RECEIVED THIS NOTICE<value_meaning/>, </info>, <info>, <category>ANSI Remark Code</category>, <category_description>American National Standards Institute Remark Codes</category_description>, <value>N435</value>, <value_meaning><value_meaning/>, </info>, <info>, <category>Remarks</category>, <category_description></category_description>, <value></value>, <value_meaning>CORRECTED CLAIM-99487 CHANGED TO G0511<value_meaning/>, </info>, <info>, <category>MSP</category>, <category_description>Medicare Secondary Payer</category_description>, <value>Yes</value>, <value_meaning>Medicare is the secondary payer<value_meaning/>, </info>, <info>, <category>SNF</category>, <category_description>Skilled Nursing Facility</category_description>, <value>No</value>, <value_meaning>Patient not in a Skilled Nursing Facility<value_meaning/>, </info>, <info>, <category>Location 2</category>, <category_description></category_description>, <value>B9996</value>, <value_meaning><value_meaning/>, </info>, <info>, <category>Status</category>, <category_description></category_description>, <value>P</value>, <value_meaning>Payment floor<value_meaning/>, </info>, <info>, <category>Location 3</category>, <category_description></category_description>, <value>B9099</value>, <value_meaning><value_meaning/>, </info>, <info>, <category>Status</category>, <category_description></category_description>, <value>S</value>, <value_meaning>Claims awaiting a response from a CWF host site<value_meaning/>, </info>, <info>, <category>Location 4</category>, <category_description></category_description>, <value>B9000</value>, <value_meaning><value_meaning/>, </info>, <info>, <category>Status</category>, <category_description></category_description>, <value>S</value>, <value_meaning>Claims ready to go to a common working file (CWF) host site<value_meaning/>, </info>, <info>, <category>Location 5</category>, <category_description></category_description>, <value>B0100</value>, <value_meaning><value_meaning/>, </info>, <info>, <category>Status</category>, <category_description></category_description>, <value>S</value>, <value_meaning>Beginning of the FISS batch process<value_meaning/>, </info>, <info>, <category>Location 6</category>, <category_description></category_description>, <value>MSPRA</value>, <value_meaning><value_meaning/>, </info>, <info>, <category>Status</category>, <category_description></category_description>, <value>S</value>, <value_meaning>Claim is being processed under Medicare Secondary Payer (MSP) rules<value_meaning/>, </info>, <info>, <category>Location 7</category>, <category_description></category_description>, <value>B0100</value>, <value_meaning><value_meaning/>, </info>, <info>, <category>Status</category>, <category_description></category_description>, <value>S</value>, <value_meaning>claim adjustment has been submitted to change a non-covered claim to a covered claim, but the appropriate claim change condition code (such as D1) was not billed<value_meaning/>, </info>, <info>, <category>Attending Physician</category>, <category_description></category_description>, <value>Denise Foster</value>, <value_meaning><value_meaning/>, </info>, <info>, <category>Specialty Code</category>, <category_description></category_description>, <value>97</value>, <value_meaning><value_meaning/>, </info>, <info>, <category>Taxonomy Code</category>, <category_description></category_description>, <value>261QR1300X</value>, <value_meaning><value_meaning/>, </info>, <info>, <category>Diagnosis Code 2</category>, <category_description></category_description>, <value>F419</value>, <value_meaning>Anxiety Disorder, unspecified<value_meaning/>, </info>, <info>, <category>Diagnosis Code 3</category>, <category_description></category_description>, <value>F319</value>, <value_meaning>Bipolar Disorder, unspecified<value_meaning/>, </info>, <info>, <category>Diagnosis Code 4</category>, <category_description></category_description>, <value>Z6828</value>, <value_meaning>Body Mass Index (BMI) of 28.0-28.9 for adults<value_meaning/>, </info>, <info>, <category>Diagnosis Code 5</category>, <category_description></category_description>, <value>K219</value>, <value_meaning>Gastro-esophageal reflux disease (GERD) without esophagitis<value_meaning/>, </info>, <info>, <category>Diagnosis Code 6</category>, <category_description></category_description>, <value>I10</value>, <value_meaning>Essential (primary) hypertension<value_meaning/>, </info>, <info>, <category>Diagnosis Code 7</category>, <category_description></category_description>, <value>F4310</value>, <value_meaning>Post-Traumatic Stress Disorder (PTSD), unspecified<value_meaning/>, </info>, <info>, <category>Diagnosis Code 8</category>, <category_description></category_description>, <value>E1165</value>, <value_meaning>Type 2 diabetes mellitus with hyperglycemia<value_meaning/>, </info>, <info>, <category>H2663</category>, <category_description>COVENTRY HEALTH CARE OF MISSOURI, INC.</category_description>, <value>1285 Fernridge Parkway, Suite 200 St. Louis MO 63141</value>, <value_meaning>1-800-533-0367<value_meaning/>, </info>,</ClaimInfo>"
        },
        {
            "role": "user",
            "content": "Location code descriptions:,P B9996 Payment floor ,P B9997 Paid/Processed claim ,P B7501 Post-pay review ,P B7505 Post-pay review ,R B9997 Claims processing rejection ,D B9997 Medical review denial ,T B9900 Daily return to provider (RTP) claim – not yet accessible ,T B9997 RTP claim – claim may be accessed and corrected through the Claim and Attachments Corrections Menu (Main menu option 03) ,S B0100 Beginning of the FISS batch process ,S B6000 Claims awaiting the creation of an additional development request (ADR) letter. Do not press [F9] on these claims because FISS will generate another ADR. ,S B6001 Claims awaiting a provider’s response to an ADR letter ,S B6099 Claims awaiting a provider’s response to an ADR letter ,S B9000 Claims ready to go to a common working file (CWF) host site ,S B9099 Claims awaiting a response from a CWF host site,"
        },
        {
            "role": "user",
            "content": "Please give me a claim summary that is a few sentences in plain English that includes the DCN, the submitted date, the attending physician, the service date, the status and location 1 code and the location 1 code description. Please only provide the summary.\r\n"
        },
        {
            "role": "user",
            "content": "Produce the response as a JSON object.\\n textContent attribute includes your regular text response.\\n ssmlContent attribute includes version of the response in ssml format. Use AWS SSML standard.\\n Wrap ssml content with <speak> tags.\\n Wrap dates and years with <say-as interpret-as=''date''> ssml tag. \\n Wrap money amounts with <say-as interpret-as=''currency''> ssml tag and with a dollar sign $ before the amount value.\\n Wrap  phone numbers with <say-as interpret-as=''telephone''>\\n Don''t treat names or places as the alphanumeric values.\\n Remove all dots and dashes from the alphanumeric diagnostic codes. For example remove the dots from codes like F90.9, F43.10, F31.9 \\n Group the 5-digit alphanumeric location code into numeric and alphabetic parts. Use <say-as interpret-as=digits>  for the numeric part. For example B9997 should be B <say-as interpret-as=''digits''>9997</say-as> \\n For numeric strings longer than 4 digits, group them into 3-digit chunks, each with individual <say-as> tags and insert a comma after each chunk.\\n If the alphanumeric string is a Medicare claim Document Control Number (DCN): Group into: two 3-digit chunks, 3 2-digit chunks, and the remaining characters in the final chunk. Wrap each chunk with individual <say-as interpret-as=''digits''>,  but if the chunk contains letters,  use individual <say-as interpret-as=''characters''> for each character, insert a comma after each. Insert a comma after each chunk, a period after the last chunk.\\n Avoid putting the entire string into a single <say-as interpret-as=''characters''>.\\n Wrap numbers, that are neither dates nor years nor part of the alphanumeric value with <say-as interpret-as=''digits''> ssml tag.\\n Split long numbers on 4 digits groups. Put space between the groups. \\n For alphanumeric values put space after every letter and put space after every 4 digits.\\n Don''t wrap alphanumeric value with any ssml tags."
        }
    ]       
}
```

### Porsche UI request

```json
{
    "roleName": "PorscheAgent",    
    "question": "Can I get pink Porsche with tiger strips delivered to my Herndon mansion?",
    "potentialBuyer":"Y",
    "voiceFlag": "N",
    "history": [ 
        {
            "type": "questionResponse",
            "content": {
                "question": "Can I order car with a custom color?",
                "response": "Sure, sir! You can do it!"
            }
        }
    ],
    
}
```

### Porsche OpenAI request after going through configuration

```json
{
    "messages": [
        {
            "role": "user",
            "content": "You are a Porsche Customer Service Representative for Porsche USA."
        },
        {
            "role": "user",
            "content": "This is a question from a potential buyer. Show huge respect! Call him Sir. Provide maximum information about Porsche club, luxury services. Use posh Fench and German words in your response."
        },
        {
            "role": "user",
            "content": "Here is the interaction so far:"
        },
        {
            "role": "user",
            "content": "Can I order car with a custom color?"
        },
        {
            "role": "assistant",
            "content": "Sure, sir! You can do it!"
        },
        {
            "role": "user",
            "content": "Can I get pink Porsche with tiger strips delivered to my Herndon mansion?"
        },
        {
            "role": "user",
            "content": "Produce the response as a JSON object. textContent attribute includes your regular text response."
        },
        {
            "role": "user",
            "content": "Please get some dirt on your competitors. Bring couple of examples why Mercedes sucks."
        }
    ]       
}
```
