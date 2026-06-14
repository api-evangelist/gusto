# Gusto GraphQL Schema

This document describes the conceptual GraphQL schema for the Gusto Embedded Payroll API. Gusto provides a REST API; this schema represents the domain model as a GraphQL type system to enable graph-based querying of payroll, HR, and benefits resources.

## Source

- Provider: Gusto
- API: Gusto Embedded Payroll API
- REST Documentation: https://docs.gusto.com/embedded-payroll
- GitHub: https://github.com/Gusto-Inc
- Schema File: gusto-schema.graphql

## Domain Overview

The Gusto API covers these primary domains:

**Company and Locations** — Company is the root resource. Each company has one or more CompanyLocations, Departments, and Signers responsible for document execution.

**Employees and Contractors** — Employees belong to a company and carry address, job, compensation, tax withholding, and payment method records. Contractors are a separate resource type. TerminatedEmployee tracks separation data.

**Payroll** — Payroll runs are scoped to a PayPeriod. Each run produces EmployeePayroll records covering earnings, deductions (garnishments, benefits), and tax liabilities. Pay stubs and checks are generated per employee per payroll.

**Benefits** — CompanyBenefit records configure plan offerings. Employees enroll via benefit coverage elections. Contributions are tracked per company and per employee. BenefitType enumerates supported plan types.

**Time Off** — TimeOffPolicy defines accrual rules. TimeOffBalance reflects current balances. TimeOffAccrual records individual accrual events.

**Banking and Payment** — BankAccount and DirectDeposit records control where employee net pay is delivered. PaymentMethod distinguishes check vs. direct deposit.

**Tax and Compliance** — EmployeeFederalTax and EmployeeStateTax hold withholding elections. TaxRate and TaxLiability track employer tax obligations. StateCode enumerates US state identifiers.

**Compensation Structure** — EarningType categorizes pay (regular, overtime, bonus). FixedCompensation and HourlyCompensation represent compensation records. Bonus is a discrete supplemental pay event.

## Types Summary (65 types)

| Type | Category |
|---|---|
| Company | Company |
| CompanyLocation | Company |
| CompanyBenefit | Benefits |
| CompanyBenefitContribution | Benefits |
| Employee | Employee |
| EmployeeAddress | Employee |
| EmployeeJob | Employee |
| EmployeeCompensation | Employee |
| EmployeeStateTax | Tax |
| EmployeeFederalTax | Tax |
| EmployeePayroll | Payroll |
| Contractor | Contractor |
| TerminatedEmployee | Employee |
| Termination | Employee |
| Payroll | Payroll |
| PayrollPayPeriod | Payroll |
| PayrollDeduction | Payroll |
| EarningsTotal | Payroll |
| TaxLiability | Tax |
| Taxes | Tax |
| EarningType | Compensation |
| FixedCompensation | Compensation |
| HourlyCompensation | Compensation |
| GarnishmentDeduction | Deduction |
| BenefitDeduction | Deduction |
| BenefitType | Benefits |
| BenefitCoverage | Benefits |
| DirectDeposit | Banking |
| BankAccount | Banking |
| PaymentMethod | Banking |
| CheckDate | Payroll |
| Check | Payroll |
| PayStub | Payroll |
| TimeOff | TimeOff |
| TimeOffBalance | TimeOff |
| TimeOffAccrual | TimeOff |
| TimeOffPolicy | TimeOff |
| WorkerComp | Compliance |
| WorkerCompClass | Compliance |
| Department | Organization |
| Location | Organization |
| Signer | Compliance |
| SignerRole | Compliance |
| ElectronicSignature | Compliance |
| TaxRate | Tax |
| StateCode | Tax |
| PayPeriod | Payroll |
| Bonus | Compensation |
| ExemptionStatus | Tax |
| FilingStatus | Tax |
| Query | Root |
| Mutation | Root |
| CompanyInput | Input |
| EmployeeInput | Input |
| ContractorInput | Input |
| PayrollInput | Input |
| BenefitInput | Input |
| TimeOffInput | Input |
| BankAccountInput | Input |
| DirectDepositInput | Input |
| TaxElectionInput | Input |
| CompensationInput | Input |
| TerminationInput | Input |
| BonusInput | Input |
| DepartmentInput | Input |

## Schema Notes

- All monetary amounts are represented as `String` in currency format (cents avoided; Gusto returns string decimals).
- Dates use `String` in ISO 8601 format (`YYYY-MM-DD`).
- UUIDs are typed as `ID`.
- Enums (StateCode, BenefitType, ExemptionStatus, FilingStatus) reflect Gusto REST API enumerated values.
- This schema is conceptual. Gusto does not currently expose a native GraphQL endpoint.
