# JSON-LD-VersionOne

JSON-LD is an emerging standard for web APIs. Don't take my word for it. [Read all about it here](http://json-ld.org).

I want to explore what it would take to support this for the VersionOne rest-1.v1 1 APIs. I'm not sure where to really start. We have an existing endpoint, `meta.v1` that serves up XML or JSON based information about the physical schema for a given entity (we call them Asset). But, all the samples I've seen for JSON-LD have a `@context` that resolves individual members ultimately to some pre-existing schema.org document. I don't know if this is the right thing for us, given that many of our users operate our software on networks that cannot resolve external addresses.

I thought I'd need to translate our current meta into JSON-LD format for contexts / schemas, but does that mean RDF? Does it require that I actual resolve to those public addresses, or can we use our own definitions? 

Any ideas are much appreciated!

Summary information about our current API below:

# Summary

VersionOne, a system for agile project management, provides an HTTP API for CRUD operations as well as defined operations. 

# Get a story as XML

Open this link: [https://www14.v1host.com/v1sdktesting/rest-1.v1/Data/Story/3795](https://www14.v1host.com/v1sdktesting/rest-1.v1/Data/Story/3795), using `admin` / `admin` for the credentials. You should see a response like this:

```xml
<Asset href="/v1sdktesting/rest-1.v1/Data/Story/3795" id="Story:3795">
<Attribute name="AssetType">Story</Attribute>
<Attribute name="Benefits"/>
<Relation name="SplitFrom"/>
<Relation name="SecurityScope">
<Asset href="/v1sdktesting/rest-1.v1/Data/Scope/3734" idref="Scope:3734"/>
</Relation>
<Relation name="Super"/>
<Relation name="Team">
<Asset href="/v1sdktesting/rest-1.v1/Data/Team/3777" idref="Team:3777"/>
</Relation>
<Relation name="IdentifiedIn"/>
<Relation name="Parent"/>
<Relation name="Category"/>
<Relation name="Risk"/>
<Relation name="Customer"/>
<Relation name="Source"/>
<Relation name="Priority"/>
<Relation name="Status"/>
<Relation name="Timebox"/>
<Relation name="Scope">
<Asset href="/v1sdktesting/rest-1.v1/Data/Scope/3734" idref="Scope:3734"/>
</Relation>
<Attribute name="Number">B-01909</Attribute>
<Attribute name="LastVersion"/>
<Attribute name="OriginalEstimate"/>
<Attribute name="RequestedBy"/>
<Attribute name="Value"/>
<Attribute name="Order">-1052513984</Attribute>
<Attribute name="Estimate">12</Attribute>
<Attribute name="Reference"/>
<Attribute name="ToDo"/>
<Attribute name="DetailEstimate"/>
<Attribute name="Description">
As a Brainstorm user, I want to trust that Brainstorm will not lose my changes so that I can feel confident using it.
</Attribute>
<Attribute name="Name">
Investigate and fix priority update and data integrity issues.
</Attribute>
<Attribute name="AssetState">64</Attribute>
<Attribute name="SplitFrom.Name"/>
<Attribute name="SplitFrom.Number"/>
<Attribute name="SecurityScope.Name">Brainstorm 1.0</Attribute>
<Attribute name="Super.Name"/>
<Attribute name="Super.Number"/>
<Attribute name="Team.Name">Brainstorm Team</Attribute>
<Attribute name="IdentifiedIn.Name"/>
<Attribute name="Parent.Name"/>
<Attribute name="Parent.Number"/>
<Attribute name="Category.Name"/>
<Attribute name="Risk.Name"/>
<Attribute name="Customer.Name"/>
<Attribute name="Customer.Nickname"/>
<Attribute name="Source.Name"/>
<Attribute name="Priority.Name"/>
<Attribute name="Status.Name"/>
<Attribute name="Timebox.Name"/>
<Attribute name="Scope.Name">Brainstorm 1.0</Attribute>
<Attribute name="Ideas"/>
<Relation name="CompletedInBuildRuns"/>
<Attribute name="CompletedInBuildRuns.Name"/>
<Relation name="Owners"/>
<Attribute name="Owners.Name"/>
<Attribute name="Owners.Nickname"/>
</Asset>
```

The same information is available in JSON with this link: [https://www14.v1host.com/v1sdktesting/rest-1.v1/Data/Story/3795?accept=application/json](https://www14.v1host.com/v1sdktesting/rest-1.v1/Data/Story/3795?accept=application/json)

The result is like this:

```json
{
  "_type": "Asset",
  "href": "\/v1sdktesting\/rest-1.v1\/Data\/Story\/3795",
  "id": "Story:3795",
  "Attributes": {
    "AssetType": {
      "_type": "Attribute",
      "name": "AssetType",
      "value": "Story"
    },
    "Benefits": {
      "_type": "Attribute",
      "name": "Benefits",
      "value": null
    },
    "SplitFrom": {
      "_type": "Relation",
      "name": "SplitFrom",
      "value": null
    },
    "SecurityScope": {
      "_type": "Relation",
      "name": "SecurityScope",
      "value": {
        "_type": "Asset",
        "href": "\/v1sdktesting\/rest-1.v1\/Data\/Scope\/3734",
        "idref": "Scope:3734"
      }
    },
    "Super": {
      "_type": "Relation",
      "name": "Super",
      "value": null
    },
    "Team": {
      "_type": "Relation",
      "name": "Team",
      "value": {
        "_type": "Asset",
        "href": "\/v1sdktesting\/rest-1.v1\/Data\/Team\/3777",
        "idref": "Team:3777"
      }
    },
    "IdentifiedIn": {
      "_type": "Relation",
      "name": "IdentifiedIn",
      "value": null
    },
    "Parent": {
      "_type": "Relation",
      "name": "Parent",
      "value": null
    },
    "Category": {
      "_type": "Relation",
      "name": "Category",
      "value": null
    },
    "Risk": {
      "_type": "Relation",
      "name": "Risk",
      "value": null
    },
    "Customer": {
      "_type": "Relation",
      "name": "Customer",
      "value": null
    },
    "Source": {
      "_type": "Relation",
      "name": "Source",
      "value": null
    },
    "Priority": {
      "_type": "Relation",
      "name": "Priority",
      "value": null
    },
    "Status": {
      "_type": "Relation",
      "name": "Status",
      "value": null
    },
    "Timebox": {
      "_type": "Relation",
      "name": "Timebox",
      "value": null
    },
    "Scope": {
      "_type": "Relation",
      "name": "Scope",
      "value": {
        "_type": "Asset",
        "href": "\/v1sdktesting\/rest-1.v1\/Data\/Scope\/3734",
        "idref": "Scope:3734"
      }
    },
    "Number": {
      "_type": "Attribute",
      "name": "Number",
      "value": "B-01909"
    },
    "LastVersion": {
      "_type": "Attribute",
      "name": "LastVersion",
      "value": null
    },
    "OriginalEstimate": {
      "_type": "Attribute",
      "name": "OriginalEstimate",
      "value": null
    },
    "RequestedBy": {
      "_type": "Attribute",
      "name": "RequestedBy",
      "value": null
    },
    "Value": {
      "_type": "Attribute",
      "name": "Value",
      "value": null
    },
    "Order": {
      "_type": "Attribute",
      "name": "Order",
      "value": "-1052513984"
    },
    "Estimate": {
      "_type": "Attribute",
      "name": "Estimate",
      "value": 12
    },
    "Reference": {
      "_type": "Attribute",
      "name": "Reference",
      "value": null
    },
    "ToDo": {
      "_type": "Attribute",
      "name": "ToDo",
      "value": null
    },
    "DetailEstimate": {
      "_type": "Attribute",
      "name": "DetailEstimate",
      "value": null
    },
    "Description": {
      "_type": "Attribute",
      "name": "Description",
      "value": "As a Brainstorm user, I want to trust that Brainstorm will not lose my changes so that I can feel confident using it."
    },
    "Name": {
      "_type": "Attribute",
      "name": "Name",
      "value": "Investigate and fix priority update and data integrity issues."
    },
    "AssetState": {
      "_type": "Attribute",
      "name": "AssetState",
      "value": 64
    },
    "SplitFrom.Name": {
      "_type": "Attribute",
      "name": "SplitFrom.Name",
      "value": null
    },
    "SplitFrom.Number": {
      "_type": "Attribute",
      "name": "SplitFrom.Number",
      "value": null
    },
    "SecurityScope.Name": {
      "_type": "Attribute",
      "name": "SecurityScope.Name",
      "value": "Brainstorm 1.0"
    },
    "Super.Name": {
      "_type": "Attribute",
      "name": "Super.Name",
      "value": null
    },
    "Super.Number": {
      "_type": "Attribute",
      "name": "Super.Number",
      "value": null
    },
    "Team.Name": {
      "_type": "Attribute",
      "name": "Team.Name",
      "value": "Brainstorm Team"
    },
    "IdentifiedIn.Name": {
      "_type": "Attribute",
      "name": "IdentifiedIn.Name",
      "value": null
    },
    "Parent.Name": {
      "_type": "Attribute",
      "name": "Parent.Name",
      "value": null
    },
    "Parent.Number": {
      "_type": "Attribute",
      "name": "Parent.Number",
      "value": null
    },
    "Category.Name": {
      "_type": "Attribute",
      "name": "Category.Name",
      "value": null
    },
    "Risk.Name": {
      "_type": "Attribute",
      "name": "Risk.Name",
      "value": null
    },
    "Customer.Name": {
      "_type": "Attribute",
      "name": "Customer.Name",
      "value": null
    },
    "Customer.Nickname": {
      "_type": "Attribute",
      "name": "Customer.Nickname",
      "value": null
    },
    "Source.Name": {
      "_type": "Attribute",
      "name": "Source.Name",
      "value": null
    },
    "Priority.Name": {
      "_type": "Attribute",
      "name": "Priority.Name",
      "value": null
    },
    "Status.Name": {
      "_type": "Attribute",
      "name": "Status.Name",
      "value": null
    },
    "Timebox.Name": {
      "_type": "Attribute",
      "name": "Timebox.Name",
      "value": null
    },
    "Scope.Name": {
      "_type": "Attribute",
      "name": "Scope.Name",
      "value": "Brainstorm 1.0"
    },
    "Ideas": {
      "_type": "Attribute",
      "name": "Ideas",
      "value": [
        
      ]
    },
    "CompletedInBuildRuns": {
      "_type": "Relation",
      "name": "CompletedInBuildRuns",
      "value": [
        
      ]
    },
    "CompletedInBuildRuns.Name": {
      "_type": "Attribute",
      "name": "CompletedInBuildRuns.Name",
      "value": [
        
      ]
    },
    "Owners": {
      "_type": "Relation",
      "name": "Owners",
      "value": [
        
      ]
    },
    "Owners.Name": {
      "_type": "Attribute",
      "name": "Owners.Name",
      "value": [
        
      ]
    },
    "Owners.Nickname": {
      "_type": "Attribute",
      "name": "Owners.Nickname",
      "value": [
        
      ]
    }
  }
}
```

# Meta information

We also have schema, or meta, information about these resources. Here's the `Story` asset's meta information (no credentials needed):

[https://www14.v1host.com/v1sdktesting/rest-1.v1/Data/Story/3795?accept=application/json](https://www14.v1host.com/v1sdktesting/rest-1.v1/Data/Story/3795?accept=application/json)

It is available as XML without the query parameter.

```json
{
  "_type": "AssetType",
  "HREF": "\/v1sdktesting\/meta.v1\/Story",
  "Version": "14.3.2.6314",
  "Name": {
    "href": "\/v1sdktesting\/meta.v1\/Story\/Name",
    "tokenref": "Story.Name"
  },
  "Token": "Story",
  "DisplayName": "AssetType'Story",
  "Abstract": false,
  "Base": {
    "nameref": "PrimaryWorkitem",
    "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem"
  },
  "DefaultOrderBy": {
    "href": "\/v1sdktesting\/meta.v1\/Story\/Order",
    "tokenref": "Story.Order"
  },
  "DefaultDisplayBy": {
    "href": "\/v1sdktesting\/meta.v1\/Story\/Name",
    "tokenref": "Story.Name"
  },
  "ShortName": {
    "href": "\/v1sdktesting\/meta.v1\/Story\/Number",
    "tokenref": "Story.Number"
  },
  "Description": {
    "href": "\/v1sdktesting\/meta.v1\/Story\/Description",
    "tokenref": "Story.Description"
  },
  "Attributes": {
    "Story.ChangeDate": {
      "_type": "AttributeDefinition",
      "Name": "ChangeDate",
      "Token": "Story.ChangeDate",
      "DisplayName": "AttributeDefinition'ChangeDate'Story",
      "AttributeType": "Date",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/BaseAsset\/ChangeDate",
        "tokenref": "BaseAsset.ChangeDate"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/ChangeDate",
        "tokenref": "Story.ChangeDate"
      }
    },
    "Story.RetireDate": {
      "_type": "AttributeDefinition",
      "Name": "RetireDate",
      "Token": "Story.RetireDate",
      "DisplayName": "AttributeDefinition'RetireDate'Story",
      "AttributeType": "Date",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/BaseAsset\/RetireDate",
        "tokenref": "BaseAsset.RetireDate"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/RetireDate",
        "tokenref": "Story.RetireDate"
      }
    },
    "Story.CreateDate": {
      "_type": "AttributeDefinition",
      "Name": "CreateDate",
      "Token": "Story.CreateDate",
      "DisplayName": "AttributeDefinition'CreateDate'Story",
      "AttributeType": "Date",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/BaseAsset\/CreateDate",
        "tokenref": "BaseAsset.CreateDate"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/CreateDate",
        "tokenref": "Story.CreateDate"
      }
    },
    "Story.ChangeDateUTC": {
      "_type": "AttributeDefinition",
      "Name": "ChangeDateUTC",
      "Token": "Story.ChangeDateUTC",
      "DisplayName": "AttributeDefinition'ChangeDateUTC'Story",
      "AttributeType": "Date",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/BaseAsset\/ChangeDateUTC",
        "tokenref": "BaseAsset.ChangeDateUTC"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/ChangeDateUTC",
        "tokenref": "Story.ChangeDateUTC"
      }
    },
    "Story.RetireDateUTC": {
      "_type": "AttributeDefinition",
      "Name": "RetireDateUTC",
      "Token": "Story.RetireDateUTC",
      "DisplayName": "AttributeDefinition'RetireDateUTC'Story",
      "AttributeType": "Date",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/BaseAsset\/RetireDateUTC",
        "tokenref": "BaseAsset.RetireDateUTC"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/RetireDateUTC",
        "tokenref": "Story.RetireDateUTC"
      }
    },
    "Story.Days": {
      "_type": "AttributeDefinition",
      "Name": "Days",
      "Token": "Story.Days",
      "DisplayName": "AttributeDefinition'Days'Story",
      "AttributeType": "Numeric",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/BaseAsset\/Days",
        "tokenref": "BaseAsset.Days"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Days",
        "tokenref": "Story.Days"
      }
    },
    "Story.CreateDateUTC": {
      "_type": "AttributeDefinition",
      "Name": "CreateDateUTC",
      "Token": "Story.CreateDateUTC",
      "DisplayName": "AttributeDefinition'CreateDateUTC'Story",
      "AttributeType": "Date",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/BaseAsset\/CreateDateUTC",
        "tokenref": "BaseAsset.CreateDateUTC"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/CreateDateUTC",
        "tokenref": "Story.CreateDateUTC"
      }
    },
    "Story.ChangeReason": {
      "_type": "AttributeDefinition",
      "Name": "ChangeReason",
      "Token": "Story.ChangeReason",
      "DisplayName": "AttributeDefinition'ChangeReason'Story",
      "AttributeType": "Text",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/BaseAsset\/ChangeReason",
        "tokenref": "BaseAsset.ChangeReason"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/ChangeReason",
        "tokenref": "Story.ChangeReason"
      }
    },
    "Story.RetireReason": {
      "_type": "AttributeDefinition",
      "Name": "RetireReason",
      "Token": "Story.RetireReason",
      "DisplayName": "AttributeDefinition'RetireReason'Story",
      "AttributeType": "Text",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/BaseAsset\/RetireReason",
        "tokenref": "BaseAsset.RetireReason"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/RetireReason",
        "tokenref": "Story.RetireReason"
      }
    },
    "Story.CreateReason": {
      "_type": "AttributeDefinition",
      "Name": "CreateReason",
      "Token": "Story.CreateReason",
      "DisplayName": "AttributeDefinition'CreateReason'Story",
      "AttributeType": "Text",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/BaseAsset\/CreateReason",
        "tokenref": "BaseAsset.CreateReason"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/CreateReason",
        "tokenref": "Story.CreateReason"
      }
    },
    "Story.ChangeComment": {
      "_type": "AttributeDefinition",
      "Name": "ChangeComment",
      "Token": "Story.ChangeComment",
      "DisplayName": "AttributeDefinition'ChangeComment'Story",
      "AttributeType": "Text",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/BaseAsset\/ChangeComment",
        "tokenref": "BaseAsset.ChangeComment"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/ChangeComment",
        "tokenref": "Story.ChangeComment"
      }
    },
    "Story.RetireComment": {
      "_type": "AttributeDefinition",
      "Name": "RetireComment",
      "Token": "Story.RetireComment",
      "DisplayName": "AttributeDefinition'RetireComment'Story",
      "AttributeType": "Text",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/BaseAsset\/RetireComment",
        "tokenref": "BaseAsset.RetireComment"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/RetireComment",
        "tokenref": "Story.RetireComment"
      }
    },
    "Story.CreateComment": {
      "_type": "AttributeDefinition",
      "Name": "CreateComment",
      "Token": "Story.CreateComment",
      "DisplayName": "AttributeDefinition'CreateComment'Story",
      "AttributeType": "Text",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/BaseAsset\/CreateComment",
        "tokenref": "BaseAsset.CreateComment"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/CreateComment",
        "tokenref": "Story.CreateComment"
      }
    },
    "Story.ChangedBy": {
      "_type": "AttributeDefinition",
      "Name": "ChangedBy",
      "Token": "Story.ChangedBy",
      "DisplayName": "AttributeDefinition'ChangedBy'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/BaseAsset\/ChangedBy",
        "tokenref": "BaseAsset.ChangedBy"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/ChangedBy.Name",
        "tokenref": "Story.ChangedBy.Name"
      },
      "DisplayByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/ChangedBy.Name",
        "tokenref": "Story.ChangedBy.Name"
      },
      "RelatedAsset": {
        "nameref": "Member",
        "href": "\/v1sdktesting\/meta.v1\/Member"
      }
    },
    "Story.RetiredBy": {
      "_type": "AttributeDefinition",
      "Name": "RetiredBy",
      "Token": "Story.RetiredBy",
      "DisplayName": "AttributeDefinition'RetiredBy'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/BaseAsset\/RetiredBy",
        "tokenref": "BaseAsset.RetiredBy"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/RetiredBy.Name",
        "tokenref": "Story.RetiredBy.Name"
      },
      "DisplayByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/RetiredBy.Name",
        "tokenref": "Story.RetiredBy.Name"
      },
      "RelatedAsset": {
        "nameref": "Member",
        "href": "\/v1sdktesting\/meta.v1\/Member"
      }
    },
    "Story.CreatedBy": {
      "_type": "AttributeDefinition",
      "Name": "CreatedBy",
      "Token": "Story.CreatedBy",
      "DisplayName": "AttributeDefinition'CreatedBy'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/BaseAsset\/CreatedBy",
        "tokenref": "BaseAsset.CreatedBy"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/CreatedBy.Name",
        "tokenref": "Story.CreatedBy.Name"
      },
      "DisplayByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/CreatedBy.Name",
        "tokenref": "Story.CreatedBy.Name"
      },
      "RelatedAsset": {
        "nameref": "Member",
        "href": "\/v1sdktesting\/meta.v1\/Member"
      }
    },
    "Story.Viewers": {
      "_type": "AttributeDefinition",
      "Name": "Viewers",
      "Token": "Story.Viewers",
      "DisplayName": "AttributeDefinition'Viewers'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/BaseAsset\/Viewers",
        "tokenref": "BaseAsset.Viewers"
      },
      "RelatedAsset": {
        "nameref": "Member",
        "href": "\/v1sdktesting\/meta.v1\/Member"
      }
    },
    "Story.Prior": {
      "_type": "AttributeDefinition",
      "Name": "Prior",
      "Token": "Story.Prior",
      "DisplayName": "AttributeDefinition'Prior'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/BaseAsset\/Prior",
        "tokenref": "BaseAsset.Prior"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Prior.Order",
        "tokenref": "Story.Prior.Order"
      },
      "DisplayByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Prior.Name",
        "tokenref": "Story.Prior.Name"
      },
      "RelatedAsset": {
        "nameref": "Story",
        "href": "\/v1sdktesting\/meta.v1\/Story"
      }
    },
    "Story.ID": {
      "_type": "AttributeDefinition",
      "Name": "ID",
      "Token": "Story.ID",
      "DisplayName": "AttributeDefinition'ID'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/ID",
        "tokenref": "Story.ID"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/ID",
        "tokenref": "Story.ID"
      },
      "DisplayByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Name",
        "tokenref": "Story.Name"
      },
      "RelatedAsset": {
        "nameref": "Story",
        "href": "\/v1sdktesting\/meta.v1\/Story"
      }
    },
    "Story.Now": {
      "_type": "AttributeDefinition",
      "Name": "Now",
      "Token": "Story.Now",
      "DisplayName": "AttributeDefinition'Now'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/ID",
        "tokenref": "Story.ID"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Now",
        "tokenref": "Story.Now"
      },
      "DisplayByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Name",
        "tokenref": "Story.Name"
      },
      "RelatedAsset": {
        "nameref": "Story",
        "href": "\/v1sdktesting\/meta.v1\/Story"
      }
    },
    "Story.History": {
      "_type": "AttributeDefinition",
      "Name": "History",
      "Token": "Story.History",
      "DisplayName": "AttributeDefinition'History'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Now",
        "tokenref": "Story.Now"
      },
      "RelatedAsset": {
        "nameref": "Story",
        "href": "\/v1sdktesting\/meta.v1\/Story"
      }
    },
    "Story.AssetType": {
      "_type": "AttributeDefinition",
      "Name": "AssetType",
      "Token": "Story.AssetType",
      "DisplayName": "AttributeDefinition'AssetType'Story",
      "AttributeType": "AssetType",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/AssetType",
        "tokenref": "Story.AssetType"
      }
    },
    "Story.Key": {
      "_type": "AttributeDefinition",
      "Name": "Key",
      "Token": "Story.Key",
      "DisplayName": "AttributeDefinition'Key'Story",
      "AttributeType": "Opaque",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Key",
        "tokenref": "Story.Key"
      }
    },
    "Story.Moment": {
      "_type": "AttributeDefinition",
      "Name": "Moment",
      "Token": "Story.Moment",
      "DisplayName": "AttributeDefinition'Moment'Story",
      "AttributeType": "Opaque",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Moment",
        "tokenref": "Story.Moment"
      }
    },
    "Story.Is": {
      "_type": "AttributeDefinition",
      "Name": "Is",
      "Token": "Story.Is",
      "DisplayName": "AttributeDefinition'Is'Story",
      "AttributeType": "Boolean",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false
    },
    "Story.Dependencies": {
      "_type": "AttributeDefinition",
      "Name": "Dependencies",
      "Token": "Story.Dependencies",
      "DisplayName": "AttributeDefinition'Dependencies'Story",
      "AttributeType": "Relation",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/Dependencies",
        "tokenref": "PrimaryWorkitem.Dependencies"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/Dependants",
        "tokenref": "PrimaryWorkitem.Dependants"
      },
      "RelatedAsset": {
        "nameref": "PrimaryWorkitem",
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem"
      }
    },
    "Story.Dependants": {
      "_type": "AttributeDefinition",
      "Name": "Dependants",
      "Token": "Story.Dependants",
      "DisplayName": "AttributeDefinition'Dependants'Story",
      "AttributeType": "Relation",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/Dependants",
        "tokenref": "PrimaryWorkitem.Dependants"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/Dependencies",
        "tokenref": "PrimaryWorkitem.Dependencies"
      },
      "RelatedAsset": {
        "nameref": "PrimaryWorkitem",
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem"
      }
    },
    "Story.EmbeddedImages": {
      "_type": "AttributeDefinition",
      "Name": "EmbeddedImages",
      "Token": "Story.EmbeddedImages",
      "DisplayName": "AttributeDefinition'EmbeddedImages'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/BaseAsset\/EmbeddedImages",
        "tokenref": "BaseAsset.EmbeddedImages"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/EmbeddedImage\/Asset",
        "tokenref": "EmbeddedImage.Asset"
      },
      "RelatedAsset": {
        "nameref": "EmbeddedImage",
        "href": "\/v1sdktesting\/meta.v1\/EmbeddedImage"
      }
    },
    "Story.MorphedInto": {
      "_type": "AttributeDefinition",
      "Name": "MorphedInto",
      "Token": "Story.MorphedInto",
      "DisplayName": "AttributeDefinition'MorphedInto'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Epic\/MorphedFrom",
        "tokenref": "Epic.MorphedFrom"
      },
      "RelatedAsset": {
        "nameref": "Epic",
        "href": "\/v1sdktesting\/meta.v1\/Epic"
      }
    },
    "Story.MentionedInExpressions": {
      "_type": "AttributeDefinition",
      "Name": "MentionedInExpressions",
      "Token": "Story.MentionedInExpressions",
      "DisplayName": "AttributeDefinition'MentionedInExpressions'Story",
      "AttributeType": "Relation",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/BaseAsset\/MentionedInExpressions",
        "tokenref": "BaseAsset.MentionedInExpressions"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Expression\/Mentions",
        "tokenref": "Expression.Mentions"
      },
      "RelatedAsset": {
        "nameref": "Expression",
        "href": "\/v1sdktesting\/meta.v1\/Expression"
      }
    },
    "Story.Benefits": {
      "_type": "AttributeDefinition",
      "Name": "Benefits",
      "Token": "Story.Benefits",
      "DisplayName": "AttributeDefinition'Benefits'Story",
      "AttributeType": "LongText",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Benefits",
        "tokenref": "Story.Benefits"
      }
    },
    "Story.SplitFrom": {
      "_type": "AttributeDefinition",
      "Name": "SplitFrom",
      "Token": "Story.SplitFrom",
      "DisplayName": "AttributeDefinition'SplitFrom'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/SplitFrom",
        "tokenref": "PrimaryWorkitem.SplitFrom"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/SplitTo",
        "tokenref": "PrimaryWorkitem.SplitTo"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/SplitFrom.Order",
        "tokenref": "Story.SplitFrom.Order"
      },
      "DisplayByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/SplitFrom.Name",
        "tokenref": "Story.SplitFrom.Name"
      },
      "RelatedAsset": {
        "nameref": "PrimaryWorkitem",
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem"
      }
    },
    "Story.SplitTo": {
      "_type": "AttributeDefinition",
      "Name": "SplitTo",
      "Token": "Story.SplitTo",
      "DisplayName": "AttributeDefinition'SplitTo'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/SplitTo",
        "tokenref": "PrimaryWorkitem.SplitTo"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/SplitFrom",
        "tokenref": "PrimaryWorkitem.SplitFrom"
      },
      "RelatedAsset": {
        "nameref": "PrimaryWorkitem",
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem"
      }
    },
    "Story.SplitFromMeAndUp": {
      "_type": "AttributeDefinition",
      "Name": "SplitFromMeAndUp",
      "Token": "Story.SplitFromMeAndUp",
      "DisplayName": "AttributeDefinition'SplitFromMeAndUp'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/SplitFromMeAndUp",
        "tokenref": "PrimaryWorkitem.SplitFromMeAndUp"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/SplitToMeAndDown",
        "tokenref": "PrimaryWorkitem.SplitToMeAndDown"
      },
      "RelatedAsset": {
        "nameref": "PrimaryWorkitem",
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem"
      }
    },
    "Story.SplitFromAndUp": {
      "_type": "AttributeDefinition",
      "Name": "SplitFromAndUp",
      "Token": "Story.SplitFromAndUp",
      "DisplayName": "AttributeDefinition'SplitFromAndUp'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/SplitFromAndUp",
        "tokenref": "PrimaryWorkitem.SplitFromAndUp"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/SplitToAndDown",
        "tokenref": "PrimaryWorkitem.SplitToAndDown"
      },
      "RelatedAsset": {
        "nameref": "PrimaryWorkitem",
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem"
      }
    },
    "Story.SplitFromAndMe": {
      "_type": "AttributeDefinition",
      "Name": "SplitFromAndMe",
      "Token": "Story.SplitFromAndMe",
      "DisplayName": "AttributeDefinition'SplitFromAndMe'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/SplitFromAndMe",
        "tokenref": "PrimaryWorkitem.SplitFromAndMe"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/SplitToAndMe",
        "tokenref": "PrimaryWorkitem.SplitToAndMe"
      },
      "RelatedAsset": {
        "nameref": "PrimaryWorkitem",
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem"
      }
    },
    "Story.SplitToMeAndDown": {
      "_type": "AttributeDefinition",
      "Name": "SplitToMeAndDown",
      "Token": "Story.SplitToMeAndDown",
      "DisplayName": "AttributeDefinition'SplitToMeAndDown'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/SplitToMeAndDown",
        "tokenref": "PrimaryWorkitem.SplitToMeAndDown"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/SplitFromMeAndUp",
        "tokenref": "PrimaryWorkitem.SplitFromMeAndUp"
      },
      "RelatedAsset": {
        "nameref": "PrimaryWorkitem",
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem"
      }
    },
    "Story.SplitToAndDown": {
      "_type": "AttributeDefinition",
      "Name": "SplitToAndDown",
      "Token": "Story.SplitToAndDown",
      "DisplayName": "AttributeDefinition'SplitToAndDown'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/SplitToAndDown",
        "tokenref": "PrimaryWorkitem.SplitToAndDown"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/SplitFromAndUp",
        "tokenref": "PrimaryWorkitem.SplitFromAndUp"
      },
      "RelatedAsset": {
        "nameref": "PrimaryWorkitem",
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem"
      }
    },
    "Story.SplitToAndMe": {
      "_type": "AttributeDefinition",
      "Name": "SplitToAndMe",
      "Token": "Story.SplitToAndMe",
      "DisplayName": "AttributeDefinition'SplitToAndMe'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/SplitToAndMe",
        "tokenref": "PrimaryWorkitem.SplitToAndMe"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/SplitFromAndMe",
        "tokenref": "PrimaryWorkitem.SplitFromAndMe"
      },
      "RelatedAsset": {
        "nameref": "PrimaryWorkitem",
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem"
      }
    },
    "Story.Ideas": {
      "_type": "AttributeDefinition",
      "Name": "Ideas",
      "Token": "Story.Ideas",
      "DisplayName": "AttributeDefinition'Ideas'Story",
      "AttributeType": "LongInt",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/BaseAsset\/Ideas",
        "tokenref": "BaseAsset.Ideas"
      }
    },
    "Story.Messages": {
      "_type": "AttributeDefinition",
      "Name": "Messages",
      "Token": "Story.Messages",
      "DisplayName": "AttributeDefinition'Messages'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/BaseAsset\/Messages",
        "tokenref": "BaseAsset.Messages"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Message\/Asset",
        "tokenref": "Message.Asset"
      },
      "RelatedAsset": {
        "nameref": "Message",
        "href": "\/v1sdktesting\/meta.v1\/Message"
      }
    },
    "Story.CompletedInBuildRuns": {
      "_type": "AttributeDefinition",
      "Name": "CompletedInBuildRuns",
      "Token": "Story.CompletedInBuildRuns",
      "DisplayName": "AttributeDefinition'CompletedInBuildRuns'Story",
      "AttributeType": "Relation",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/CompletedInBuildRuns",
        "tokenref": "PrimaryWorkitem.CompletedInBuildRuns"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/BuildRun\/CompletesPrimaryWorkitems",
        "tokenref": "BuildRun.CompletesPrimaryWorkitems"
      },
      "RelatedAsset": {
        "nameref": "BuildRun",
        "href": "\/v1sdktesting\/meta.v1\/BuildRun"
      }
    },
    "Story.SecurityScope": {
      "_type": "AttributeDefinition",
      "Name": "SecurityScope",
      "Token": "Story.SecurityScope",
      "DisplayName": "AttributeDefinition'SecurityScope'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/BaseAsset\/SecurityScope",
        "tokenref": "BaseAsset.SecurityScope"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Scope\/SecuredAssets",
        "tokenref": "Scope.SecuredAssets"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/SecurityScope.Name",
        "tokenref": "Story.SecurityScope.Name"
      },
      "DisplayByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/SecurityScope.Name",
        "tokenref": "Story.SecurityScope.Name"
      },
      "RelatedAsset": {
        "nameref": "Scope",
        "href": "\/v1sdktesting\/meta.v1\/Scope"
      }
    },
    "Story.Super": {
      "_type": "AttributeDefinition",
      "Name": "Super",
      "Token": "Story.Super",
      "DisplayName": "AttributeDefinition'Super'Story",
      "AttributeType": "Relation",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/Super",
        "tokenref": "Workitem.Super"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Epic\/Subs",
        "tokenref": "Epic.Subs"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Super.Order",
        "tokenref": "Story.Super.Order"
      },
      "DisplayByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Super.Name",
        "tokenref": "Story.Super.Name"
      },
      "RelatedAsset": {
        "nameref": "Epic",
        "href": "\/v1sdktesting\/meta.v1\/Epic"
      }
    },
    "Story.Subs": {
      "_type": "AttributeDefinition",
      "Name": "Subs",
      "Token": "Story.Subs",
      "DisplayName": "AttributeDefinition'Subs'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/Subs",
        "tokenref": "Workitem.Subs"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/Super",
        "tokenref": "Workitem.Super"
      },
      "RelatedAsset": {
        "nameref": "Workitem",
        "href": "\/v1sdktesting\/meta.v1\/Workitem"
      }
    },
    "Story.SuperMeAndUp": {
      "_type": "AttributeDefinition",
      "Name": "SuperMeAndUp",
      "Token": "Story.SuperMeAndUp",
      "DisplayName": "AttributeDefinition'SuperMeAndUp'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/SuperMeAndUp",
        "tokenref": "Workitem.SuperMeAndUp"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/SubsMeAndDown",
        "tokenref": "Workitem.SubsMeAndDown"
      },
      "RelatedAsset": {
        "nameref": "Workitem",
        "href": "\/v1sdktesting\/meta.v1\/Workitem"
      }
    },
    "Story.SuperAndUp": {
      "_type": "AttributeDefinition",
      "Name": "SuperAndUp",
      "Token": "Story.SuperAndUp",
      "DisplayName": "AttributeDefinition'SuperAndUp'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/SuperAndUp",
        "tokenref": "Workitem.SuperAndUp"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/SubsAndDown",
        "tokenref": "Workitem.SubsAndDown"
      },
      "RelatedAsset": {
        "nameref": "Workitem",
        "href": "\/v1sdktesting\/meta.v1\/Workitem"
      }
    },
    "Story.SuperAndMe": {
      "_type": "AttributeDefinition",
      "Name": "SuperAndMe",
      "Token": "Story.SuperAndMe",
      "DisplayName": "AttributeDefinition'SuperAndMe'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/SuperAndMe",
        "tokenref": "Workitem.SuperAndMe"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/SubsAndMe",
        "tokenref": "Workitem.SubsAndMe"
      },
      "RelatedAsset": {
        "nameref": "Workitem",
        "href": "\/v1sdktesting\/meta.v1\/Workitem"
      }
    },
    "Story.SubsMeAndDown": {
      "_type": "AttributeDefinition",
      "Name": "SubsMeAndDown",
      "Token": "Story.SubsMeAndDown",
      "DisplayName": "AttributeDefinition'SubsMeAndDown'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/SubsMeAndDown",
        "tokenref": "Workitem.SubsMeAndDown"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/SuperMeAndUp",
        "tokenref": "Workitem.SuperMeAndUp"
      },
      "RelatedAsset": {
        "nameref": "Workitem",
        "href": "\/v1sdktesting\/meta.v1\/Workitem"
      }
    },
    "Story.SubsAndDown": {
      "_type": "AttributeDefinition",
      "Name": "SubsAndDown",
      "Token": "Story.SubsAndDown",
      "DisplayName": "AttributeDefinition'SubsAndDown'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/SubsAndDown",
        "tokenref": "Workitem.SubsAndDown"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/SuperAndUp",
        "tokenref": "Workitem.SuperAndUp"
      },
      "RelatedAsset": {
        "nameref": "Workitem",
        "href": "\/v1sdktesting\/meta.v1\/Workitem"
      }
    },
    "Story.SubsAndMe": {
      "_type": "AttributeDefinition",
      "Name": "SubsAndMe",
      "Token": "Story.SubsAndMe",
      "DisplayName": "AttributeDefinition'SubsAndMe'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/SubsAndMe",
        "tokenref": "Workitem.SubsAndMe"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/SuperAndMe",
        "tokenref": "Workitem.SuperAndMe"
      },
      "RelatedAsset": {
        "nameref": "Workitem",
        "href": "\/v1sdktesting\/meta.v1\/Workitem"
      }
    },
    "Story.Goals": {
      "_type": "AttributeDefinition",
      "Name": "Goals",
      "Token": "Story.Goals",
      "DisplayName": "AttributeDefinition'Goals'Story",
      "AttributeType": "Relation",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/Goals",
        "tokenref": "Workitem.Goals"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Goal\/Workitems",
        "tokenref": "Goal.Workitems"
      },
      "RelatedAsset": {
        "nameref": "Goal",
        "href": "\/v1sdktesting\/meta.v1\/Goal"
      }
    },
    "Story.Team": {
      "_type": "AttributeDefinition",
      "Name": "Team",
      "Token": "Story.Team",
      "DisplayName": "AttributeDefinition'Team'Story",
      "AttributeType": "Relation",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/Team",
        "tokenref": "Workitem.Team"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Team\/Workitems",
        "tokenref": "Team.Workitems"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Team.Name",
        "tokenref": "Story.Team.Name"
      },
      "DisplayByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Team.Name",
        "tokenref": "Story.Team.Name"
      },
      "RelatedAsset": {
        "nameref": "Team",
        "href": "\/v1sdktesting\/meta.v1\/Team"
      }
    },
    "Story.IdentifiedIn": {
      "_type": "AttributeDefinition",
      "Name": "IdentifiedIn",
      "Token": "Story.IdentifiedIn",
      "DisplayName": "AttributeDefinition'IdentifiedIn'Story",
      "AttributeType": "Relation",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Retrospective\/IdentifiedStories",
        "tokenref": "Retrospective.IdentifiedStories"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/IdentifiedIn.Name",
        "tokenref": "Story.IdentifiedIn.Name"
      },
      "DisplayByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/IdentifiedIn.Name",
        "tokenref": "Story.IdentifiedIn.Name"
      },
      "RelatedAsset": {
        "nameref": "Retrospective",
        "href": "\/v1sdktesting\/meta.v1\/Retrospective"
      }
    },
    "Story.ChangeSets": {
      "_type": "AttributeDefinition",
      "Name": "ChangeSets",
      "Token": "Story.ChangeSets",
      "DisplayName": "AttributeDefinition'ChangeSets'Story",
      "AttributeType": "Relation",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/ChangeSets",
        "tokenref": "PrimaryWorkitem.ChangeSets"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/ChangeSet\/PrimaryWorkitems",
        "tokenref": "ChangeSet.PrimaryWorkitems"
      },
      "RelatedAsset": {
        "nameref": "ChangeSet",
        "href": "\/v1sdktesting\/meta.v1\/ChangeSet"
      }
    },
    "Story.AffectedByDefects": {
      "_type": "AttributeDefinition",
      "Name": "AffectedByDefects",
      "Token": "Story.AffectedByDefects",
      "DisplayName": "AttributeDefinition'AffectedByDefects'Story",
      "AttributeType": "Relation",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/AffectedByDefects",
        "tokenref": "PrimaryWorkitem.AffectedByDefects"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Defect\/AffectedPrimaryWorkitems",
        "tokenref": "Defect.AffectedPrimaryWorkitems"
      },
      "RelatedAsset": {
        "nameref": "Defect",
        "href": "\/v1sdktesting\/meta.v1\/Defect"
      }
    },
    "Story.Requests": {
      "_type": "AttributeDefinition",
      "Name": "Requests",
      "Token": "Story.Requests",
      "DisplayName": "AttributeDefinition'Requests'Story",
      "AttributeType": "Relation",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/Requests",
        "tokenref": "PrimaryWorkitem.Requests"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Request\/PrimaryWorkitems",
        "tokenref": "Request.PrimaryWorkitems"
      },
      "RelatedAsset": {
        "nameref": "Request",
        "href": "\/v1sdktesting\/meta.v1\/Request"
      }
    },
    "Story.BlockingIssues": {
      "_type": "AttributeDefinition",
      "Name": "BlockingIssues",
      "Token": "Story.BlockingIssues",
      "DisplayName": "AttributeDefinition'BlockingIssues'Story",
      "AttributeType": "Relation",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/BlockingIssues",
        "tokenref": "PrimaryWorkitem.BlockingIssues"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Issue\/BlockedPrimaryWorkitems",
        "tokenref": "Issue.BlockedPrimaryWorkitems"
      },
      "RelatedAsset": {
        "nameref": "Issue",
        "href": "\/v1sdktesting\/meta.v1\/Issue"
      }
    },
    "Story.Issues": {
      "_type": "AttributeDefinition",
      "Name": "Issues",
      "Token": "Story.Issues",
      "DisplayName": "AttributeDefinition'Issues'Story",
      "AttributeType": "Relation",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/Issues",
        "tokenref": "PrimaryWorkitem.Issues"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Issue\/PrimaryWorkitems",
        "tokenref": "Issue.PrimaryWorkitems"
      },
      "RelatedAsset": {
        "nameref": "Issue",
        "href": "\/v1sdktesting\/meta.v1\/Issue"
      }
    },
    "Story.Owners": {
      "_type": "AttributeDefinition",
      "Name": "Owners",
      "Token": "Story.Owners",
      "DisplayName": "AttributeDefinition'Owners'Story",
      "AttributeType": "Relation",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/Owners",
        "tokenref": "Workitem.Owners"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Member\/OwnedWorkitems",
        "tokenref": "Member.OwnedWorkitems"
      },
      "RelatedAsset": {
        "nameref": "Member",
        "href": "\/v1sdktesting\/meta.v1\/Member"
      }
    },
    "Story.Parent": {
      "_type": "AttributeDefinition",
      "Name": "Parent",
      "Token": "Story.Parent",
      "DisplayName": "AttributeDefinition'Parent'Story",
      "AttributeType": "Relation",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/Parent",
        "tokenref": "Workitem.Parent"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Theme\/Children",
        "tokenref": "Theme.Children"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Parent.Name",
        "tokenref": "Story.Parent.Name"
      },
      "DisplayByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Parent.Name",
        "tokenref": "Story.Parent.Name"
      },
      "RelatedAsset": {
        "nameref": "Theme",
        "href": "\/v1sdktesting\/meta.v1\/Theme"
      }
    },
    "Story.Children": {
      "_type": "AttributeDefinition",
      "Name": "Children",
      "Token": "Story.Children",
      "DisplayName": "AttributeDefinition'Children'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/Children",
        "tokenref": "Workitem.Children"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/Parent",
        "tokenref": "Workitem.Parent"
      },
      "RelatedAsset": {
        "nameref": "Workitem",
        "href": "\/v1sdktesting\/meta.v1\/Workitem"
      }
    },
    "Story.ParentMeAndUp": {
      "_type": "AttributeDefinition",
      "Name": "ParentMeAndUp",
      "Token": "Story.ParentMeAndUp",
      "DisplayName": "AttributeDefinition'ParentMeAndUp'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/ParentMeAndUp",
        "tokenref": "Workitem.ParentMeAndUp"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/ChildrenMeAndDown",
        "tokenref": "Workitem.ChildrenMeAndDown"
      },
      "RelatedAsset": {
        "nameref": "Workitem",
        "href": "\/v1sdktesting\/meta.v1\/Workitem"
      }
    },
    "Story.ParentAndUp": {
      "_type": "AttributeDefinition",
      "Name": "ParentAndUp",
      "Token": "Story.ParentAndUp",
      "DisplayName": "AttributeDefinition'ParentAndUp'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/ParentAndUp",
        "tokenref": "Workitem.ParentAndUp"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/ChildrenAndDown",
        "tokenref": "Workitem.ChildrenAndDown"
      },
      "RelatedAsset": {
        "nameref": "Workitem",
        "href": "\/v1sdktesting\/meta.v1\/Workitem"
      }
    },
    "Story.ParentAndMe": {
      "_type": "AttributeDefinition",
      "Name": "ParentAndMe",
      "Token": "Story.ParentAndMe",
      "DisplayName": "AttributeDefinition'ParentAndMe'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/ParentAndMe",
        "tokenref": "Workitem.ParentAndMe"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/ChildrenAndMe",
        "tokenref": "Workitem.ChildrenAndMe"
      },
      "RelatedAsset": {
        "nameref": "Workitem",
        "href": "\/v1sdktesting\/meta.v1\/Workitem"
      }
    },
    "Story.ChildrenMeAndDown": {
      "_type": "AttributeDefinition",
      "Name": "ChildrenMeAndDown",
      "Token": "Story.ChildrenMeAndDown",
      "DisplayName": "AttributeDefinition'ChildrenMeAndDown'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/ChildrenMeAndDown",
        "tokenref": "Workitem.ChildrenMeAndDown"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/ParentMeAndUp",
        "tokenref": "Workitem.ParentMeAndUp"
      },
      "RelatedAsset": {
        "nameref": "Workitem",
        "href": "\/v1sdktesting\/meta.v1\/Workitem"
      }
    },
    "Story.ChildrenAndDown": {
      "_type": "AttributeDefinition",
      "Name": "ChildrenAndDown",
      "Token": "Story.ChildrenAndDown",
      "DisplayName": "AttributeDefinition'ChildrenAndDown'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/ChildrenAndDown",
        "tokenref": "Workitem.ChildrenAndDown"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/ParentAndUp",
        "tokenref": "Workitem.ParentAndUp"
      },
      "RelatedAsset": {
        "nameref": "Workitem",
        "href": "\/v1sdktesting\/meta.v1\/Workitem"
      }
    },
    "Story.ChildrenAndMe": {
      "_type": "AttributeDefinition",
      "Name": "ChildrenAndMe",
      "Token": "Story.ChildrenAndMe",
      "DisplayName": "AttributeDefinition'ChildrenAndMe'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/ChildrenAndMe",
        "tokenref": "Workitem.ChildrenAndMe"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/ParentAndMe",
        "tokenref": "Workitem.ParentAndMe"
      },
      "RelatedAsset": {
        "nameref": "Workitem",
        "href": "\/v1sdktesting\/meta.v1\/Workitem"
      }
    },
    "Story.Attachments": {
      "_type": "AttributeDefinition",
      "Name": "Attachments",
      "Token": "Story.Attachments",
      "DisplayName": "AttributeDefinition'Attachments'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/BaseAsset\/Attachments",
        "tokenref": "BaseAsset.Attachments"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Attachment\/Asset",
        "tokenref": "Attachment.Asset"
      },
      "RelatedAsset": {
        "nameref": "Attachment",
        "href": "\/v1sdktesting\/meta.v1\/Attachment"
      }
    },
    "Story.Actuals": {
      "_type": "AttributeDefinition",
      "Name": "Actuals",
      "Token": "Story.Actuals",
      "DisplayName": "AttributeDefinition'Actuals'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/Actuals",
        "tokenref": "Workitem.Actuals"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Actual\/Workitem",
        "tokenref": "Actual.Workitem"
      },
      "RelatedAsset": {
        "nameref": "Actual",
        "href": "\/v1sdktesting\/meta.v1\/Actual"
      }
    },
    "Story.Links": {
      "_type": "AttributeDefinition",
      "Name": "Links",
      "Token": "Story.Links",
      "DisplayName": "AttributeDefinition'Links'Story",
      "AttributeType": "Relation",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": true,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/BaseAsset\/Links",
        "tokenref": "BaseAsset.Links"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Link\/Asset",
        "tokenref": "Link.Asset"
      },
      "RelatedAsset": {
        "nameref": "Link",
        "href": "\/v1sdktesting\/meta.v1\/Link"
      }
    },
    "Story.Category": {
      "_type": "AttributeDefinition",
      "Name": "Category",
      "Token": "Story.Category",
      "DisplayName": "AttributeDefinition'Category'Story",
      "AttributeType": "Relation",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/StoryCategory\/Stories",
        "tokenref": "StoryCategory.Stories"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Category.Order",
        "tokenref": "Story.Category.Order"
      },
      "DisplayByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Category.Name",
        "tokenref": "Story.Category.Name"
      },
      "RelatedAsset": {
        "nameref": "StoryCategory",
        "href": "\/v1sdktesting\/meta.v1\/StoryCategory"
      }
    },
    "Story.Risk": {
      "_type": "AttributeDefinition",
      "Name": "Risk",
      "Token": "Story.Risk",
      "DisplayName": "AttributeDefinition'Risk'Story",
      "AttributeType": "Relation",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/WorkitemRisk\/Stories",
        "tokenref": "WorkitemRisk.Stories"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Risk.Order",
        "tokenref": "Story.Risk.Order"
      },
      "DisplayByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Risk.Name",
        "tokenref": "Story.Risk.Name"
      },
      "RelatedAsset": {
        "nameref": "WorkitemRisk",
        "href": "\/v1sdktesting\/meta.v1\/WorkitemRisk"
      }
    },
    "Story.Customer": {
      "_type": "AttributeDefinition",
      "Name": "Customer",
      "Token": "Story.Customer",
      "DisplayName": "AttributeDefinition'Customer'Story",
      "AttributeType": "Relation",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Member\/CustomeredStories",
        "tokenref": "Member.CustomeredStories"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Customer.Name",
        "tokenref": "Story.Customer.Name"
      },
      "DisplayByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Customer.Name",
        "tokenref": "Story.Customer.Name"
      },
      "RelatedAsset": {
        "nameref": "Member",
        "href": "\/v1sdktesting\/meta.v1\/Member"
      }
    },
    "Story.Source": {
      "_type": "AttributeDefinition",
      "Name": "Source",
      "Token": "Story.Source",
      "DisplayName": "AttributeDefinition'Source'Story",
      "AttributeType": "Relation",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": true,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/Source",
        "tokenref": "PrimaryWorkitem.Source"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/StorySource\/PrimaryWorkitems",
        "tokenref": "StorySource.PrimaryWorkitems"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Source.Order",
        "tokenref": "Story.Source.Order"
      },
      "DisplayByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Source.Name",
        "tokenref": "Story.Source.Name"
      },
      "RelatedAsset": {
        "nameref": "StorySource",
        "href": "\/v1sdktesting\/meta.v1\/StorySource"
      }
    },
    "Story.Priority": {
      "_type": "AttributeDefinition",
      "Name": "Priority",
      "Token": "Story.Priority",
      "DisplayName": "AttributeDefinition'Priority'Story",
      "AttributeType": "Relation",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/Priority",
        "tokenref": "PrimaryWorkitem.Priority"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/WorkitemPriority\/PrimaryWorkitems",
        "tokenref": "WorkitemPriority.PrimaryWorkitems"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Priority.Order",
        "tokenref": "Story.Priority.Order"
      },
      "DisplayByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Priority.Name",
        "tokenref": "Story.Priority.Name"
      },
      "RelatedAsset": {
        "nameref": "WorkitemPriority",
        "href": "\/v1sdktesting\/meta.v1\/WorkitemPriority"
      }
    },
    "Story.Status": {
      "_type": "AttributeDefinition",
      "Name": "Status",
      "Token": "Story.Status",
      "DisplayName": "AttributeDefinition'Status'Story",
      "AttributeType": "Relation",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/Status",
        "tokenref": "PrimaryWorkitem.Status"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/StoryStatus\/PrimaryWorkitems",
        "tokenref": "StoryStatus.PrimaryWorkitems"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Status.Order",
        "tokenref": "Story.Status.Order"
      },
      "DisplayByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Status.Name",
        "tokenref": "Story.Status.Name"
      },
      "RelatedAsset": {
        "nameref": "StoryStatus",
        "href": "\/v1sdktesting\/meta.v1\/StoryStatus"
      }
    },
    "Story.Timebox": {
      "_type": "AttributeDefinition",
      "Name": "Timebox",
      "Token": "Story.Timebox",
      "DisplayName": "AttributeDefinition'Timebox'Story",
      "AttributeType": "Relation",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/Timebox",
        "tokenref": "Workitem.Timebox"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Timebox\/Workitems",
        "tokenref": "Timebox.Workitems"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Timebox.EndDate",
        "tokenref": "Story.Timebox.EndDate"
      },
      "DisplayByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Timebox.Name",
        "tokenref": "Story.Timebox.Name"
      },
      "RelatedAsset": {
        "nameref": "Timebox",
        "href": "\/v1sdktesting\/meta.v1\/Timebox"
      }
    },
    "Story.Scope": {
      "_type": "AttributeDefinition",
      "Name": "Scope",
      "Token": "Story.Scope",
      "DisplayName": "AttributeDefinition'Scope'Story",
      "AttributeType": "Relation",
      "IsReadOnly": false,
      "IsRequired": true,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/Scope",
        "tokenref": "Workitem.Scope"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Scope\/Workitems",
        "tokenref": "Scope.Workitems"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Scope.Name",
        "tokenref": "Story.Scope.Name"
      },
      "DisplayByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Scope.Name",
        "tokenref": "Story.Scope.Name"
      },
      "RelatedAsset": {
        "nameref": "Scope",
        "href": "\/v1sdktesting\/meta.v1\/Scope"
      }
    },
    "Story.Number": {
      "_type": "AttributeDefinition",
      "Name": "Number",
      "Token": "Story.Number",
      "DisplayName": "AttributeDefinition'Number'Story",
      "AttributeType": "Text",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/Number",
        "tokenref": "Workitem.Number"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Number",
        "tokenref": "Story.Number"
      }
    },
    "Story.LastVersion": {
      "_type": "AttributeDefinition",
      "Name": "LastVersion",
      "Token": "Story.LastVersion",
      "DisplayName": "AttributeDefinition'LastVersion'Story",
      "AttributeType": "Text",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": true,
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/LastVersion",
        "tokenref": "Story.LastVersion"
      }
    },
    "Story.OriginalEstimate": {
      "_type": "AttributeDefinition",
      "Name": "OriginalEstimate",
      "Token": "Story.OriginalEstimate",
      "DisplayName": "AttributeDefinition'OriginalEstimate'Story",
      "AttributeType": "Numeric",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": true,
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/OriginalEstimate",
        "tokenref": "Story.OriginalEstimate"
      }
    },
    "Story.RequestedBy": {
      "_type": "AttributeDefinition",
      "Name": "RequestedBy",
      "Token": "Story.RequestedBy",
      "DisplayName": "AttributeDefinition'RequestedBy'Story",
      "AttributeType": "Text",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": true,
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/RequestedBy",
        "tokenref": "Story.RequestedBy"
      }
    },
    "Story.Value": {
      "_type": "AttributeDefinition",
      "Name": "Value",
      "Token": "Story.Value",
      "DisplayName": "AttributeDefinition'Value'Story",
      "AttributeType": "Numeric",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Value",
        "tokenref": "Story.Value"
      }
    },
    "Story.Order": {
      "_type": "AttributeDefinition",
      "Name": "Order",
      "Token": "Story.Order",
      "DisplayName": "AttributeDefinition'Order'Story",
      "AttributeType": "Rank",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/Order",
        "tokenref": "PrimaryWorkitem.Order"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Order",
        "tokenref": "Story.Order"
      }
    },
    "Story.Estimate": {
      "_type": "AttributeDefinition",
      "Name": "Estimate",
      "Token": "Story.Estimate",
      "DisplayName": "AttributeDefinition'Estimate'Story",
      "AttributeType": "Numeric",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/Estimate",
        "tokenref": "PrimaryWorkitem.Estimate"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Estimate",
        "tokenref": "Story.Estimate"
      }
    },
    "Story.Reference": {
      "_type": "AttributeDefinition",
      "Name": "Reference",
      "Token": "Story.Reference",
      "DisplayName": "AttributeDefinition'Reference'Story",
      "AttributeType": "Text",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": true,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/Reference",
        "tokenref": "Workitem.Reference"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Reference",
        "tokenref": "Story.Reference"
      }
    },
    "Story.ToDo": {
      "_type": "AttributeDefinition",
      "Name": "ToDo",
      "Token": "Story.ToDo",
      "DisplayName": "AttributeDefinition'ToDo'Story",
      "AttributeType": "Numeric",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/ToDo",
        "tokenref": "Workitem.ToDo"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/ToDo",
        "tokenref": "Story.ToDo"
      }
    },
    "Story.DetailEstimate": {
      "_type": "AttributeDefinition",
      "Name": "DetailEstimate",
      "Token": "Story.DetailEstimate",
      "DisplayName": "AttributeDefinition'DetailEstimate'Story",
      "AttributeType": "Numeric",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/DetailEstimate",
        "tokenref": "Workitem.DetailEstimate"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/DetailEstimate",
        "tokenref": "Story.DetailEstimate"
      }
    },
    "Story.Description": {
      "_type": "AttributeDefinition",
      "Name": "Description",
      "Token": "Story.Description",
      "DisplayName": "AttributeDefinition'Description'Story",
      "AttributeType": "LongText",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/BaseAsset\/Description",
        "tokenref": "BaseAsset.Description"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Description",
        "tokenref": "Story.Description"
      }
    },
    "Story.Name": {
      "_type": "AttributeDefinition",
      "Name": "Name",
      "Token": "Story.Name",
      "DisplayName": "AttributeDefinition'Name'Story",
      "AttributeType": "Text",
      "IsReadOnly": false,
      "IsRequired": true,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/BaseAsset\/Name",
        "tokenref": "BaseAsset.Name"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Name",
        "tokenref": "Story.Name"
      }
    },
    "Story.AssetState": {
      "_type": "AttributeDefinition",
      "Name": "AssetState",
      "Token": "Story.AssetState",
      "DisplayName": "AttributeDefinition'AssetState'Story",
      "AttributeType": "State",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/BaseAsset\/AssetState",
        "tokenref": "BaseAsset.AssetState"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/AssetState",
        "tokenref": "Story.AssetState"
      }
    },
    "Story.Custom_ooooo": {
      "_type": "AttributeDefinition",
      "Name": "Custom_ooooo",
      "Token": "Story.Custom_ooooo",
      "DisplayName": "AttributeDefinition'Custom_ooooo'Story",
      "AttributeType": "Relation",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": false,
      "IsCustom": true,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/Custom_ooooo",
        "tokenref": "PrimaryWorkitem.Custom_ooooo"
      },
      "ReciprocalRelation": {
        "href": "\/v1sdktesting\/meta.v1\/Custom_zzz\/ReciprocalOf_PrimaryWorkitem_Custom_ooooo",
        "tokenref": "Custom_zzz.ReciprocalOf_PrimaryWorkitem_Custom_ooooo"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Custom_ooooo.Order",
        "tokenref": "Story.Custom_ooooo.Order"
      },
      "DisplayByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Custom_ooooo.Name",
        "tokenref": "Story.Custom_ooooo.Name"
      },
      "RelatedAsset": {
        "nameref": "Custom_zzz",
        "href": "\/v1sdktesting\/meta.v1\/Custom_zzz"
      }
    },
    "Story.Custom_Tags2": {
      "_type": "AttributeDefinition",
      "Name": "Custom_Tags2",
      "Token": "Story.Custom_Tags2",
      "DisplayName": "AttributeDefinition'Custom_Tags2'Story",
      "AttributeType": "Text",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": false,
      "IsCustom": true,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/Custom_Tags2",
        "tokenref": "PrimaryWorkitem.Custom_Tags2"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Custom_Tags2",
        "tokenref": "Story.Custom_Tags2"
      }
    },
    "Story.Custom_OHExternalID": {
      "_type": "AttributeDefinition",
      "Name": "Custom_OHExternalID",
      "Token": "Story.Custom_OHExternalID",
      "DisplayName": "AttributeDefinition'Custom_OHExternalID'Story",
      "AttributeType": "Text",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": false,
      "IsCustom": true,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/Custom_OHExternalID",
        "tokenref": "PrimaryWorkitem.Custom_OHExternalID"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Custom_OHExternalID",
        "tokenref": "Story.Custom_OHExternalID"
      }
    },
    "Story.Custom_OHLastUpdate": {
      "_type": "AttributeDefinition",
      "Name": "Custom_OHLastUpdate",
      "Token": "Story.Custom_OHLastUpdate",
      "DisplayName": "AttributeDefinition'Custom_OHLastUpdate'Story",
      "AttributeType": "Text",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": false,
      "IsCustom": true,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/Custom_OHLastUpdate",
        "tokenref": "PrimaryWorkitem.Custom_OHLastUpdate"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Custom_OHLastUpdate",
        "tokenref": "Story.Custom_OHLastUpdate"
      }
    },
    "Story.Custom_AcceptanceDate": {
      "_type": "AttributeDefinition",
      "Name": "Custom_AcceptanceDate",
      "Token": "Story.Custom_AcceptanceDate",
      "DisplayName": "AttributeDefinition'Custom_AcceptanceDate'Story",
      "AttributeType": "Date",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": false,
      "IsCustom": true,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/Custom_AcceptanceDate",
        "tokenref": "PrimaryWorkitem.Custom_AcceptanceDate"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Custom_AcceptanceDate",
        "tokenref": "Story.Custom_AcceptanceDate"
      }
    },
    "Story.Custom_Test": {
      "_type": "AttributeDefinition",
      "Name": "Custom_Test",
      "Token": "Story.Custom_Test",
      "DisplayName": "AttributeDefinition'Custom_Test'Story",
      "AttributeType": "Text",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": false,
      "IsCustom": true,
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Custom_Test",
        "tokenref": "Story.Custom_Test"
      }
    },
    "Story.Custom_Testing123": {
      "_type": "AttributeDefinition",
      "Name": "Custom_Testing123",
      "Token": "Story.Custom_Testing123",
      "DisplayName": "AttributeDefinition'Custom_Testing123'Story",
      "AttributeType": "Text",
      "IsReadOnly": false,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": false,
      "IsCustom": true,
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Custom_Testing123",
        "tokenref": "Story.Custom_Testing123"
      }
    },
    "Story.CanUpdate": {
      "_type": "AttributeDefinition",
      "Name": "CanUpdate",
      "Token": "Story.CanUpdate",
      "DisplayName": "AttributeDefinition'CanUpdate'Story",
      "AttributeType": "Boolean",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/CanUpdate",
        "tokenref": "Story.CanUpdate"
      }
    },
    "Story.IsReadOnly": {
      "_type": "AttributeDefinition",
      "Name": "IsReadOnly",
      "Token": "Story.IsReadOnly",
      "DisplayName": "AttributeDefinition'IsReadOnly'Story",
      "AttributeType": "Boolean",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/IsReadOnly",
        "tokenref": "Workitem.IsReadOnly"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/IsReadOnly",
        "tokenref": "Story.IsReadOnly"
      }
    },
    "Story.IsDeletable": {
      "_type": "AttributeDefinition",
      "Name": "IsDeletable",
      "Token": "Story.IsDeletable",
      "DisplayName": "AttributeDefinition'IsDeletable'Story",
      "AttributeType": "Boolean",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/IsDeletable",
        "tokenref": "Workitem.IsDeletable"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/IsDeletable",
        "tokenref": "Story.IsDeletable"
      }
    },
    "Story.IsDeleted": {
      "_type": "AttributeDefinition",
      "Name": "IsDeleted",
      "Token": "Story.IsDeleted",
      "DisplayName": "AttributeDefinition'IsDeleted'Story",
      "AttributeType": "Boolean",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/BaseAsset\/IsDeleted",
        "tokenref": "BaseAsset.IsDeleted"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/IsDeleted",
        "tokenref": "Story.IsDeleted"
      }
    },
    "Story.IsUndeletable": {
      "_type": "AttributeDefinition",
      "Name": "IsUndeletable",
      "Token": "Story.IsUndeletable",
      "DisplayName": "AttributeDefinition'IsUndeletable'Story",
      "AttributeType": "Boolean",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/BaseAsset\/IsUndeletable",
        "tokenref": "BaseAsset.IsUndeletable"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/IsUndeletable",
        "tokenref": "Story.IsUndeletable"
      }
    },
    "Story.IsInactive": {
      "_type": "AttributeDefinition",
      "Name": "IsInactive",
      "Token": "Story.IsInactive",
      "DisplayName": "AttributeDefinition'IsInactive'Story",
      "AttributeType": "Boolean",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/BaseAsset\/IsInactive",
        "tokenref": "BaseAsset.IsInactive"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/IsInactive",
        "tokenref": "Story.IsInactive"
      }
    },
    "Story.IsClosed": {
      "_type": "AttributeDefinition",
      "Name": "IsClosed",
      "Token": "Story.IsClosed",
      "DisplayName": "AttributeDefinition'IsClosed'Story",
      "AttributeType": "Boolean",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/BaseAsset\/IsClosed",
        "tokenref": "BaseAsset.IsClosed"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/IsClosed",
        "tokenref": "Story.IsClosed"
      }
    },
    "Story.IsDead": {
      "_type": "AttributeDefinition",
      "Name": "IsDead",
      "Token": "Story.IsDead",
      "DisplayName": "AttributeDefinition'IsDead'Story",
      "AttributeType": "Boolean",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/BaseAsset\/IsDead",
        "tokenref": "BaseAsset.IsDead"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/IsDead",
        "tokenref": "Story.IsDead"
      }
    },
    "Story.FakeAssetState": {
      "_type": "AttributeDefinition",
      "Name": "FakeAssetState",
      "Token": "Story.FakeAssetState",
      "DisplayName": "AttributeDefinition'FakeAssetState'Story",
      "AttributeType": "State",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/BaseAsset\/FakeAssetState",
        "tokenref": "BaseAsset.FakeAssetState"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/FakeAssetState",
        "tokenref": "Story.FakeAssetState"
      }
    },
    "Story.MyLastChangeMoment": {
      "_type": "AttributeDefinition",
      "Name": "MyLastChangeMoment",
      "Token": "Story.MyLastChangeMoment",
      "DisplayName": "AttributeDefinition'MyLastChangeMoment'Story",
      "AttributeType": "Opaque",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/BaseAsset\/MyLastChangeMoment",
        "tokenref": "BaseAsset.MyLastChangeMoment"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/MyLastChangeMoment",
        "tokenref": "Story.MyLastChangeMoment"
      }
    },
    "Story.IsCompleted": {
      "_type": "AttributeDefinition",
      "Name": "IsCompleted",
      "Token": "Story.IsCompleted",
      "DisplayName": "AttributeDefinition'IsCompleted'Story",
      "AttributeType": "Boolean",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/IsCompleted",
        "tokenref": "Workitem.IsCompleted"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/IsCompleted",
        "tokenref": "Story.IsCompleted"
      }
    },
    "Story.EstimatedDone": {
      "_type": "AttributeDefinition",
      "Name": "EstimatedDone",
      "Token": "Story.EstimatedDone",
      "DisplayName": "AttributeDefinition'EstimatedDone'Story",
      "AttributeType": "Numeric",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/EstimatedDone",
        "tokenref": "Workitem.EstimatedDone"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/EstimatedDone",
        "tokenref": "Story.EstimatedDone"
      }
    },
    "Story.Inactive": {
      "_type": "AttributeDefinition",
      "Name": "Inactive",
      "Token": "Story.Inactive",
      "DisplayName": "AttributeDefinition'Inactive'Story",
      "AttributeType": "Boolean",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/Inactive",
        "tokenref": "Workitem.Inactive"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Inactive",
        "tokenref": "Story.Inactive"
      }
    },
    "Story.AllocatedToDo": {
      "_type": "AttributeDefinition",
      "Name": "AllocatedToDo",
      "Token": "Story.AllocatedToDo",
      "DisplayName": "AttributeDefinition'AllocatedToDo'Story",
      "AttributeType": "Numeric",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/AllocatedToDo",
        "tokenref": "Workitem.AllocatedToDo"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/AllocatedToDo",
        "tokenref": "Story.AllocatedToDo"
      }
    },
    "Story.AllocatedDetailEstimate": {
      "_type": "AttributeDefinition",
      "Name": "AllocatedDetailEstimate",
      "Token": "Story.AllocatedDetailEstimate",
      "DisplayName": "AttributeDefinition'AllocatedDetailEstimate'Story",
      "AttributeType": "Numeric",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/AllocatedDetailEstimate",
        "tokenref": "Workitem.AllocatedDetailEstimate"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/AllocatedDetailEstimate",
        "tokenref": "Story.AllocatedDetailEstimate"
      }
    },
    "Story.EstimatedAllocatedDone": {
      "_type": "AttributeDefinition",
      "Name": "EstimatedAllocatedDone",
      "Token": "Story.EstimatedAllocatedDone",
      "DisplayName": "AttributeDefinition'EstimatedAllocatedDone'Story",
      "AttributeType": "Numeric",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/EstimatedAllocatedDone",
        "tokenref": "Workitem.EstimatedAllocatedDone"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/EstimatedAllocatedDone",
        "tokenref": "Story.EstimatedAllocatedDone"
      }
    },
    "Story.CompleteEstimate": {
      "_type": "AttributeDefinition",
      "Name": "CompleteEstimate",
      "Token": "Story.CompleteEstimate",
      "DisplayName": "AttributeDefinition'CompleteEstimate'Story",
      "AttributeType": "Numeric",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/CompleteEstimate",
        "tokenref": "PrimaryWorkitem.CompleteEstimate"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/CompleteEstimate",
        "tokenref": "Story.CompleteEstimate"
      }
    },
    "Story.IncompleteEstimate": {
      "_type": "AttributeDefinition",
      "Name": "IncompleteEstimate",
      "Token": "Story.IncompleteEstimate",
      "DisplayName": "AttributeDefinition'IncompleteEstimate'Story",
      "AttributeType": "Numeric",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/IncompleteEstimate",
        "tokenref": "PrimaryWorkitem.IncompleteEstimate"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/IncompleteEstimate",
        "tokenref": "Story.IncompleteEstimate"
      }
    },
    "Story.OpenEstimate": {
      "_type": "AttributeDefinition",
      "Name": "OpenEstimate",
      "Token": "Story.OpenEstimate",
      "DisplayName": "AttributeDefinition'OpenEstimate'Story",
      "AttributeType": "Numeric",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/OpenEstimate",
        "tokenref": "PrimaryWorkitem.OpenEstimate"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/OpenEstimate",
        "tokenref": "Story.OpenEstimate"
      }
    },
    "Story.ClosedEstimate": {
      "_type": "AttributeDefinition",
      "Name": "ClosedEstimate",
      "Token": "Story.ClosedEstimate",
      "DisplayName": "AttributeDefinition'ClosedEstimate'Story",
      "AttributeType": "Numeric",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/ClosedEstimate",
        "tokenref": "PrimaryWorkitem.ClosedEstimate"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/ClosedEstimate",
        "tokenref": "Story.ClosedEstimate"
      }
    },
    "Story.Jeopardy": {
      "_type": "AttributeDefinition",
      "Name": "Jeopardy",
      "Token": "Story.Jeopardy",
      "DisplayName": "AttributeDefinition'Jeopardy'Story",
      "AttributeType": "Numeric",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/Jeopardy",
        "tokenref": "Story.Jeopardy"
      }
    },
    "Story.WasAnEpic": {
      "_type": "AttributeDefinition",
      "Name": "WasAnEpic",
      "Token": "Story.WasAnEpic",
      "DisplayName": "AttributeDefinition'WasAnEpic'Story",
      "AttributeType": "Boolean",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/WasAnEpic",
        "tokenref": "Story.WasAnEpic"
      }
    },
    "Story.CanConvertToDefect": {
      "_type": "AttributeDefinition",
      "Name": "CanConvertToDefect",
      "Token": "Story.CanConvertToDefect",
      "DisplayName": "AttributeDefinition'CanConvertToDefect'Story",
      "AttributeType": "Boolean",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/CanConvertToDefect",
        "tokenref": "Story.CanConvertToDefect"
      }
    },
    "Story.CheckSplit": {
      "_type": "AttributeDefinition",
      "Name": "CheckSplit",
      "Token": "Story.CheckSplit",
      "DisplayName": "AttributeDefinition'CheckSplit'Story",
      "AttributeType": "Boolean",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/CheckSplit",
        "tokenref": "PrimaryWorkitem.CheckSplit"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/CheckSplit",
        "tokenref": "Story.CheckSplit"
      }
    },
    "Story.CheckQuickSignup": {
      "_type": "AttributeDefinition",
      "Name": "CheckQuickSignup",
      "Token": "Story.CheckQuickSignup",
      "DisplayName": "AttributeDefinition'CheckQuickSignup'Story",
      "AttributeType": "Boolean",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/CheckQuickSignup",
        "tokenref": "Story.CheckQuickSignup"
      }
    },
    "Story.CheckQuickClose": {
      "_type": "AttributeDefinition",
      "Name": "CheckQuickClose",
      "Token": "Story.CheckQuickClose",
      "DisplayName": "AttributeDefinition'CheckQuickClose'Story",
      "AttributeType": "Boolean",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/CheckQuickClose",
        "tokenref": "Story.CheckQuickClose"
      }
    },
    "Story.CheckMakeTemplate": {
      "_type": "AttributeDefinition",
      "Name": "CheckMakeTemplate",
      "Token": "Story.CheckMakeTemplate",
      "DisplayName": "AttributeDefinition'CheckMakeTemplate'Story",
      "AttributeType": "Boolean",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/CheckMakeTemplate",
        "tokenref": "Story.CheckMakeTemplate"
      }
    },
    "Story.CheckCopy": {
      "_type": "AttributeDefinition",
      "Name": "CheckCopy",
      "Token": "Story.CheckCopy",
      "DisplayName": "AttributeDefinition'CheckCopy'Story",
      "AttributeType": "Boolean",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/CheckCopy",
        "tokenref": "Story.CheckCopy"
      }
    },
    "Story.CheckBreakdown": {
      "_type": "AttributeDefinition",
      "Name": "CheckBreakdown",
      "Token": "Story.CheckBreakdown",
      "DisplayName": "AttributeDefinition'CheckBreakdown'Story",
      "AttributeType": "Boolean",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/CheckBreakdown",
        "tokenref": "Story.CheckBreakdown"
      }
    },
    "Story.CheckShallowCopy": {
      "_type": "AttributeDefinition",
      "Name": "CheckShallowCopy",
      "Token": "Story.CheckShallowCopy",
      "DisplayName": "AttributeDefinition'CheckShallowCopy'Story",
      "AttributeType": "Boolean",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/CheckShallowCopy",
        "tokenref": "Story.CheckShallowCopy"
      }
    },
    "Story.CheckDeepCopy": {
      "_type": "AttributeDefinition",
      "Name": "CheckDeepCopy",
      "Token": "Story.CheckDeepCopy",
      "DisplayName": "AttributeDefinition'CheckDeepCopy'Story",
      "AttributeType": "Boolean",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/CheckDeepCopy",
        "tokenref": "Story.CheckDeepCopy"
      }
    },
    "Story.CheckReactivate": {
      "_type": "AttributeDefinition",
      "Name": "CheckReactivate",
      "Token": "Story.CheckReactivate",
      "DisplayName": "AttributeDefinition'CheckReactivate'Story",
      "AttributeType": "Boolean",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/PrimaryWorkitem\/CheckReactivate",
        "tokenref": "PrimaryWorkitem.CheckReactivate"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/CheckReactivate",
        "tokenref": "Story.CheckReactivate"
      }
    },
    "Story.CheckInactivate": {
      "_type": "AttributeDefinition",
      "Name": "CheckInactivate",
      "Token": "Story.CheckInactivate",
      "DisplayName": "AttributeDefinition'CheckInactivate'Story",
      "AttributeType": "Boolean",
      "IsReadOnly": true,
      "IsRequired": false,
      "IsMultivalue": false,
      "IsCanned": true,
      "IsCustom": false,
      "Base": {
        "href": "\/v1sdktesting\/meta.v1\/Workitem\/CheckInactivate",
        "tokenref": "Workitem.CheckInactivate"
      },
      "OrderByAttribute": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/CheckInactivate",
        "tokenref": "Story.CheckInactivate"
      }
    }
  },
  "Operations": {
    "Story.Delete": {
      "_type": "Operation",
      "Name": "Delete",
      "Validator": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/IsDeletable",
        "tokenref": "Story.IsDeletable"
      }
    },
    "Story.Undelete": {
      "_type": "Operation",
      "Name": "Undelete",
      "Validator": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/IsUndeletable",
        "tokenref": "Story.IsUndeletable"
      }
    },
    "Story.Split": {
      "_type": "Operation",
      "Name": "Split",
      "Validator": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/CheckSplit",
        "tokenref": "Story.CheckSplit"
      }
    },
    "Story.Breakdown": {
      "_type": "Operation",
      "Name": "Breakdown",
      "Validator": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/CheckBreakdown",
        "tokenref": "Story.CheckBreakdown"
      }
    },
    "Story.ConvertToDefect": {
      "_type": "Operation",
      "Name": "ConvertToDefect",
      "Validator": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/CanConvertToDefect",
        "tokenref": "Story.CanConvertToDefect"
      }
    },
    "Story.Copy": {
      "_type": "Operation",
      "Name": "Copy",
      "Validator": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/CheckCopy",
        "tokenref": "Story.CheckCopy"
      }
    },
    "Story.DeepCopy": {
      "_type": "Operation",
      "Name": "DeepCopy",
      "Validator": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/CheckDeepCopy",
        "tokenref": "Story.CheckDeepCopy"
      }
    },
    "Story.Inactivate": {
      "_type": "Operation",
      "Name": "Inactivate",
      "Validator": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/CheckInactivate",
        "tokenref": "Story.CheckInactivate"
      }
    },
    "Story.MakeTemplate": {
      "_type": "Operation",
      "Name": "MakeTemplate",
      "Validator": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/CheckMakeTemplate",
        "tokenref": "Story.CheckMakeTemplate"
      }
    },
    "Story.QuickClose": {
      "_type": "Operation",
      "Name": "QuickClose",
      "Validator": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/CheckQuickClose",
        "tokenref": "Story.CheckQuickClose"
      }
    },
    "Story.QuickSignup": {
      "_type": "Operation",
      "Name": "QuickSignup",
      "Validator": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/CheckQuickSignup",
        "tokenref": "Story.CheckQuickSignup"
      }
    },
    "Story.Reactivate": {
      "_type": "Operation",
      "Name": "Reactivate",
      "Validator": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/CheckReactivate",
        "tokenref": "Story.CheckReactivate"
      }
    },
    "Story.ShallowCopy": {
      "_type": "Operation",
      "Name": "ShallowCopy",
      "Validator": {
        "href": "\/v1sdktesting\/meta.v1\/Story\/CheckShallowCopy",
        "tokenref": "Story.CheckShallowCopy"
      }
    }
  }
}
```

