# Techniques

Adds fields to the tender, lot and lot group objects to describe the use of techniques, such as framework agreements, dynamic purchasing systems and electronic auctions.

## Guidance

### Framework agreement's `value` and `period`

The `value` and `period` fields of `FrameworkAgreement` objects should only be used if a data source provides values and periods for both the contract/lot and the framework agreement, like TED XML Schema R2.08. Otherwise:

* If a procurement isn't divided into lots, use the `tender.value` and `tender.contractPeriod` fields.
* If a procurement is divided into lots, use the `value` and `contractPeriod` fields of `Lot` objects.

### Framework agreement's `method`

Here are the possible values for a framework agreement's `method` field, and common synonyms:

- withoutReopeningCompetition: call-offs
- withReopeningCompetition: mini-competitions
- withAndWithoutReopeningCompetition: call-offs and mini-competitions

## Legal context

In the European Union, this extension's fields correspond to [eForms BG-706 (Techniques), BG-557 (Group Framework Maximum Value and BT-271 (Framework Maximum Value)](https://docs.ted.europa.eu/eforms/latest/reference/business-terms/). For correspondences to eForms fields, see [OCDS for eForms](https://standard.open-contracting.org/profiles/eforms/latest/). For correspondences to Tenders Electronic Daily (TED), see [OCDS for the European Union](http://standard.open-contracting.org/profiles/eu/master/en/).

## Examples

### Framework agreement

```json
{
  "tender": {
    "lots": [
      {
        "id": "1",
        "techniques": {
          "hasFrameworkAgreement": true,
          "frameworkAgreement": {
            "minimumParticipants": 2,
            "maximumParticipants": 100,
            "method": "withoutReopeningCompetition",
            "periodRationale": "<A good justification>",
            "buyerCategories": "all hospitals in the Tuscany region",
            "value": {
              "amount": 240000,
              "currency": "EUR"
            },
            "maximumValue": {
              "amount": 300000,
              "currency": "EUR"
            },
            "period": {
              "durationInDays": 730
            },
            "description": "Call offs are estimated to be organized every 3 months, with an average value of 60,000 euros per contract."
          }
        }
      }
    ]
  }
}
```

### Dynamic purchasing system

```json
{
  "tender": {
    "lots": [
      {
        "id": "1",
        "techniques": {
          "hasDynamicPurchasingSystem": true,
          "dynamicPurchasingSystem": {
            "type": "closed",
            "status": "active"
          }
        }
      }
    ]
  }
}
```

### Electronic auction

```json
{
  "tender": {
    "lots": [
      {
        "id": "1",
        "techniques": {
          "hasElectronicAuction": true,
          "electronicAuction": {
            "url": "https://example.com/auction/1",
            "description": "<Any relevant details>"
          }
        }
      }
    ]
  }
}
```

## Issues

Report issues for this extension in the [ocds-extensions repository](https://github.com/open-contracting/ocds-extensions/issues), putting the extension's name in the issue's title.

## Changelog

### 2023-05-30

* Add fields:
  * `LotGroup.techniques`
  * `FrameworkAgreement.maximumValue`

### 2020-10-05

* Add fields:
  * `FrameworkAgreement.minimumParticipants`
  * `FrameworkAgreement.value`
  * `FrameworkAgreement.period`
  * `FrameworkAgreement.description`

### 2020-04-24

* Add `minProperties`, `minItems` and/or `minLength` properties.

This extension was originally discussed as part of the [OCDS for EU profile](https://github.com/open-contracting-extensions/european-union/issues), in [pull requests](https://github.com/open-contracting-extensions/ocds_techniques_extension/pulls?q=is%3Apr+is%3Aclosed) and in <https://github.com/open-contracting/standard/issues/695>.
