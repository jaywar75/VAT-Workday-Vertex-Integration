# Local Purchase VAT Configuration

## Overview
Configure Vertex tax decision engine for handling VAT on local purchases with proper separation of recoverable and irrecoverable VAT portions. This scenario is critical for accurate financial reporting and tax compliance.

## Configuration Steps

### 1. Workday Configuration

#### Business Use Categories
```
Navigation: Workday → Tax → Setup → Business Use Categories
```

1. **Business Use Classification**
   - Create 100% business use category
   - Set up mixed-use categories (e.g., 80% business, 20% personal)
   - Configure non-business use category (0% recovery)
   - Set up activity-based categories

2. **Recovery Rate Configuration**
   - Configure standard recovery rates by category
   - Set up time-based recovery rates
   - Configure product-specific recovery rates
   - Set up location-based recovery rates

#### Asset Categories and Recovery
```
Navigation: Workday → Assets → Setup → Asset Categories
```

1. **Asset Classification**
   - Configure capital goods categories
   - Set up revenue expense categories
   - Configure mixed-use asset categories
   - Set up maintenance and repair categories

2. **Recovery Period Configuration**
   - Set up capital goods scheme periods
   - Configure adjustment review periods
   - Set up depreciation-linked recovery
   - Configure disposal adjustment rules

### 2. Vertex Configuration

#### Recovery Rate Rules
```
Vertex Central → Tax Rules → Recovery Rules → Local Purchase
```

1. **Standard Recovery Rules**
   - Configure 100% recovery for business purchases
   - Set up 0% recovery for personal purchases
   - Configure partial recovery rates
   - Set up activity-based recovery

2. **Product-Specific Recovery**
   - Configure entertainment recovery (often 0% or 50%)
   - Set up vehicle recovery rates
   - Configure meal and accommodation recovery
   - Set up professional service recovery

3. **Time-Based Recovery**
   - Configure initial recovery rates
   - Set up adjustment periods
   - Configure review triggers
   - Set up automatic adjustment calculations

#### GL Account Mapping
```
Vertex Central → GL Integration → Account Mapping
```

1. **Recoverable VAT Accounts**
   - Map to input VAT receivable accounts
   - Configure by business unit
   - Set up by expense category
   - Configure by recovery percentage

2. **Non-Recoverable VAT Accounts**
   - Map to expense accounts
   - Configure by asset category
   - Set up by business unit
   - Configure by recovery percentage

### 3. Integration Configuration

#### Recovery Calculation Logic
```
Workday Purchase → Vertex Recovery Engine → VAT Allocation → GL Posting
```

1. **Purchase Classification**
   - Determine business use percentage
   - Classify expense/asset category
   - Apply recovery rate rules
   - Calculate recoverable/non-recoverable portions

2. **VAT Allocation Process**
   - Calculate total VAT amount
   - Apply recovery rate
   - Allocate to recoverable portion
   - Allocate to non-recoverable portion

3. **GL Posting Logic**
   - Post recoverable VAT to input VAT account
   - Post non-recoverable VAT to expense account
   - Create control account entries
   - Generate audit trail

### 4. Posting Rules Configuration

#### Recoverable VAT Posting
```
Workday → Accounting → Setup → Posting Rules → Input VAT
```

1. **Standard Recovery Posting**
   - Debit input VAT receivable account
   - Credit accounts payable
   - Create VAT control entries
   - Generate recovery tracking

2. **Partial Recovery Posting**
   - Split VAT between recoverable and non-recoverable
   - Post recoverable portion to input VAT account
   - Post non-recoverable portion to expense account
   - Maintain detailed tracking

#### Non-Recoverable VAT Posting
```
Workday → Accounting → Setup → Posting Rules → Non-Recoverable VAT
```

1. **Expense Integration**
   - Add non-recoverable VAT to expense amount
   - Post to appropriate expense account
   - Maintain separate VAT tracking
   - Create detailed reporting

2. **Asset Integration**
   - Add non-recoverable VAT to asset cost
   - Post to appropriate asset account
   - Maintain asset register updates
   - Create depreciation impact

## Example Configurations

### Full Recovery Example
```
Purchase: Office Equipment
Cost: €10,000.00
VAT: €2,100.00 (21%)
Business Use: 100%
Recovery Rate: 100%

GL Posting:
- Debit: Equipment Asset €10,000.00
- Debit: Input VAT Receivable €2,100.00
- Credit: Accounts Payable €12,100.00

Net Cost: €10,000.00
```

### Partial Recovery Example
```
Purchase: Company Car
Cost: €30,000.00
VAT: €6,300.00 (21%)
Business Use: 80%
Recovery Rate: 80%

Recoverable VAT: €5,040.00 (80% of €6,300.00)
Non-recoverable VAT: €1,260.00 (20% of €6,300.00)

GL Posting:
- Debit: Vehicle Asset €31,260.00 (€30,000 + €1,260)
- Debit: Input VAT Receivable €5,040.00
- Credit: Accounts Payable €36,300.00

Net Cost: €31,260.00
```

