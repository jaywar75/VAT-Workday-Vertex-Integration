# Configuration Examples

## Domestic EU Sale Examples

### Example 1: Standard Belgian Sale
```json
{
  "transaction": {
    "type": "SALE",
    "date": "2025-07-17",
    "seller": {
      "country": "BE",
      "vatNumber": "BE123456789",
      "name": "Belgian Company BVBA"
    },
    "customer": {
      "country": "BE",
      "vatNumber": "BE987654321",
      "name": "Belgian Customer SA",
      "type": "BUSINESS"
    },
    "lineItems": [
      {
        "productCode": "LAPTOP001",
        "description": "Business Laptop",
        "quantity": 1,
        "unitPrice": 1000.00,
        "taxCategory": "STANDARD"
      }
    ]
  },
  "taxCalculation": {
    "jurisdiction": "BE",
    "rate": 0.21,
    "taxAmount": 210.00,
    "totalAmount": 1210.00,
    "exemptionCode": null
  }
}
```

### Example 2: German Reduced Rate Sale
```json
{
  "transaction": {
    "type": "SALE",
    "date": "2025-07-17",
    "seller": {
      "country": "DE",
      "vatNumber": "DE123456789",
      "name": "German Company GmbH"
    },
    "customer": {
      "country": "DE",
      "vatNumber": "DE987654321",
      "name": "German Customer AG",
      "type": "BUSINESS"
    },
    "lineItems": [
      {
        "productCode": "BOOK001",
        "description": "Technical Manual",
        "quantity": 5,
        "unitPrice": 50.00,
        "taxCategory": "REDUCED"
      }
    ]
  },
  "taxCalculation": {
    "jurisdiction": "DE",
    "rate": 0.07,
    "taxAmount": 17.50,
    "totalAmount": 267.50,
    "exemptionCode": null
  }
}
```

## Cross-border EU Sale Examples

### Example 3: Intra-Community Supply (Belgium to France)
```json
{
  "transaction": {
    "type": "SALE",
    "date": "2025-07-17",
    "seller": {
      "country": "BE",
      "vatNumber": "BE123456789",
      "name": "Belgian Exporter BVBA"
    },
    "customer": {
      "country": "FR",
      "vatNumber": "FR987654321",
      "name": "French Importer SARL",
      "type": "BUSINESS"
    },
    "lineItems": [
      {
        "productCode": "MACHINE001",
        "description": "Industrial Equipment",
        "quantity": 1,
        "unitPrice": 50000.00,
        "taxCategory": "INTRACOMMUNITY"
      }
    ]
  },
  "taxCalculation": {
    "jurisdiction": "BE",
    "rate": 0.00,
    "taxAmount": 0.00,
    "totalAmount": 50000.00,
    "exemptionCode": "INTRACOMMUNITY_SUPPLY",
    "reverseCharge": true
  }
}
```

### Example 4: Distance Selling (Netherlands to Belgium)
```json
{
  "transaction": {
    "type": "SALE",
    "date": "2025-07-17",
    "seller": {
      "country": "NL",
      "vatNumber": "NL123456789B01",
      "name": "Dutch Online Store BV"
    },
    "customer": {
      "country": "BE",
      "vatNumber": null,
      "name": "Belgian Consumer",
      "type": "CONSUMER"
    },
    "lineItems": [
      {
        "productCode": "ELECTRONICS001",
        "description": "Consumer Electronics",
        "quantity": 1,
        "unitPrice": 500.00,
        "taxCategory": "DISTANCE_SELLING"
      }
    ]
  },
  "taxCalculation": {
    "jurisdiction": "BE",
    "rate": 0.21,
    "taxAmount": 105.00,
    "totalAmount": 605.00,
    "exemptionCode": null,
    "note": "Distance selling threshold exceeded"
  }
}
```

## Cross-border EU Purchase Examples

### Example 5: Intra-Community Acquisition (Germany from Italy)
```json
{
  "transaction": {
    "type": "PURCHASE",
    "date": "2025-07-17",
    "buyer": {
      "country": "DE",
      "vatNumber": "DE123456789",
      "name": "German Buyer GmbH"
    },
    "supplier": {
      "country": "IT",
      "vatNumber": "IT987654321",
      "name": "Italian Supplier SRL",
      "type": "BUSINESS"
    },
    "lineItems": [
      {
        "productCode": "MARBLE001",
        "description": "Marble Tiles",
        "quantity": 100,
        "unitPrice": 25.00,
        "taxCategory": "INTRACOMMUNITY"
      }
    ]
  },
  "taxCalculation": {
    "jurisdiction": "DE",
    "acquisitionVAT": {
      "rate": 0.19,
      "amount": 475.00
    },
    "inputVAT": {
      "rate": 0.19,
      "amount": 475.00,
      "recoverable": true
    },
    "netVATImpact": 0.00,
    "totalAmount": 2500.00
  }
}
```

