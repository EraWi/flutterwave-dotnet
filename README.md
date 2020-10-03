<p align="center">
    <img title="Flutterwave" height="200" src="https://flutterwave.com/images/logo-colored.svg" width="50%"/>
</p>

# .NET Library for Flutterwave (version 3) APIs
This library makes it easy to consume [Flutterwave API (v3)](https://developer.flutterwave.com/reference#introduction-1) in .Net projects.

## Introduction
This library implements the following services:
1. Banks
    * Get bank branches
    * Get all banks
2. Miscellaneous
    * Verify a bank account number
3. Payments
    * Initiate payment
4. Transactions
    * Get all transactions
    * Verify a transaction
    
## Configuration
1. Include the Flutterwave.Net namespace to expose all types
    ```c#
    ...
    using Flutterwave.Net;
    ...
    ```
2. Declare and initialise the [FlutterwaveAPI](src/flutterwave-dotnet/FlutterwaveApi.cs) class with your secret key
    ```c#
    string flutterwaveSecretKey = ConfigurationManager.AppSettings["FlutterwaveSecretKey"];
    var api = new FlutterwaveApi(flutterwaveSecretKey);
    ```

## Usage

### - Banks
1. Get bank branches
    ```c#
    string bankId = "280";

    GetBankBranchesResponse response = api.GetBankBranches(bankId)

    // success
    if (response.Status == "success")
    {
        // Get bank branches
        List<BankBranch> bankBranches = response.Data;
    }
    // error
    else
    {
        // Get error message
        string errorMessage = response.Message;
    }
    ```
    
2. Get all banks
    ```c#
    GetBanksResponse response = api.GetBanks(Country.Nigeria)

    // success
    if (response.Status == "success")
    {
        // Get all banks
        List<Bank> banks = response.Data;
    }
    // error
    else
    {
        // Get error message
        string errorMessage = response.Message;
    }
    ```

### - Miscellaneous
1. Verify a bank account number
    ```c#
    string accountNumber = "0690000032";
    string bankCode = "044";
    VerifyBankAccountResponse response = api.Miscellaneous.VerifyBankAccount(accountNumber, bankCode);

    // success
    if (response.Status == "success")
    {
        // Get the bank account
        BankAccount bankAccount = response.Data;
    }
    // error
    else
    {
        // Get error message
        string errorMessage = response.Message;
    }
    ```

### - Payments
1. Initiate payment
    ```c#
    string txRef = "hooli-tx-1920bbtytty";
    decimal amount = 100;
    string redirectUrl = "https://webhook.site/9d0b00ba-9a69-44fa-a43d-a82c33c36fdc";
    string customerEmail = "user@gmail.com";
    string customerPhonenumber = "08012345678";
    string customerName = "Yemi Desola";
    string paymentTitle = "Pied Piper Payments";
    string paymentDescription = "Middleout isn't free. Pay the price";
    string brandLogoUrl = "https://assets.piedpiper.com/logo.png";

    InitiatePaymentResponse response = api.Payments.InitiatePayment(txRef,
                                                                    amount,
                                                                    redirectUrl,
                                                                    customerName,
                                                                    customerEmail,
                                                                    customerPhonenumber,
                                                                    paymentTitle,
                                                                    paymentDescription,
                                                                    brandLogoUrl);

    // success
    if (response.Status == "success")
    {
        // Get payment hosted link 
        string hostedLink = response.Data.Link;
    }
    // error
    else
    {
        // Get error message
        string errorMessage = response.Message;
    }
    ```

### - Transactions
1. Get all transactions
    ```c#
    GetTransactionsResponse response = api.Transactions.GetTransactions();

    // success
    if (response.Status == "success")
    {
        // Get all transactions
        List<Transaction> transactions = response.Data;
    }
    // error
    else
    {
        // Get error message
        string errorMessage = response.Message;
    }
    ```
2. Verify a transaction
    ```c#
    string id = "1234567";
    VerifyTransactionResponse response = api.Transactions.VerifyTransaction(id);

    // success
    if (response.Status == "success")
    {
        // Get the transaction
        Transaction transaction = response.Data;
        
        // Verify transaction status
        bool isSuccess = transaction.Status == "successful";
        
        // Verify that the transaction reference, currency and charged amount i.e
        // transaction.TxRef, transaction.Currency and transaction.ChargedAmount
        // are what you expect them to be
        
    }
    // error
    else
    {
        // Get error message
        string errorMessage = response.Message;
    }
    ```

## Support
Create a new issue or add a comment to an open issue to request for new features and/or report bugs

[Send a mail](mailto:hello@egahi.net) for further assistance using this library
