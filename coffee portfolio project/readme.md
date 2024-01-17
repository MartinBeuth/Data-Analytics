# Readme
---
**Inhalt / *Contents*:**

1. [Allgemein / *General*](#allgemein)

2. [Formeln für Datenaufbearbeitung / *Formulas for data processing*](#formeln)


|  |  |
|--|--|
|[Coffee Type](#coffee_type)|[Coffee Type Name](#coffee_type_name)
|[Country](#country)| [Customer Name](#customer_name)
| [E-Mail](#e_mail) |  [Loyality Card](#loyality_card)
| [Roast Type Name](#roast_type_name) |  [Roast Type / Size / Unit Price](#roast_type_size_unit_price)
| [Sales](#sales)

---

## Allgemein

1. Die Datenaufbereitung erfolgte mit **Libre Calc**.

 2. Das Projekt enthält **zwei Dateien**. 
*The project contains **two files.*** 
 -  orders_of_coffee
 -  orders_of_coffee_with_charts
 
 orders_of_coffee ist der **unbearbeitete** Datensatz. 
 orders_of_coffee_with_charts ist der **bearbeitete** Datensatz. 
 *orders_of_coffee is the **unprocessed** data set. 
 orders_of_coffee_with_charts is the **processed** data set.* 
 

 3. Beide Datensätze enthalten **drei voneinander abweichende Datenblätter**: 
 *Both data sets contain **three different data sheets:***
 - orders
 - customers,
 - products

4. orders_of_coffee_with_charts **enthält zudem:**
*orders_of_coffee_with_charts **also contains:***

 - Dashboard
 - Top 5 Customers
 - Sales_Country
 - Total Sales
 
5. Das `Dashboard` **fasst** den Inhalt von `Top 5 Customers, Sales_Country und Total Sales` **zusammen**.
 *The `dashboard` **summarizes** the content of `Top 5 Customers, Sales_Country and Total Sales`.*

6. Die **Datenaufbereitung** findet weitesgehend in `orders` statt. 
*The **data preparation** takes place largely in `orders`.* 

---

## Formeln

 1. #### Customer_Name: 
 
 Die Namen der Kunden werden ermittelt mit der Formel: 
 *The names of the customers are determined using the formula:* 
 ```
 INDEX($customers.B1:B1002;VERGLEICH(1;($customers.A1:A1002=C2);0))` 
 ```

Die gegebene Formel  besteht aus zwei Teilen:
*The given formula consists of two parts:*

 -  `VERGLEICH(1;($customers.A1:A1002=C2);0)`: Dieser Teil der Formel sucht nach dem ersten Wert in der Spalte A der Tabelle  `$customers`, der mit dem Wert in der Zelle C2 übereinstimmt. Die Funktion gibt die Position dieses Werts zurück. *This part of the formula searches for the first value in column A of the table `$customers` that matches the value in cell C2. The function returns the position of this value.*
    
-  `INDEX($customers.B1:B1002;...)`: Dieser Teil der Formel verwendet die Position, die durch die  `VERGLEICH`-Funktion gefunden wurde, um den Wert in der entsprechenden Zelle in der Spalte B der Tabelle  `$customers`  abzurufen. *This part of the formula uses the position found by the 'MATCH' function to retrieve the value in the corresponding cell in column B of the '$customers' table.*

 2. #### E_Mail 
 
 Die E-Mail des Kunden wird ermittelt mit der Formel: 

     `WENN(INDEX($customers.C1:C1001;VERGLEICH(1;($customers.A1:A1001=C2);0))<>0;INDEX($customers.C1:C1001;VERGLEICH(1;($customers.A1:A1001=C2);0));"not available")`
 
Die Formel besteht aus mehreren Teilen:

-  `INDEX($customers.C1:C1001;VERGLEICH(1;($customers.A1:A1001=C2);0))`  - Dieser Teil sucht nach einer Übereinstimmung des Wertes in der Spalte A der Tabelle "customers" mit dem Wert in der Zelle C2. Wenn eine Übereinstimmung gefunden wird, wird der Wert in der entsprechenden Zelle in der Spalte C zurückgegeben. *This part searches for a match between the value in column A of the "customers" table and the value in cell C2. If a match is found, the value in the corresponding cell in column C is returned.*
    
-  `WENN(INDEX(...)<>0;INDEX(...);"not available")`  - Dieser Teil überprüft, ob der zurückgegebene Wert aus dem vorherigen Schritt ungleich 0 ist. Wenn der Wert ungleich 0 ist, wird der Wert zurückgegeben. Andernfalls wird der Text "not available" ausgegeben. *This part checks whether the value returned from the previous step is not equal to 0. If the value is not equal to 0, the value is returned. Otherwise, the text "not available" is output.*

3. #### Country

Das Land des Kunden wird mit folgender Formel ermittelt:
*The customer's country is determined using the following formula*:  

    WENN(ISTFEHLER(INDEX($customers.G1:G1002;VERGLEICH(1;($customers.A1:A1002=C2);0)));"not available";INDEX($customers.G1:G1002;VERGLEICH(1;($customers.A1:A1002=C2);0)))

Die Analyse der Formel ergibt:
*The formula is analysed:*

-  `($customers.A1:A1002=C2)`  vergleicht den Wert in Zelle C2 mit dem Zellbereich A1:A1002 in der Tabelle "customers". *compares the value in cell C2 with the cell range A1:A1002 in the "customers" table.*
    
-  `VERGLEICH(1;($customers.A1:A1002=C2);0)`  sucht nach dem ersten übereinstimmenden Wert in der Spalte A des Zellbereichs A1:A1002 und gibt die Position zurück. *searches for the first matching value in column A of the cell range A1:A1002 and returns the position.*
    
-  `INDEX($customers.G1:G1002;VERGLEICH(1;($customers.A1:A1002=C2);0))`  ruft den Wert aus der Spalte G ab, der sich in der gleichen Zeile wie der übereinstimmende Wert in der Spalte A befindet. *retrieves the value from column G that is in the same row as the matching value in column A.*
    
-  `ISTFEHLER(INDEX($customers.G1:G1002;VERGLEICH(1;($customers.A1:A1002=C2);0)))`  überprüft, ob der abgerufene Wert einen Fehler enthält. *checks whether the retrieved value contains an error.*
    
-  `WENN(ISTFEHLER(INDEX($customers.G1:G1002;VERGLEICH(1;($customers.A1:A1002=C2);0)));"not available";INDEX($customers.G1:G1002;VERGLEICH(1;($customers.A1:A1002=C2);0)))`  gibt entweder "not available" zurück, wenn der abgerufene Wert einen Fehler enthält, oder den abgerufenen Wert selbst, wenn er verfügbar ist.  *returns either "not available" if the retrieved value contains an error, or the retrieved value itself if it is available.*

4. #### Coffee_Type

Die Kaffeesorte wird mit der Formel bestimmt:
*The type of coffee is determined using the formula:*
```
INDEX($products.A1:G49;VERGLEICH($D2;$products.A1:A49;0);VERGLEICH($I1;$products.A1:G1;0))

```

- Die Formel verwendet die `INDEX`-Funktion, um Daten aus dem Bereich `$products.A1:G49` abzurufen. Die Zeilennummer wird durch die `VERGLEICH`-Funktion basierend auf dem Wert in Zelle `$D2` ermittelt, während die Spaltennummer durch die `VERGLEICH`-Funktion ausgehend auf dem Wert in Zelle `$I1` ermittelt wird.
*The formula uses the `INDEX` function to retrieve data from the range `$products.A1:G49`. The row number is determined by the `CALCIFY` function based on the value in cell `$D2`, while the column number is determined by the `MATCH` function based on the value in cell `$I1`.*

5. #### Roast_Type_Size_Unit_Price

Die Röstungsart wird bestimmt durch:


*The type of coffee is determined using the formula:*
```
INDEX($products.B1:G49;VERGLEICH($D2;$products.A1:A49;0);VERGLEICH($I1;$products.A1:G1;0))

```

Die Größe wird bestimmt durch:

*The size is determined using the formula:*
```
INDEX($products.C1:G49;VERGLEICH($D2;$products.A1:A49;0);VERGLEICH($I1;$products.A1:G1;0))

```
Der Stückpreis
*The unit price is determined using the formula:*
```
INDEX($products.D1:G49;VERGLEICH($D2;$products.A1:A49;0);VERGLEICH($I1;$products.A1:G1;0))

```

Lediglich die Bereichsdefinition ändert sich von `B1:G49` über `C1:G49` zu `D1:G49`.

*Only the range definition changes from `B1:G49` via `C1:G49` to `D1:G49`.*

Ansonsten gilt für alle:

*Otherwise, the same applies to all:*

-  `INDEX($products.B1:G49; ...)`  - Bereichsdefinition: B1 bis G49 in der Tabelle "products". *Range definition: B1 to G49 in the "products" table.*
    
-  `VERGLEICH($D2;$products.A1:A49;0)`  - Dieser Teil der Formel sucht nach dem Wert in Zelle D2 in der Spalte A1 bis A49 der Tabelle "products" und gibt die Zeilennummer zurück, in der der Wert gefunden wurde.  *This part of the formula searches for the value in cell D2 in column A1 to A49 of the "products" table and returns the row number in which the value was found.*
    
-  `VERGLEICH($I1;$products.A1:G1;0)`  - Dieser Teil der Formel sucht nach dem Wert in Zelle I1 in der Zeile A1 bis G1 der Tabelle "products" und gibt die Spaltennummer zurück, in der der Wert gefunden wurde. *This part of the formula searches for the value in cell I1 in row A1 to G1 of the "products" table and returns the column number in which the value was found.*

5. #### Sales
Die Verkäufe ergeben sich aus der Multiplikation von `Unit Price` und `Quantity`:
*The sales result from the multiplication of `'unit price'` and `'quantity'`:*

```
L2*E2

```
6. #### Coffee_Type_Name

Hierbei handelt es sich um den ausbuchstabierten Namen von `Coffee Type`.

*This is the spelt-out name of `'Coffee Type'`.*
```
WENN(I2="Rob";"Robuster";WENN(I2="Exc";"Excelser";WENN(I2="Ara";"Arabica";WENN(I2="Lib";"Liberica"))))
```
Die Formel überprüft die Zelle `I2` (Coffee Type). Wenn der Wert in `I2 "Rob"` ist, wird der Wert `"Robuster"` zurückgegeben. Andernfalls wird die nächste WENN-Funktion überprüft. Wenn der Wert in `I2 "Exc"` ist, wird der Wert `"Excelser"` zurückgegeben. Dieser Prozess wird fortgesetzt, bis alle Bedingungen überprüft wurden. Wenn keine der Bedingungen erfüllt ist, wird der Standardwert `"Liberica"` zurückgegeben.
*The formula checks the cell `I2` (Coffee Type). If the value in `I2` is "Rob"`, the value `"Robuster"` is returned. Otherwise, the next IF function is checked. If the value in `I2` is "Exc"`, the value `"Excelser"` is returned. This process continues until all conditions have been checked. If none of the conditions are met, the default value `"Liberica"` is returned.*

7. #### Roast_Type_Name

Analog zu `Coffee Type Name` wird der `Roast Type` ausbuchstabiert.

*The `Roast Type` is spelt out in the same way as `Coffee Type Name`.*

```
WENN(J2="M";"Medium";WENN(J2="L";"Light";WENN(J2="D";"Dark")))
```

8.  #### Loyality_Card 
Hier wird überprüft ob der Kunde eine `Loyality Card` besitzt. 
*This checks whether the customer has a `Loyalty Card`.* 
```
INDEX($customers.I1:I1002;VERGLEICH(1;($customers.A1:A1002=123);0))
```
Diese Formel sucht nach dem Wert in der Zelle `C2` in der Spalte `A` des Bereichs `A1:A1002` in der Kundentabelle. Wenn der Wert gefunden wird, gibt die INDEX-Funktion den Wert aus der entsprechenden Zelle in der Spalte `I` zurück.

*This formula searches for the value in cell `C2` in column `A` of the range `A1:A1002` in the customer table. If the value is found, the INDEX function returns the value from the corresponding cell in column `I`.*



