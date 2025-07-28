# Cross-border EU Purchase Configuration

## Overview
Configure Vertex tax decision engine for handling VAT on cross-border purchases from other EU member states. This scenario covers intra-community acquisitions and the reverse charge mechanism from the buyer's perspective.

## Configuration Steps

### 1. Workday Configuration

#### Supplier Setup
```
Navigation: Workday → Procurement → Suppliers → Supplier Data
```

1. **VAT Number Management**
   - Configure EU VAT number validation for suppliers
   - Set up VIES integration for supplier validation
   - Configure invalid VAT number handling
   - Set up supplier registration alerts

2. **Supplier Location Setup**
   - Configure accurate EU country codes
   - Set up supplier address validation
   - Configure delivery location tracking
   - Set up terms and conditions mapping

#### Tax Categories for Cross-border Purchases
```
Navigation: Workday → Tax → Setup → Tax Categories
```

1. **Intra-Community Acquisition Configuration**
   - Create reverse charge tax category
   - Configure acquisition VAT rates
   - Set up simultaneous input VAT deduction
   - Configure non-deductible VAT handling

2. **Import VAT Configuration**
   - Set up import VAT deferment
   - Configure customs duty integration
   - Set up C79 certificate processing
   - Configure import VAT recovery

### 2. Vertex Configuration

#### Cross-border Purchase Tax Rules
```
Vertex Central → Tax Rules → Cross-border Rules → EU Purchases
```

1. **Intra-Community Acquisition Rules**
   - Configure reverse charge conditions
   - Set up valid VAT number requirements
   - Configure acquisition VAT rates
   - Set up input VAT deduction rules

2. **Use and Enjoy Rules**
   - Configure place of supply determination
   - Set up use and enjoy criteria
   - Configure country-specific variations
   - Set up mixed-use allocation rules

3. **Recoverability Rules**
   - Configure input VAT recovery rates
   - Set up partial recovery calculations
   - Configure non-deductible VAT treatment
   - Set up business/private use allocation

#### Product/Service Classification
```
Vertex Central → Product Classification → Purchase Rules
```

1. **Goods Classification**
   - Configure physical goods acquisition rules
   - Set up installation and assembly rules
   - Configure warranty and support rules
   - Set up capital goods rules

2. **Services Classification**
   - Configure service acquisition rules
   - Set up consultancy service rules
   - Configure digital service rules
   - Set up professional service rules

### 3. Integration Configuration

#### Cross-border Purchase Tax Determination
```
Workday Purchase → Vertex Validation → Tax Calculation → VAT Posting
```

1. **Supplier Validation Process**
   - VAT number format validation
   - VIES real-time validation
   - Supplier registration verification
   - Business classification confirmation

2. **Transaction Classification**
   - Goods vs services determination
   - Place of supply determination
   - Use and enjoy assessment
   - Recovery rate application

3. **Tax Calculation Logic**
   - Reverse charge application
   - Input VAT calculation
   - Recovery rate application
   - Non-deductible VAT calculation

### 4. GL Posting Configuration

#### Chart of Accounts Setup
```
Workday → Accounting → Setup → Chart of Accounts
```

1. **Acquisition VAT Accounts**
   - Create acquisition VAT payable accounts
   - Set up input VAT receivable accounts
   - Configure non-deductible VAT expense accounts
   - Set up VAT control accounts

2. **Recovery Accounts**
   - Configure partial recovery accounts
   - Set up full recovery accounts
   - Configure non-recovery expense accounts
   - Set up adjustment accounts

#### Posting Rules Configuration
```
Workday → Accounting → Setup → Posting Rules → Purchase VAT
```

1. **Simultaneous Posting Rules**
   - Configure acquisition VAT posting
   - Set up input VAT posting
   - Configure net expense posting
   - Set up control account reconciliation

## Example Configurations

### Sample Cross-border Purchase (Belgium from Germany)
```
Supplier: German Company (DE123456789)
Buyer: Belgian Company (BE987654321)
Product: Manufacturing Equipment
Value: €50,000.00

Tax Treatment:
- German VAT: 0% (Intra-community supply)
- Belgian Acquisition VAT: 21% (€10,500.00)
- Belgian Input VAT: 21% (€10,500.00) - Recoverable
- Net VAT Impact: €0.00
```

