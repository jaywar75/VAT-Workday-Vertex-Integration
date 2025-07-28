# Domestic EU Sale Configuration

## Overview
Configure Vertex tax decision engine for handling VAT on domestic sales within the same EU country. This scenario applies when both the seller and buyer are located in the same EU member state.

## Configuration Steps

### 1. Workday Configuration

#### Tax Categories Setup
```
Navigation: Workday → Tax → Setup → Tax Categories
```

1. Create or verify domestic sales tax category
2. Configure standard VAT rate for the country
3. Set up reduced VAT rates (if applicable)
4. Configure exempt transaction types

#### Business Process Configuration
```
Navigation: Workday → Tax → Setup → Business Process → Calculate Tax
```

1. Enable automatic tax calculation for domestic sales
2. Configure tax determination rules
3. Set up approval workflows for tax exceptions
4. Configure tax posting rules

### 2. Vertex Configuration

#### Tax Rules Setup
```
Vertex Central → Tax Rules → Country Rules → [EU Country]
```

1. **Standard Rate Configuration**
   - Set standard VAT rate (e.g., 21% for Belgium, 19% for Germany)
   - Configure effective dates
   - Set up rate change history

2. **Reduced Rate Configuration**
   - Configure reduced rates for specific products/services
   - Set up food and beverage rates
   - Configure essential goods rates

3. **Exemption Rules**
   - Set up B2B exemptions with valid VAT numbers
   - Configure export exemptions
   - Set up intra-community supply rules

#### Product Classification
```
Vertex Central → Product Classification → Tax Categories
```

1. Map Workday product codes to Vertex tax categories
2. Configure product-specific tax rates
3. Set up service tax classifications
4. Configure digital goods tax rules

### 3. Integration Configuration

#### Tax Determination Flow
```
Workday Transaction → Vertex Tax Engine → Tax Calculation → Workday Posting
```

1. **Request Configuration**
   - Customer location validation
   - Product tax classification
   - Transaction type determination
   - Tax exemption verification

2. **Response Processing**
   - Tax amount calculation
   - Tax rate application
   - Audit trail creation
   - Error handling

### 4. Tax Posting Configuration

#### General Ledger Setup
```
Workday → Accounting → Setup → Worktags → Tax Codes
```

1. Create domestic VAT payable accounts
2. Set up VAT receivable accounts (for returns)
3. Configure tax reporting accounts
4. Set up reconciliation accounts

#### Posting Rules
```
Workday → Accounting → Setup → Posting Rules → Tax Posting
```

1. Configure automatic posting for calculated taxes
2. Set up manual posting override rules
3. Configure tax adjustment posting
4. Set up period-end accrual rules

## Example Configuration

### Sample Transaction Flow
```
Sale Invoice: €1,000.00
VAT Rate: 21% (Belgium standard rate)
VAT Amount: €210.00
Total Invoice: €1,210.00

Workday Posting:
- Debit: Accounts Receivable €1,210.00
- Credit: Revenue €1,000.00
- Credit: VAT Payable €210.00
```

### Tax Code Configuration
```
Tax Code: DOM-VAT-STD
Description: Domestic VAT - Standard Rate
Rate: 21.00%
Effective Date: 01/01/2023
GL Account: 2410 - VAT Payable
```

## Testing and Validation

### Test Scenarios
1. **Standard Rate Transaction**
   - Create test invoice with standard products
   - Verify correct VAT calculation
   - Confirm proper GL posting

2. **Reduced Rate Transaction**
   - Test with reduced rate products
   - Verify rate application
   - Confirm tax reporting

3. **Exempt Transaction**
   - Test B2B exempt sales
   - Verify exemption logic
   - Confirm audit trail

### Validation Checklist
- [ ] Tax rates match government regulations
- [ ] Product classifications are accurate
- [ ] GL postings are correct
- [ ] Audit trails are complete
- [ ] Exception handling works properly

## Troubleshooting

### Common Issues
1. **Incorrect Tax Rate**
   - Verify Vertex rate configuration
   - Check effective date settings
   - Confirm product classification

2. **Missing Tax Calculation**
   - Check integration connectivity
   - Verify customer location data
   - Confirm tax category assignment

3. **Posting Errors**
   - Verify GL account setup
   - Check posting rule configuration
   - Confirm tax code mapping

## Compliance Considerations

### VAT Reporting
- Ensure all domestic sales are properly classified
- Verify VAT return calculations
- Maintain detailed transaction records
- Configure automated reporting schedules

### Audit Requirements
- Maintain complete audit trails
- Document all tax configurations
- Provide transaction details for auditors
- Ensure data retention compliance

## Next Steps
After completing domestic EU sale configuration, proceed to [Cross-border EU Sale Configuration](crossborder-eu-sale.md).
