# SOAP

The `SOAP` keyword enables bots to communicate with legacy SOAP/XML web services, allowing integration with enterprise systems, government APIs, and older corporate infrastructure that still relies on SOAP protocols.

---

## Syntax

```basic
result = SOAP "wsdl_url", "operation", params
```

---

## Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `wsdl_url` | String | URL to the WSDL file or SOAP endpoint |
| `operation` | String | Name of the SOAP operation to call |
| `params` | Object | Parameters to pass to the operation |

---

## Description

`SOAP` sends a SOAP (Simple Object Access Protocol) request to a web service, automatically building the XML envelope and parsing the response. This enables integration with legacy enterprise systems that haven't migrated to REST APIs.

Use cases include:
- Connecting to government tax and fiscal systems
- Integrating with legacy ERP systems (SAP, Oracle)
- Communicating with banking and payment systems
- Accessing healthcare HL7/SOAP interfaces
- Interfacing with older CRM systems

---

## Examples

### Basic SOAP Request

```basic
' Call a simple SOAP service
result = SOAP "https://api.example.com/service?wsdl", "GetUserInfo", #{
    "userId": "12345"
}

TALK "User name: " + result.name
```

### Tax Calculation Service

```basic
' Brazilian NF-e fiscal service example
nfe_params = #{
    "CNPJ": company_cnpj,
    "InvoiceNumber": invoice_number,
    "Items": invoice_items,
    "TotalValue": total_value
}

result = SOAP "https://nfe.fazenda.gov.br/NFeAutorizacao4/NFeAutorizacao4.asmx?wsdl",
    "NfeAutorizacao",
    nfe_params

IF result.status = "Authorized" THEN
    TALK "Invoice authorized! Protocol: " + result.protocol
ELSE
    TALK "Authorization failed: " + result.errorMessage
END IF
```

### Currency Exchange Service

```basic
' Get exchange rates from central bank
params = #{
    "fromCurrency": "USD",
    "toCurrency": "BRL",
    "date": FORMAT(NOW(), "YYYY-MM-DD")
}

result = SOAP "https://www.bcb.gov.br/webservice/cotacao.asmx?wsdl",
    "GetCotacao",
    params

rate = result.cotacao.valor
TALK "Today's USD/BRL rate: " + rate
```

### Weather Service (Legacy)

```basic
' Access legacy weather SOAP service
weather_params = #{
    "city": city_name,
    "country": "BR"
}

result = SOAP "https://weather.example.com/service.asmx?wsdl",
    "GetWeather",
    weather_params

TALK "Weather in " + city_name + ": " + result.description
TALK "Temperature: " + result.temperature + "°C"
```

### SAP Integration

```basic
' Query SAP for material information
sap_params = #{
    "MaterialNumber": material_code,
    "Plant": "1000"
}

result = SOAP "https://sap.company.com:8443/sap/bc/srt/wsdl/MATERIAL_INFO?wsdl",
    "GetMaterialDetails",
    sap_params

material = result.MaterialData
TALK "Material: " + material.Description
TALK "Stock: " + material.AvailableStock + " units"
TALK "Price: $" + material.StandardPrice
```

---

## Working with Complex Types

### Nested Objects

```basic
' SOAP request with nested structure
customer_data = #{
    "Customer": #{
        "Name": customer_name,
        "Address": #{
            "Street": street,
            "City": city,
            "ZipCode": zipcode,
            "Country": "BR"
        },
        "Contact": #{
            "Email": email,
            "Phone": phone
        }
    }
}

result = SOAP "https://crm.company.com/CustomerService.asmx?wsdl",
    "CreateCustomer",
    customer_data

TALK "Customer created with ID: " + result.CustomerId
```

### Array Parameters

```basic
' Send multiple items in SOAP request
order_items = [
    #{ "SKU": "PROD-001", "Quantity": 2, "Price": 99.99 },
    #{ "SKU": "PROD-002", "Quantity": 1, "Price": 49.99 },
    #{ "SKU": "PROD-003", "Quantity": 5, "Price": 19.99 }
]

order_params = #{
    "OrderHeader": #{
        "CustomerId": customer_id,
        "OrderDate": FORMAT(NOW(), "YYYY-MM-DD")
    },
    "OrderItems": order_items
}

result = SOAP "https://erp.company.com/OrderService?wsdl",
    "CreateOrder",
    order_params

TALK "Order " + result.OrderNumber + " created successfully!"
```

---

## Response Handling

### Parsing Complex Responses

```basic
' Handle structured SOAP response
result = SOAP "https://api.example.com/InvoiceService?wsdl",
    "GetInvoices",
    #{ "CustomerId": customer_id, "Year": 2024 }

' Access nested response data
FOR EACH invoice IN result.Invoices.Invoice
    TALK "Invoice #" + invoice.Number + " - $" + invoice.Total
    TALK "  Date: " + invoice.Date
    TALK "  Status: " + invoice.Status
END FOR
```

### Checking Response Status

```basic
result = SOAP service_url, operation, params

IF result.ResponseCode = "0" OR result.Success = true THEN
    TALK "Operation completed successfully"
    ' Process result data
ELSE
    TALK "Operation failed: " + result.ErrorMessage
END IF
```

---

## Error Handling

