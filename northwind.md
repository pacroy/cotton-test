[Cotton](https://github.com/chonla/cotton) command: `cotton -u https://services.odata.org -d northwind.md`

# 1. List Northwind Customers

## GET /V2/Northwind/Northwind.svc/Customers/?$format=json&$top=10

Query first 10 customers

## Expectation

| Assert | Expected |
| - | - |
| StatusCode | 200 |
| Data.d[0].CustomerID | ALFKI |
| Data.d[1].CustomerID | ANATR |
| Data.d[2].CustomerID | ANTON |
| Data.d[3].CustomerID | AROUT |
| Data.d[4].CustomerID | BERGS |
| Data.d[5].CustomerID | BLAUS |
| Data.d[6].CustomerID | BLONP |
| Data.d[7].CustomerID | BOLID |
| Data.d[8].CustomerID | BONAP |
| Data.d[9].CustomerID | BOTTM |
| Data.d[10].CustomerID | *Should not exist*

# 2. Filter Customer by ContactName

## GET /V2/Northwind/Northwind.svc/Customers/?$format=json&$filter=ContactName eq 'Frédérique Citeaux'

Query customer with ContactName = 'Frédérique Citeaux'

## Expectation

| Assert | Expected |
| - | - |
| StatusCode | 200 |
| Data.d.results[0].CustomerID | BLONP |
| Data.d.results[0].CompanyName | *Should exist* |
| Data.d.results[0].ContactName | *Should exist* |
| Data.d.results[0].ContactTitle | *Should exist* |
| Data.d.results[0].Address | *Should exist* |
| Data.d.results[0].City | *Should exist* |
| Data.d.results[0].Region | *Should be null* |
| Data.d.results[0].Region | *Should exist* |
| Data.d.results[0].PostalCode | *Should exist* |  
| Data.d.results[0].Country | *Should exist* |
| Data.d.results[0].Phone | *Should exist* |
| Data.d.results[0].Fax | *Should exist* |
| Data.d.results[0].Orders | *Should exist* |
| Data.d.results[0].CustomerDemographics | *Should exist* |
| Data.d.results[1] | *should not exist* |

# 3. Get Customer BOLID

Get single customer ID `BOLID`

## GET /V2/Northwind/Northwind.svc/Customers('BOLID')/?$format=json&$select=CustomerID,CompanyName,ContactName,Country

## Expectation

| Assert | Expected |
| - | - |
| StatusCode | 200 |
| Data.d.CustomerID | BOLID |
| Data.d.CompanyName | *Should exist* |
| Data.d.ContactName | *Should exist* |
| Data.d.ContactTitle | *Should not exist* |
| Data.d.Address | *Should not exist* |
| Data.d.City | *Should not exist* |
| Data.d.Region | *Should not exist* |
| Data.d.PostalCode | *Should not exist* |
| Data.d.Country | *Should exist* |
| Data.d.Phone | *Should not exist* |
| Data.d.Fax | *Should not exist* |
| Data.d.Orders | *Should not exist* |
| Data.d.CustomerDemographics | *Should not exist* |

# 4. Get Product 1

## GET /V2/Northwind/Northwind.svc/Products(1)/?$format=json

## Expectation

| Assert | Expected |
| - | - |
| StatusCode | 200 |
| Data.d.ProductID | 1 |
| Data.d.Discontinued | *Should be false* |

# 5. Get Employee 1 (Slash tests)

## GET /V2/Northwind/Northwind.svc/Employees(1)?$select=EmployeeID,FirstName,LastName, BirthDate,PhotoPath

| Header | Value |
| - | - |
| Accept | application/json |

## Expectation

| Assert | Expected |
| - | - |
| StatusCode | 200 |
| Data.d.EmployeeID | 1 |
| Data.d.LastName | Davolio |
| Data.d.FirstName | Nancy |
| Data.d.BirthDate | /Date(-664761600000)/ |
| Data.d.PhotoPath | http://accweb/emmployees/davolio.bmp |