## Local Purchase Examples

### Example 6: Full Recovery Purchase (Belgium)
```json
{
  "transaction": {
    "type": "PURCHASE",
    "date": "2025-07-17",
    "buyer": {
      "country": "BE",
      "vatNumber": "BE123456789",
      "name": "Belgian Company BVBA"
    },
    "supplier": {
      "country": "BE",
      "vatNumber": "BE987654321",
      "name": "Belgian Supplier SA",
      "type": "BUSINESS"
    },
    "lineItems": [
      {
        "productCode": "OFFICE001",
        "description": "Office Supplies",
        "quantity": 1,
        "unitPrice": 1000.00,
        "businessUse": 100,
        "taxCategory": "STANDARD"
      }
    ]
  },
  "taxCalculation": {
    "jurisdiction": "BE",
    "rate": 0.21,
    "vatAmount": 210.00,
    "recoverableVAT": 210.00,
    "nonRecoverableVAT": 0.00,
    "recoveryRate": 1.00,
    "totalAmount": 1210.00,
    "netCost": 1000.00
  }
}
```

### Example 7: Partial Recovery Purchase (Company Car)
```json
{
  "transaction": {
    "type": "PURCHASE",
    "date": "2025-07-17",
    "buyer": {
      "country": "BE",
      "vatNumber": "BE123456789",
      "name": "Belgian Company BVBA"
    },
    "supplier": {
      "country": "BE",
      "vatNumber": "BE987654321",
      "name": "Car Dealer SA",
      "type": "BUSINESS"
    },
    "lineItems": [
      {
        "productCode": "CAR001",
        "description": "Company Vehicle",
        "quantity": 1,
        "unitPrice": 30000.00,
        "businessUse": 80,
        "taxCategory": "VEHICLE"
      }
    ]
  },
  "taxCalculation": {
    "jurisdiction": "BE",
    "rate": 0.21,
    "vatAmount": 6300.00,
    "recoverableVAT": 5040.00,
    "nonRecoverableVAT": 1260.00,
    "recoveryRate": 0.80,
    "totalAmount": 36300.00,
    "netCost": 31260.00
  }
}
```

### Example 8: Non-Recoverable Purchase (Entertainment)
```json
{
  "transaction": {
    "type": "PURCHASE",
    "date": "2025-07-17",
    "buyer": {
      "country": "BE",
      "vatNumber": "BE123456789",
      "name": "Belgian Company BVBA"
    },
    "supplier": {
      "country": "BE",
      "vatNumber": "BE987654321",
      "name": "Restaurant SA",
      "type": "BUSINESS"
    },
    "lineItems": [
      {
        "productCode": "ENT001",
        "description": "Client Entertainment",
        "quantity": 1,
        "unitPrice": 500.00,
        "businessUse": 0,
        "taxCategory": "ENTERTAINMENT"
      }
    ]
  },
  "taxCalculation": {
    "jurisdiction": "BE",
    "rate": 0.21,
    "vatAmount": 105.00,
    "recoverableVAT": 0.00,
    "nonRecoverableVAT": 105.00,
    "recoveryRate": 0.00,
    "totalAmount": 605.00,
    "netCost": 605.00
  }
}
```

## Special Scenario Examples

### Example 9: Triangular Transaction
```json
{
  "transaction": {
    "type": "TRIANGULAR",
    "date": "2025-07-17",
    "parties": {
      "operator": {
        "country": "BE",
        "vatNumber": "BE123456789",
        "name": "Belgian Operator BVBA"
      },
      "supplier": {
        "country": "DE",
        "vatNumber": "DE987654321",
        "name": "German Supplier GmbH"
      },
      "customer": {
        "country": "FR",
        "vatNumber": "FR456789123",
        "name": "French Customer SARL"
      }
    },
    "lineItems": [
      {
        "productCode": "GOODS001",
        "description": "Traded Goods",
        "quantity": 1,
        "unitPrice": 10000.00,
        "taxCategory": "TRIANGULAR"
      }
    ]
  },
  "taxCalculation": {
    "germanSupply": {
      "rate": 0.00,
      "amount": 0.00,
      "exemptionCode": "TRIANGULAR_SUPPLY"
    },
    "belgianSupply": {
      "rate": 0.00,
      "amount": 0.00,
      "exemptionCode": "TRIANGULAR_SUPPLY"
    },
    "frenchAcquisition": {
      "rate": 0.20,
      "amount": 2000.00,
      "reverseCharge": true
    }
  }
}
```

