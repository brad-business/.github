# BRAD Business

BRAD Business is an SME product that handles all major transaction operations in a business environment.
It is primarily an ERP Product for Small Businesses.

## Overview

It is premised on the fact that all businesses have similar operations. It doesn't matter which one.
Whether it is a restaurant, clinic, mini market, wholesale business or boutique business, their operations
share these similarities:

- They have items to sell or offer for sale (inventory)
- They have cash or credit transactions
- They need to have an accounting process for all their incomes and expenses.

## Access

BRAD Business will be initially for individual accounts. A cloud-based version will be envisioned in the future.
Its installation will be primarily web based although a desktop version will also be available subject to servicing
fees.

Due to the nature of the application and the nature of local business environments, it is prudent to provide Desktop
and mobile clients particularly for basic services like Point of Sale (POS).

Integration with other software is also crucial to enable a larger use case.

The software is essentially a monolith with a heavy regard to API services and checked into version management. This should however form the basis for a microservice environment that can later be made performant.

## Environment

The initial environment for the application is:

- PHP/Laravel (v 9.0 +)
- Web Server - Apache for Local installation and shared hosting for online versions.
- MySQL/MariaDB database
- Desktop clients in Java (Swing or JavaFX)
- Mobile Client in Android stack (Kotlin, React Native or Flutter)

## Modules

There are three version controlled modules and an extra custom module for special purposes. These are:

- Basic
- Standard
- Enterprise
- Custom

### Basic

This is suitable for the very small business that just needs to record daily sale transactions and related
stock operations. This module is the basis of all the other modules and costs the least.

The git branch name for this module is `basic`. The functionality of this module include:

- Inventory Management
- Point of Sale (POS)
- Daily, Weekly, Monthly Reports

### Standard

This is suitable for a majority of SMEs and record almost all aspects of an SME business. It is recomended
to businesses with daily operations and a need to have accurate accounting practices.

The git branch name for this module is `standard`. The functionality of this module include:

- All of Basic +
- Stock Control
- Accounting
- CRM
- Payroll

### Enterprise

This module is suitable for businesses that require integrations with other common services and APIs. It
also includes an eCommerce functionality for those businesses that require online access to their products.

The git branch name for this module is `enterprise`. The functionality of this module include:

- All of Standard +
- Bank Integration
- Common API Integration
- Communication (SMS, Email)
- eCommerce
- 24/7 technical support

### Custom

This module is suitable for those businesses that require services not available in the standard or enterprise
modules. Because of their proprietory nature, this module has a special git naming convention. The git branches
for this module will have a `custom/` prefix to distingush between versions. Some of the envisioned functionality
includes:

- All of Enterprise +
- Custom Payment Integration
- Integration with internal systems and processes
- Daily cloud backup
- Other requirements per customer requests

All these modules are supported by web, desktop and mobile clients and are forward based services, i.e. a sale in the basic module will only register the sale and create a cash received record but a sale in the enterprise + modules will also post the same and add an accounting record too. The API endpoint will be similar but the execution of the services will be slightly different.

