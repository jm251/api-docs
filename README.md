<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>API Creation Guide</title>
  <style>
    /* General Styles */
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background: #f5f5f5;
      color: #333;
    }
    .container {
      width: 90%;
      max-width: 960px;
      margin: 20px auto;
      padding: 20px;
      background: #fff;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    }
    /* Header Styles */
    header h1 {
      margin-top: 0;
      color: #2c3e50;
    }
    header p {
      font-size: 1.1em;
    }
    /* Section Styles */
    section {
      margin-bottom: 30px;
    }
    section h2 {
      border-bottom: 2px solid #e74c3c;
      padding-bottom: 5px;
      color: #e74c3c;
    }
    /* Diagram Styles */
    .diagram {
      background: #f0f0f0;
      padding: 15px;
      border-left: 4px solid #e74c3c;
      margin: 15px 0;
      overflow-x: auto;
      font-family: monospace;
    }
    /* Code Block Styles */
    pre.code {
      background: #333;
      color: #f8f8f2;
      padding: 15px;
      overflow-x: auto;
      border-radius: 5px;
      font-size: 0.9em;
    }
    /* List Styles */
    ul, ol {
      margin-left: 20px;
    }
    /* Link Styles */
    a {
      color: #2980b9;
      text-decoration: none;
    }
    a:hover {
      text-decoration: underline;
    }
  </style>
  <!-- Optional: Include Mermaid.js if you want to render the diagram -->
  <!--
  <script src="https://cdn.jsdelivr.net/npm/mermaid/dist/mermaid.min.js"></script>
  <script>
    mermaid.initialize({startOnLoad:true});
  </script>
  -->
</head>
<body>
  <div class="container">
    <header>
      <h1>API Creation Guide</h1>
      <p>This guide outlines the steps to create and use the API for order creation on the ShypBuddy platform.</p>
    </header>
    <section class="workflow">
      <h2>Workflow Graph</h2>
      <p>The following diagram explains the sequence of steps you need to follow:</p>
      <div class="diagram">
        <pre>
graph TD
    A[Register or Login<br>https://seller.shypbuddy.net]
    B[Complete your KYC<br>https://seller.shypbuddy.net/kyc]
    C[Add your default warehouse<br>https://seller.shypbuddy.net/address/list_address]
    D[Set up 3PL Preference Page<br>https://seller.shypbuddy.net/settings]
    E[Generate an API Token<br>https://seller.shypbuddy.net/settings]

    A --> B
    B --> C
    C --> D
    D --> E
        </pre>
      </div>
    </section>
    <section class="api-details">
      <h2>API Endpoint Details</h2>
      <p>Once you have completed the initial steps and generated a token, you can use the API endpoint to create orders.</p>
      <div class="endpoint">
        <h3>Endpoint</h3>
        <pre class="code">https://seller.shypbuddy.net/api/orderApi/createOrder</pre>
      </div>
      <div class="headers">
        <h3>Headers</h3>
        <ul>
          <li><strong>Content-Type:</strong> application/json</li>
          <li><strong>Authorization:</strong> Bearer &lt;your_generated_token&gt;</li>
        </ul>
        <p>Replace <code>&lt;your_generated_token&gt;</code> with the token you generated from the settings page.</p>
      </div>
      <div class="request-body">
        <h3>Request Body</h3>
        <p>Below is an example request body:</p>
        <pre class="code">
{
  "orderData": {
    "deliveryType": "FORWARD", // Options: "FORWARD" or "REVERSE"
    "isDangerousGoods": "n",     // "n" for no or "y" for yes
    "paymentMode": "cod",        // Options: "cod" or "prepaid"
    "length": 10,
    "breadth": 10,
    "height": 15,
    "warehouseName": "Warehouse", // Default warehouse name
    "packageCount": 2,
    "shippingMode": "surface",    // Options: "surface" or "air"
    "deadWeight": 0.5
    // "deliveryPartner": "shadowfax" // Optional: Uncomment if applicable
  },
  "customerAddressList": {
    "fullName": "Rahul Kumar",
    "contactNumber": "9876543210",
    "email": "rahul.kumar@email.com",
    "alternateNumber": "8765432109",
    "buyerCompanyName": "Tech Solutions Pvt Ltd",
    "buyerGstin": "27AAPFU0939F1ZV",
    "address": "B-404, Silver Heights, Sector 7",
    "landmark": "Near City Mall",
    "pincode": 400028,
    "createdAt": "2024-03-21T10:30:00Z",
    "city": "Mumbai",
    "state": "Maharashtra"
  },
  "packageList": [
    {
      "name": "Gaming Laptop",
      "qty": 1,
      "price": 82,
      "category": "Electronics",
      "sku": "LAP-GM-001",
      "hsnCode": "847130"
    },
    {
      "name": "Wireless Mouse",
      "qty": 2,
      "price": 12,
      "category": "Electronics",
      "sku": "ACC-MS-002",
      "hsnCode": "847160"
    }
  ]
}
        </pre>
      </div>
    </section>
    <section class="usage-steps">
      <h2>Usage Steps Summary</h2>
      <ol>
        <li>
          <strong>Register or Login:</strong> Visit <a href="https://seller.shypbuddy.net" target="_blank">https://seller.shypbuddy.net</a> to register or log in to your account.
        </li>
        <li>
          <strong>Complete your KYC:</strong> Complete your KYC at <a href="https://seller.shypbuddy.net/kyc" target="_blank">https://seller.shypbuddy.net/kyc</a>.
        </li>
        <li>
          <strong>Add your Default Warehouse:</strong> Set up your default warehouse at <a href="https://seller.shypbuddy.net/address/list_address" target="_blank">https://seller.shypbuddy.net/address/list_address</a>.
        </li>
        <li>
          <strong>Configure 3PL Preferences:</strong> Go to the 3PL Preference Page at <a href="https://seller.shypbuddy.net/settings" target="_blank">https://seller.shypbuddy.net/settings</a>.
        </li>
        <li>
          <strong>Generate an API Token:</strong> Generate your API token from <a href="https://seller.shypbuddy.net/settings" target="_blank">https://seller.shypbuddy.net/settings</a> and use it in your API requests.
        </li>
      </ol>
      <p>Follow the guide and the examples to integrate with the API successfully.</p>
    </section>
  </div>
</body>
</html>