### Vertex Tax Rules Configuration
```
Rule Name: EU_CROSS_BORDER_PURCHASE
Conditions:
- Supplier Country ≠ Buyer Country
- Valid EU VAT Number Present
- Goods/Services Acquisition
- B2B Transaction

Tax Result:
- Acquisition VAT Rate: 21.00%
- Input VAT Rate: 21.00%
- Recovery Rate: 100.00%
- Net VAT: 0.00%
```

### GL Posting Example
```
Purchase Invoice: €50,000.00
Acquisition VAT: €10,500.00
Input VAT: €10,500.00

GL Posting:
- Debit: Equipment Asset €50,000.00
- Debit: Input VAT Receivable €10,500.00
- Credit: Acquisition VAT Payable €10,500.00
- Credit: Accounts Payable €50,000.00
```

## Recoverability Configuration

### Full Recovery Scenario
```
Business Use: 100%
Recovery Rate: 100%
Input VAT: Fully deductible
GL Impact: No net VAT cost
```

### Partial Recovery Scenario
```
Business Use: 80%
Recovery Rate: 80%
Recoverable VAT: €8,400.00 (80% of €10,500.00)
Non-recoverable VAT: €2,100.00 (20% of €10,500.00)
GL Impact: €2,100.00 additional cost
```

### Non-Recovery Scenario
```
Business Use: 0% (Personal use)
Recovery Rate: 0%
Recoverable VAT: €0.00
Non-recoverable VAT: €10,500.00
GL Impact: €10,500.00 additional cost
```

## Testing and Validation

### Test Scenarios

1. **Standard Cross-border Purchase**
   - Verify supplier VAT number validation
   - Confirm reverse charge application
   - Check simultaneous VAT posting
   - Validate recovery calculation

2. **Partial Recovery Test**
   - Configure mixed-use scenario
   - Test recovery rate application
   - Verify expense allocation
   - Check GL posting accuracy

3. **Service Acquisition Test**
   - Test place of supply rules
   - Verify use and enjoy criteria
   - Check service classification
   - Validate tax calculation

### Validation Checklist
- [ ] Supplier VAT validation working
- [ ] Reverse charge correctly applied
- [ ] Input VAT properly calculated
- [ ] Recovery rates accurate
- [ ] GL postings balanced
- [ ] Control accounts reconciled

## Troubleshooting

### Common Issues

1. **Supplier VAT Number Issues**
   - Check VIES service connectivity
   - Verify VAT number format
   - Confirm supplier registration
   - Review validation timeout settings

2. **Incorrect Recovery Rates**
   - Verify business use percentages
   - Check recovery rate configuration
   - Confirm product classification
   - Review mixed-use allocation

3. **GL Posting Errors**
   - Check account mapping
   - Verify posting rule configuration
   - Confirm tax code setup
   - Review control account setup

## Compliance Considerations

### VAT Return Reporting
- Configure acquisition VAT reporting
- Set up input VAT claim reporting
- Maintain transaction documentation
- Ensure audit trail completeness

### Documentation Requirements
- Maintain supplier invoices
- Keep VAT number validation records
- Document business use evidence
- Maintain recovery rate justification

### Audit Preparation
- Prepare acquisition VAT schedules
- Document recovery calculations
- Maintain control account reconciliations
- Prepare transaction listings

## Advanced Configuration

### Mixed-Use Allocation
```
Example: Office building purchase
Total Cost: €1,000,000.00
Acquisition VAT: €210,000.00

Business Use: 60%
Personal Use: 40%

Recoverable VAT: €126,000.00 (60%)
Non-recoverable VAT: €84,000.00 (40%)
```

### Capital Goods Scheme
```
Configuration for capital goods over threshold:
- Track recovery adjustments
- Configure annual reviews
- Set up adjustment calculations
- Maintain adjustment records
```

### Import VAT Deferment
```
UK-specific configuration:
- Set up deferment account
- Configure C79 certificate processing
- Set up monthly payment schedules
- Configure duty and VAT allocation
```

## Special Scenarios

### Triangular Transactions
```
Scenario: Belgian company facilitating German-French transaction
Configuration:
- Facilitator rules
- Country-specific obligations
- Documentation requirements
- Audit trail maintenance
```

### Distance Selling Purchases
```
Scenario: Purchasing from distance seller
Configuration:
- Threshold monitoring
- Rate determination
- Registration verification
- Compliance validation
```

## Next Steps
After completing cross-border EU purchase configuration, proceed to [Local Purchase VAT Configuration](local-purchase-vat.md).
