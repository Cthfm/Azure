# Variable Types

## ​Overview

Azure Bicep supports several fundamental data types for defining infrastructure as code:

| Data Type        | Description                                                                                      | Example                                             |
| ---------------- | ------------------------------------------------------------------------------------------------ | --------------------------------------------------- |
| **String**       | A sequence of characters enclosed in single quotes. Supports escape sequences and interpolation. | `param exampleString string = 'test value'`         |
| **Integer**      | A 64-bit whole number.                                                                           | `param exampleInt int = 42`                         |
| **Boolean**      | Represents a true or false value.                                                                | `param exampleBool bool = true`                     |
| **Array**        | An ordered collection of values of any type.                                                     | `var exampleArray = ['abc', 123, true]`             |
| **Object**       | A collection of key-value pairs, where keys are strings and values can be of any type.           | `var exampleObject = { name: 'example', count: 1 }` |
| **SecureString** | A string whose value is treated as sensitive information.                                        | `@secure() param password string`                   |
| **SecureObject** | An object whose contents are treated as sensitive information.                                   | `@secure() param configValues object`               |
| **Union**        | A type that allows a value to be one of several specified types or literals.                     | \`type direction = 'north'                          |
| **User-defined** | Custom types created using the `type` keyword to encapsulate complex structures or constraints.  | \`type storageAccountSku = 'Standard\_LRS'          |