### Example 10: Digital Services B2B
```json
{
  "transaction": {
    "type": "DIGITAL_SERVICE",
    "date": "2025-07-17",
    "seller": {
      "country": "NL",
      "vatNumber": "NL123456789B01",
      "name": "Dutch Software Company BV"
    },
    "customer": {
      "country": "ES",
      "vatNumber": "ES987654321",
      "name": "Spanish Customer SL",
      "type": "BUSINESS"
    },
    "lineItems": [
      {
        "productCode": "SOFTWARE001",
        "description": "Software License",
        "quantity": 1,
        "unitPrice": 5000.00,
        "taxCategory": "DIGITAL_SERVICE_B2B"
      }
    ]
  },
  "taxCalculation": {
    "jurisdiction": "ES",
    "rate": 0.00,
    "taxAmount": 0.00,
    "totalAmount": 5000.00,
    "exemptionCode": "DIGITAL_SERVICE_B2B",
    "reverseCharge": true,
    "placeOfSupply": "CUSTOMER_LOCATION"
  }
}
```

## Workday Configuration Examples

### Tax Category Configuration
```xml
<!-- Workday Tax Category Configuration -->
<Tax_Category>
  <Tax_Category_ID>DOM-VAT-STD</Tax_Category_ID>
  <Tax_Category_Name>Domestic VAT - Standard Rate</Tax_Category_Name>
  <Tax_Rate>21.00</Tax_Rate>
  <Effective_Date>2023-01-01</Effective_Date>
  <Country_Code>BE</Country_Code>
  <GL_Account>2410</GL_Account>
  <Description>Belgian standard VAT rate</Description>
</Tax_Category>
```

### Customer Configuration
```xml
<!-- Workday Customer Configuration -->
<Customer>
  <Customer_ID>CUST001</Customer_ID>
  <Customer_Name>Belgian Customer SA</Customer_Name>
  <VAT_Number>BE987654321</VAT_Number>
  <Country_Code>BE</Country_Code>
  <Customer_Type>BUSINESS</Customer_Type>
  <Tax_Exemption_Code></Tax_Exemption_Code>
  <Default_Tax_Category>DOM-VAT-STD</Default_Tax_Category>
</Customer>
```

### Product Configuration
```xml
<!-- Workday Product Configuration -->
<Product>
  <Product_ID>LAPTOP001</Product_ID>
  <Product_Name>Business Laptop</Product_Name>
  <Product_Category>ELECTRONICS</Product_Category>
  <Tax_Classification>STANDARD</Tax_Classification>
  <Commodity_Code>8471300000</Commodity_Code>
  <Default_Tax_Category>DOM-VAT-STD</Default_Tax_Category>
</Product>
```

## Vertex Configuration Examples

### Tax Rule Configuration
```json
{
  "ruleId": "EU_DOMESTIC_SALE",
  "ruleName": "EU Domestic Sale Rule",
  "conditions": [
    {
      "field": "SELLER_COUNTRY",
      "operator": "EQUALS",
      "value": "CUSTOMER_COUNTRY"
    },
    {
      "field": "TRANSACTION_TYPE",
      "operator": "EQUALS",
      "value": "SALE"
    },
    {
      "field": "CUSTOMER_TYPE",
      "operator": "EQUALS",
      "value": "BUSINESS"
    }
  ],
  "actions": [
    {
      "type": "APPLY_RATE",
      "rate": "STANDARD_RATE"
    },
    {
      "type": "SET_EXEMPTION",
      "exemption": "NONE"
    }
  ]
}
```

### Recovery Rate Configuration
```json
{
  "recoveryRuleId": "VEHICLE_RECOVERY",
  "ruleName": "Vehicle Purchase Recovery",
  "conditions": [
    {
      "field": "PRODUCT_CATEGORY",
      "operator": "EQUALS",
      "value": "VEHICLE"
    },
    {
      "field": "TRANSACTION_TYPE",
      "operator": "EQUALS",
      "value": "PURCHASE"
    }
  ],
  "recoveryRate": 0.50,
  "description": "50% recovery rate for vehicle purchases"
}
```

## Testing Data Sets

### Standard Test Cases
```json
{
  "testSuite": "EU_VAT_STANDARD",
  "testCases": [
    {
      "testId": "DOM_SALE_001",
      "description": "Domestic sale with standard rate",
      "expectedResult": {
        "rate": 0.21,
        "exempt": false,
        "reverseCharge": false
      }
    },
    {
      "testId": "CROSS_SALE_001",
      "description": "Cross-border B2B sale",
      "expectedResult": {
        "rate": 0.00,
        "exempt": true,
        "reverseCharge": true
      }
    },
    {
      "testId": "PURCHASE_001",
      "description": "Local purchase with full recovery",
      "expectedResult": {
        "rate": 0.21,
        "recoveryRate": 1.00,
        "netVATImpact": 0.00
      }
    }
  ]
}
```

These examples provide comprehensive configuration templates for implementing the various EU VAT scenarios in your Vertex-Workday integration.
