# Quantum Computing Power Marketplace Smart Contract

## Overview

The Quantum Computing Power Marketplace is a decentralized smart contract written in Clarity. It allows providers to list quantum computing resources, while users can book these resources based on their available balance. The contract also features functionality to manage balances, book resources, queue jobs, and update market-related variables based on demand.

This contract implements core functionalities for resource management and financial transactions in a quantum computing marketplace, offering seamless interactions between users and providers.

## Features

- **Resource Listing**: Providers can list computing resources with defined computational power and price per unit.
- **Resource Availability Management**: Providers can update the availability status of their listed resources.
- **Booking Mechanism**: Users can book resources for use based on their balance and the resource’s availability.
- **Deposit and Withdraw Balance**: Users can manage their balances by depositing or withdrawing funds.
- **Job Management**: Users can queue jobs to use booked resources, with job status tracking.
- **Demand Factor Update**: The demand factor, which can affect pricing, is periodically updated by the contract owner.
- **Price Calculation**: Retrieves the current price of a specific resource based on demand.
- **Market Value Tracking**: Tracks the total market value of listed resources.

## Contract Components

### Constants
- **Contract Owner**: Specifies the owner of the contract, who has administrative privileges.
- **Error Codes**: Various error codes are used for handling specific error cases, such as insufficient balance or unauthorized actions.

### Data Maps
- **`quantum-resources`**: Stores details for each resource provided, including computational power, price per unit, and availability status.
- **`user-balances`**: Tracks the balance for each user in the marketplace.

### Variables
- **`next-resource-id`**: Tracks the next available resource ID.
- **`job-status`**: Stores the current status of jobs queued in the system.
- **`demand-factor`**: An adjustable factor that can influence resource pricing based on demand.
- **`total-market-value`**: Tracks the total market value of resources listed on the marketplace.

### Functions

#### Public Functions
1. **`(list-resource (computational-power uint) (price-per-unit uint))`**: Allows providers to list a new resource by specifying computational power and price per unit.
2. **`(update-resource-availability (resource-id uint) (available bool))`**: Allows providers to update the availability status of a specific resource.
3. **`(book-resource (provider principal) (resource-id uint) (units uint))`**: Enables users to book units of a specified resource if they have sufficient balance.
4. **`(deposit (amount uint))`**: Allows users to deposit funds into their marketplace balance.
5. **`(withdraw (amount uint))`**: Allows users to withdraw funds from their balance.
6. **`(queue-job (provider principal) (resource-id uint) (job-data (string-ascii 1000)))`**: Queues a job for a specific resource.
7. **`(update-job-status (new-status (string-ascii 20)))`**: Updates the status of a queued job; this function is restricted to the contract owner.
8. **`(update-demand-factor (new-factor uint))`**: Updates the demand factor, potentially affecting resource prices. Restricted to the contract owner.

#### Read-Only Functions
1. **`(get-job-status)`**: Retrieves the current status of queued jobs.
2. **`(get-current-price (provider principal) (resource-id uint))`**: Calculates the current price of a resource based on the demand factor.
3. **`(get-balance (user principal))`**: Retrieves the balance of a specified user.
4. **`(get-resource-details (provider principal) (resource-id uint))`**: Retrieves details of a specified resource.
5. **`(get-total-market-value)`**: Returns the total market value of all listed resources.

## Error Handling

The contract uses custom error codes for robust error handling:
- **`err-owner-only`**: Returned when a non-owner tries to perform owner-specific actions.
- **`err-not-found`**: Indicates a resource was not found.
- **`err-already-listed`**: Indicates a resource is already listed.
- **`err-insufficient-balance`**: Triggered when a user lacks sufficient balance for booking.
- **`err-insufficient-funds`**: Returned if a user attempts to withdraw more than their available balance.
- **`err-invalid-input`**: Used to catch invalid inputs such as zero values for resource parameters.

## Security

Input validation checks are added for critical functions to prevent invalid data from causing unexpected behavior. Additionally, administrative functions are restricted to the contract owner, ensuring controlled management of demand factors and job status updates.

## Usage Example

1. **Listing a Resource**: 
   ```clarity
   (list-resource u100 u10) ;; Lists a resource with 100 units of computational power at a rate of 10 per unit
   ```

2. **Depositing Balance**:
   ```clarity
   (deposit u1000) ;; Deposits 1000 units to the user’s balance
   ```

3. **Booking a Resource**:
   ```clarity
   (book-resource provider principal resource-id u5) ;; Books 5 units of the resource from a specified provider
   ```
## License
This project is open-sourced under the MIT License.