### Non-Recovery Example
```
Purchase: Client Entertainment
Cost: €500.00
VAT: €105.00 (21%)
Business Use: 0% (Entertainment - non-recoverable)
Recovery Rate: 0%

GL Posting:
- Debit: Entertainment Expense €605.00 (€500 + €105)
- Credit: Accounts Payable €605.00

Net Cost: €605.00
```

## Recovery Rate Configuration

### Standard Recovery Rates by Category
```
Office Supplies: 100%
Equipment: 100%
Professional Services: 100%
Vehicles: 50% (country-specific)
Entertainment: 0%
Meals: 50% (country-specific)
```

### Mixed-Use Allocation
```
Example: Office Building Purchase
Total Cost: €1,000,000.00
VAT: €210,000.00

Usage Allocation:
- Business Use: 70%
- Personal Use: 30%

VAT Allocation:
- Recoverable: €147,000.00 (70%)
- Non-recoverable: €63,000.00 (30%)
```

## Testing and Validation

### Test Scenarios

1. **100% Recovery Test**
   - Create standard business purchase
   - Verify full VAT recovery
   - Check GL posting accuracy
   - Validate reporting

2. **Partial Recovery Test**
   - Create mixed-use purchase
   - Test recovery rate application
   - Verify VAT allocation
   - Check expense integration

3. **Zero Recovery Test**
   - Create non-recoverable purchase
   - Verify zero recovery application
   - Check expense integration
   - Validate cost allocation

### Validation Checklist
- [ ] Recovery rates correctly applied
- [ ] VAT properly allocated
- [ ] GL postings balanced
- [ ] Expense amounts accurate
- [ ] Asset costs properly calculated
- [ ] Reporting data complete

## Troubleshooting

### Common Issues

1. **Incorrect Recovery Rates**
   - Check business use classification
   - Verify recovery rate configuration
   - Confirm product category mapping
   - Review country-specific rules

2. **GL Posting Errors**
   - Verify account mapping
   - Check posting rule configuration
   - Confirm VAT code setup
   - Review allocation logic

3. **Expense Allocation Issues**
   - Check non-recoverable VAT calculation
   - Verify expense account mapping
   - Confirm cost center allocation
   - Review project charging

## Compliance Considerations

### VAT Return Reporting
- Configure input VAT claim reporting
- Set up partial recovery reporting
- Maintain detailed transaction records
- Ensure audit trail completeness

### Documentation Requirements
- Maintain business use evidence
- Document recovery rate justification
- Keep allocation method records
- Maintain review and adjustment logs

### Audit Preparation
- Prepare recovery rate schedules
- Document allocation methods
- Maintain supporting evidence
- Prepare variance analysis

## Advanced Configuration

### Capital Goods Scheme
```
For capital goods over threshold (e.g., €50,000):
- Track initial recovery
- Configure annual reviews
- Set up adjustment calculations
- Maintain adjustment records

Example: Building Purchase
Year 1: 70% business use
Year 3: 90% business use
Adjustment: Additional 20% VAT recovery
```

### Time-Based Recovery Changes
```
Example: Office space conversion
Initial: 100% business use
Later: 50% business use (part converted to personal)
Adjustment: Clawback of 50% previously claimed VAT
```

### Sector-Specific Rules
```
Financial Services (partial exemption):
- Calculate recovery percentage
- Apply to all purchases
- Monitor threshold changes
- Adjust recovery rates

Healthcare (mixed supplies):
- Separate exempt and taxable activities
- Calculate business use percentage
- Apply appropriate recovery rates
- Monitor activity changes
```

## Special Scenarios

### Blocked Input VAT
```
Scenario: Purchases related to exempt supplies
Configuration:
- Identify exempt-related purchases
- Apply 0% recovery rate
- Post all VAT to expense
- Maintain separate tracking
```

### Pre-Trading Expenditure
```
Scenario: Purchases before business registration
Configuration:
- Track pre-trading purchases
- Apply appropriate recovery rates
- Configure registration adjustment
- Maintain detailed records
```

### Change of Use
```
Scenario: Asset use changes over time
Configuration:
- Monitor use percentage changes
- Configure adjustment triggers
- Calculate adjustment amounts
- Process adjustment postings
```

## Integration with Other Modules

### Fixed Assets Integration
```
- Link to asset register
- Update asset costs automatically
- Track depreciation impact
- Configure disposal adjustments
```

### Expense Management Integration
```
- Link to expense claims
- Apply recovery rates automatically
- Update expense amounts
- Generate compliance reports
```

### Project Accounting Integration
```
- Allocate VAT to projects
- Apply project-specific recovery rates
- Track project VAT costs
- Generate project reports
```

## Next Steps
After completing local purchase VAT configuration, proceed to [Tax Reporting and Compliance](tax-reporting.md) for comprehensive reporting setup.
