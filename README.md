# QuantHive

**QuantHive** is a decentralized marketplace for quantum computing resources, allowing providers to list their computational power and users to book these resources seamlessly. This contract manages resource listings, bookings, user balances, and market dynamics through a transparent and secure framework.

## Features

- **Resource Listing**: Providers can list their quantum computing resources with specified computational power and price per unit.
- **Resource Booking**: Users can book available resources by specifying the provider, resource ID, and number of units required.
- **Balance Management**: Users can deposit and withdraw balances in the marketplace.
- **Demand Factor Tracking**: The contract maintains a demand factor that can be adjusted to influence pricing based on market conditions.
- **Job Management**: Users can queue jobs and update their status as required.
- **Market Value Calculation**: The total market value of all resources is calculated based on their computational power and price.

## Usage

### Smart Contract Functions

1. **List Resource**
   - `list-resource(computational-power: uint, price-per-unit: uint)`
   - Allows a provider to list a new quantum computing resource.

2. **Update Resource Availability**
   - `update-resource-availability(resource-id: uint, available: bool)`
   - Updates the availability status of a listed resource.

3. **Book Resource**
   - `book-resource(provider: principal, resource-id: uint, units: uint)`
   - Allows a user to book a specified number of units from a provider's resource.

4. **Deposit Balance**
   - `deposit(amount: uint)`
   - Users can deposit STX into their balance for bookings.

5. **Withdraw Balance**
   - `withdraw(amount: uint)`
   - Allows users to withdraw STX from their balance.

6. **Queue Job**
   - `queue-job(provider: principal, resource-id: uint, job-data: (string-ascii 1000))`
   - Queues a job for the specified resource.

7. **Update Job Status**
   - `update-job-status(new-status: (string-ascii 20))`
   - Updates the status of a queued job (restricted to contract owner).

8. **Update Demand Factor**
   - `update-demand-factor(new-factor: uint)`
   - Updates the demand factor influencing pricing (restricted to contract owner).

9. **Get Job Status**
   - `get-job-status()`
   - Retrieves the current status of a job.

10. **Get Current Price**
    - `get-current-price(provider: principal, resource-id: uint)`
    - Returns the current price of a resource based on demand.

11. **Get User Balance**
    - `get-balance(user: principal)`
    - Retrieves the balance of a specified user.

12. **Get Resource Details**
    - `get-resource-details(provider: principal, resource-id: uint)`
    - Returns details about a specific resource.

13. **Get Total Market Value**
    - `get-total-market-value()`
    - Retrieves the total market value of all listed resources.

## Security Considerations

- Ensure that only authorized users can update sensitive information, such as job status and demand factors.
- Always validate user inputs to prevent incorrect data from being processed.
- 
## License

This project is licensed under the MIT License.
