# Cross-border EU Sale Configuration

## Overview
Configure Vertex tax decision engine for handling VAT on cross-border sales between different EU member states. This scenario covers intra-community supplies and the reverse charge mechanism.

## Configuration Steps

### 1. Workday Configuration

#### Customer Setup
```
Navigation: Workday → Revenue → Customers → Customer Data
```

1. **VAT Number Validation**
   - Configure EU VAT number validation
   - Set up VIES integration for real-time validation
   - Configure invalid VAT number handling
   - Set up periodic re-validation

2. **Customer Location Setup**
   - Configure accurate EU country codes
   - Set up customer address validation
   - Configure shipping address tracking
   - Set up delivery terms mapping

#### Tax Categories for Cross-border Sales
```
Navigation: Workday → Tax → Setup → Tax Categories
```

1. **Intra-Community Supply Configuration**
   - Create zero-rated tax category (0% VAT)
   - Configure reverse charge indicators
   - Set up triangular transaction handling
   - Configure distance selling thresholds

2. **Threshold Management**
   - Set up distance selling thresholds per country
   - Configure threshold monitoring
   - Set up automatic threshold breach alerts
   - Configure fallback tax rates

### 2. Vertex Configuration

#### Cross-border Tax Rules
```
Vertex Central → Tax Rules → Cross-border Rules → EU
```

1. **Intra-Community Supply Rules**
   - Configure zero-rate conditions
   - Set up valid VAT number requirements
   - Configure proof of export requirements
   - Set up reverse charge indicators

2. **Distance Selling Configuration**
   - Configure country-specific thresholds
   - Set up threshold monitoring rules
   - Configure automatic rate switching
   - Set up compliance alerts

3. **Triangular Transaction Rules**
   - Configure three-party transaction logic
   - Set up operator/facilitator rules
   - Configure country-specific variations
   - Set up audit trail requirements

#### Product/Service Classification
```
Vertex Central → Product Classification → Cross-border Rules
```

1. **Goods Classification**
   - Configure physical goods rules
   - Set up installation service rules
   - Configure assembly service rules
   - Set up warranty service rules

2. **Digital Services Classification**
   - Configure digital service rules
   - Set up place of supply rules
   - Configure B2B vs B2C determination
   - Set up telecommunications rules

### 3. Integration Configuration

#### Cross-border Tax Determination
```
Workday Transaction → Vertex Validation → Tax Calculation → Compliance Check
```

1. **Customer Validation Process**
   - VAT number format validation
   - VIES real-time validation
   - Customer status verification
   - Business/consumer classification

2. **Transaction Classification**
   - Goods vs services determination
   - Digital service identification
   - Place of supply determination
   - Threshold impact assessment

3. **Tax Calculation Logic**
   - Zero-rate application rules
   - Reverse charge determination
   - Local rate application (if threshold exceeded)
   - Multi-country shipping rules

### 4. Compliance and Reporting Setup

#### EU Sales List (ESL) Configuration
```
Workday → Tax → Reporting → EU Sales List
```

1. **ESL Data Collection**
   - Configure transaction aggregation
   - Set up customer VAT number tracking
   - Configure quarterly reporting periods
   - Set up automatic data validation

2. **ESL Reporting Format**
   - Configure country-specific formats
   - Set up electronic filing formats
   - Configure submission schedules
   - Set up correction procedures

#### Intrastat Configuration
```
Workday → Tax → Reporting → Intrastat
```

1. **Intrastat Data Requirements**
   - Configure commodity codes
   - Set up statistical values
   - Configure transaction nature codes
   - Set up delivery terms mapping

## Example Configurations

### Sample Cross-border Sale (Germany to France)
```
Seller: German Company (DE123456789)
Customer: French Company (FR987654321)
Product: Industrial Equipment
Value: €10,000.00

Tax Treatment:
- German VAT: 0% (Intra-community supply)
- French VAT: Reverse charge (Customer pays 20%)
- ESL Reporting: Required in Germany
- Intrastat: Required if above threshold
```

### Vertex Tax Rules Configuration
```
Rule Name: EU_CROSS_BORDER_B2B
Conditions:
- Customer Country ≠ Seller Country
- Valid EU VAT Number Present
- Goods Transaction
- B2B Transaction

Tax Result:
- Rate: 0.00%
- Reason Code: INTRA_COMMUNITY_SUPPLY
- Reverse Charge: True
- ESL Reportable: True
```

### Distance Selling Example (Netherlands to Belgium)
```
Scenario: Online retailer selling to consumers
Threshold: €35,000 annually to Belgian consumers
Current Sales: €40,000 (threshold exceeded)

Tax Treatment:
- Rate: 21% (Belgian standard rate)
- Place of Supply: Belgium
- Registration Required: Yes
- Local VAT Return: Required
```

## Testing and Validation

### Test Scenarios

1. **Standard Cross-border B2B Sale**
   - Verify VAT number validation
   - Confirm zero-rate application
   - Check ESL data capture
   - Validate reverse charge indicator

2. **Distance Selling Threshold Test**
   - Monitor threshold tracking
   - Test automatic rate switching
   - Verify registration alerts
   - Confirm compliance notifications

3. **Triangular Transaction Test**
   - Verify three-party logic
   - Check operator responsibilities
   - Confirm country-specific rules
   - Validate audit trail

### Validation Checklist
- [ ] VAT number validation working
- [ ] Zero-rate correctly applied
- [ ] ESL data accurately captured
- [ ] Intrastat data complete
- [ ] Threshold monitoring active
- [ ] Compliance alerts functioning

## Troubleshooting

### Common Issues

1. **VAT Number Validation Failures**
   - Check VIES service availability
   - Verify VAT number format
   - Confirm network connectivity
   - Review validation timeout settings

2. **Incorrect Tax Rate Application**
   - Verify customer country mapping
   - Check threshold calculations
   - Confirm product classification
   - Review transaction type logic

3. **ESL Reporting Errors**
   - Verify customer VAT number capture
   - Check transaction aggregation
   - Confirm reporting period setup
   - Review data validation rules

## Compliance Considerations

### VAT Registration Requirements
- Monitor distance selling thresholds
- Track registration obligations
- Maintain compliance calendars
- Configure automated alerts

### Documentation Requirements
- Maintain proof of export documentation
- Keep VAT number validation records
- Document transaction evidence
- Maintain audit trail integrity

### Reporting Obligations
- Configure ESL submission schedules
- Set up Intrastat reporting
- Maintain VAT return accuracy
- Ensure data retention compliance

## Advanced Configuration

### Multi-country Shipping
```
Scenario: German company shipping to French customer via Belgian warehouse
Configuration:
- Origin: Germany
- Destination: France
- Transit: Belgium
- Tax Treatment: Based on final destination
- Documentation: Transit documents required
```

### Digital Services Rules
```
B2B Digital Services:
- Place of Supply: Customer location
- Rate: 0% (reverse charge)
- Evidence: Customer VAT number

B2C Digital Services:
- Place of Supply: Customer location
- Rate: Local rate
- Registration: Required if threshold exceeded
```

## Next Steps
After completing cross-border EU sale configuration, proceed to [Cross-border EU Purchase Configuration](crossborder-eu-purchase.md).