```basic
ON ERROR RESUME NEXT

result = SOAP "https://legacy.system.com/service.asmx?wsdl",
    "ProcessPayment",
    payment_params

IF ERROR THEN
    error_msg = ERROR_MESSAGE
    
    IF INSTR(error_msg, "timeout") > 0 THEN
        TALK "The service is taking too long. Please try again."
    ELSE IF INSTR(error_msg, "WSDL") > 0 THEN
        TALK "Cannot connect to the service. It may be down."
    ELSE IF INSTR(error_msg, "authentication") > 0 THEN
        TALK "Authentication failed. Please check credentials."
    ELSE
        TALK "Service error: " + error_msg
    END IF
ELSE
    IF result.TransactionId THEN
        TALK "Payment processed! Transaction: " + result.TransactionId
    END IF
END IF
```

### Common Errors

| Error | Cause | Solution |
|-------|-------|----------|
| `WSDL_PARSE_ERROR` | Invalid WSDL format | Verify WSDL URL and format |
| `SOAP_FAULT` | Service returned fault | Check error message from service |
| `TIMEOUT` | Request took too long | Increase timeout or retry |
| `CONNECTION_ERROR` | Cannot reach service | Check network and URL |
| `AUTHENTICATION_ERROR` | Invalid credentials | Verify authentication headers |

---

## Authentication

### WS-Security (Username Token)

```basic
' For services requiring WS-Security authentication
' Set credentials via SET HEADER before SOAP call
SET HEADER "Authorization", "Basic " + BASE64(username + ":" + password)

result = SOAP service_url, operation, params
```

### Certificate-Based Authentication

For services requiring client certificates, configure at the system level in `config.csv`:

```csv
name,value
soap-client-cert,/path/to/client.pem
soap-client-key,/path/to/client.key
soap-ca-cert,/path/to/ca.pem
```

---

## Practical Examples

### Brazilian NFe (Electronic Invoice)

```basic
' Emit electronic invoice to Brazilian tax authority
nfe_data = #{
    "infNFe": #{
        "ide": #{
            "cUF": "35",
            "natOp": "VENDA",
            "serie": "1",
            "nNF": invoice_number
        },
        "emit": #{
            "CNPJ": company_cnpj,
            "xNome": company_name
        },
        "dest": #{
            "CNPJ": customer_cnpj,
            "xNome": customer_name
        },
        "det": invoice_items,
        "total": #{
            "vNF": total_value
        }
    }
}

result = SOAP "https://nfe.fazenda.sp.gov.br/ws/NFeAutorizacao4.asmx?wsdl",
    "nfeAutorizacaoLote",
    nfe_data

IF result.cStat = "100" THEN
    TALK "NFe authorized! Key: " + result.chNFe
ELSE
    TALK "Error: " + result.xMotivo
END IF
```

### Healthcare HL7/SOAP

```basic
' Query patient information from healthcare system
patient_query = #{
    "PatientId": patient_id,
    "IncludeHistory": true
}

result = SOAP "https://hospital.example.com/PatientService?wsdl",
    "GetPatientRecord",
    patient_query

TALK "Patient: " + result.Patient.Name
TALK "DOB: " + result.Patient.DateOfBirth
TALK "Allergies: " + JOIN(result.Patient.Allergies, ", ")
```

### Legacy CRM Integration

```basic
' Update customer in legacy Siebel CRM
update_data = #{
    "AccountId": account_id,
    "AccountName": new_name,
    "PrimaryContact": #{
        "FirstName": first_name,
        "LastName": last_name,
        "Email": email
    },
    "UpdatedBy": bot_user
}

result = SOAP "https://siebel.company.com/eai_enu/start.swe?SWEExtSource=WebService&wsdl",
    "AccountUpdate",
    update_data

TALK "CRM updated. Transaction ID: " + result.TransactionId
```

---

## SOAP vs REST

| Aspect | SOAP | REST |
|--------|------|------|
| Protocol | XML-based | JSON typically |
| Standards | WS-Security, WS-*, WSDL | OpenAPI, OAuth |
| Use Case | Enterprise, legacy | Modern APIs |
| Keyword | `SOAP` | `POST`, `GET` |
| Complexity | Higher | Lower |

**When to use SOAP:**
- Integrating with legacy enterprise systems
- Government/fiscal APIs requiring SOAP
- Systems with strict WS-Security requirements
- Banking and financial services
- Healthcare systems (HL7 SOAP)

---

## Configuration

No specific configuration required. The keyword handles SOAP envelope construction automatically.

For services requiring custom SOAP headers or namespaces, these are inferred from the WSDL.

---

## Implementation Notes

- Implemented in Rust under `src/basic/keywords/http_operations.rs`
- Automatically fetches and parses WSDL
- Builds SOAP envelope from parameters
- Parses XML response into JSON-like object
- Timeout: 120 seconds by default
- Supports SOAP 1.1 and 1.2

---

## Related Keywords

- [POST](keyword-post.md) — For REST API calls
- [GET](keyword-get.md) — For REST GET requests
- [GRAPHQL](keyword-graphql.md) — For GraphQL APIs
- [SET HEADER](keyword-set-header.md) — Set authentication headers

---

## Summary

`SOAP` enables integration with legacy SOAP/XML web services that are still common in enterprise, government, and healthcare sectors. While REST is preferred for modern APIs, SOAP remains essential for connecting to fiscal systems (NFe, tax services), legacy ERPs (SAP, Oracle), and older enterprise infrastructure. The keyword handles XML envelope construction and parsing automatically, making SOAP integration as simple as REST calls.