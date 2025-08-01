# Data Alchemy: A Guide to Transforming Raw Text into Gold

This document outlines the entire process followed by a user and the assistant, from parsing raw text to generating a custom-formatted string. It includes the exact prompts that guided each step and shows the complete data output at every stage.

---
<br>

### 1. Initial Data Parsing to a Table 📊

The process began with the user providing a block of unstructured text to be organised into a structured table.

#### The Request 💬
> Parse the given date to a markdown table:
>
> Id 169 Alpha-Num 2 X1PPGROUP.Pgroup_id
> Name 171 Alpha-Num 20 X1PPGROUP.group_name
> Type 191 Alpha-Num 2 X1PPGROUP.type 01=Channel type 02=Host type
> Uptime 193 Alpha-Num 12 Computed, X1PONLPROC.sdate, X1PONLPROC.stime
> TxnInFlight 205 Alpha-Num 10 Computed, ITC/IOS Context file IOS: CT_STAT = “ “ ITC: CC = “ “ within the last hour
> TxnGood 215 Alpha-Num 10 Computed, ITC Context file only ITC: CC like “/% “ within the last hour
> TxnTimeOut 225 Alpha-Num 10 Computed, ITC/IOS Context file IOS: CT_STAT IN (‘0000’, ‘0001’, ‘0002’, ‘1000’, ‘1001’) ITC: CC = “.A01“ within the last hour
> TxnBad 235 Alpha-Num 10 Computed, ITC Context file only ITC: CC like ‘.%’ AND CC!=’.A01’ within the last hour
> TPS 245 Alpha-Num 6 Line Context file of channel interface Compute from completed transactions within the last hour

#### The Transformation ✨
> The assistant interpreted the pattern in the raw text and formatted it into the following complete table.
>
> **_Before: Raw Text 📄_**
> ```
> Id 169 Alpha-Num 2 X1PPGROUP.Pgroup_id
> Name 171 Alpha-Num 20 X1PPGROUP.group_name
> ...
> ```
> <br>
>
 
#### After: Complete Markdown Table 📋

 | Field Name  | Start | Data Type | Length | Source / Computation                                                                                                                  |
 | :---------- | :---- | :-------- | :----- | :------------------------------------------------------------------------------------------------------------------------------------ |
 | **Id** | 169   | Alpha-Num | 2      | `X1PPGROUP.Pgroup_id`                                                                                                                 |
 | **Name** | 171   | Alpha-Num | 20     | `X1PPGROUP.group_name`                                                                                                                |
 | **Type** | 191   | Alpha-Num | 2      | `X1PPGROUP.type` (01=Channel type, 02=Host type)                                                                                      |
 | **Uptime** | 193   | Alpha-Num | 12     | Computed from `X1PONLPROC.sdate`, `X1PONLPROC.stime`                                                                                    |
 | **TxnInFlight** | 205   | Alpha-Num | 10     | Computed from ITC/IOS Context file (IOS: `CT_STAT = " "`, ITC: `CC = " "`) within the last hour.                                         |
 | **TxnGood** | 215   | Alpha-Num | 10     | Computed from ITC Context file only (ITC: `CC` like `"/& "`) within the last hour.                                                      |
 | **TxnTimeOut** | 225   | Alpha-Num | 10     | Computed from ITC/IOS Context file (IOS: `CT_STAT` IN `(‘0000’, ‘0001’, ‘0002’, ‘1000’, ‘1001’)`, ITC: `CC = ".A01"`) within the last hour. |
 | **TxnBad** | 235   | Alpha-Num | 10     | Computed from ITC Context file only (ITC: `CC` like `'.%'` AND `CC!='.A01'`) within the last hour.                                      |
 | **TPS** | 245   | Alpha-Num | 6      | Computed from the Line Context file of the channel interface using completed transactions within the last hour.                       |

---
<br>

### 2. Refining the Table with Specific Headers 🎯

Next, the table structure was refined using a specific set of headers provided by the user.

#### The Request 💬
> Use the headers as headers:
>
> Name Offset Data Type Length Description
> ...

#### The Transformation ✨
The assistant re-parsed the data to align perfectly with the user's required structure, producing a new, more precise table.

> **_Before: First Table ➡️_**
> ```md
> | Field Name  | Start | Data Type | ... |
> | :---------- | :---- | :-------- | :-- |
> ```
> <br>

#### After: Refined Markdown Table ✅

| Name        | Offset | Data Type | Length | Description                                                                                                                   |
| :---------- | :----- | :-------- | :----- | :---------------------------------------------------------------------------------------------------------------------------- |
| Id          | 169    | Alpha-Num | 2      | `X1PPGROUP.Pgroup_id`                                                                                                         |
| Name        | 171    | Alpha-Num | 20     | `X1PPGROUP.group_name`                                                                                                        |
| Type        | 191    | Alpha-Num | 2      | `X1PPGROUP.type` 01=Channel type 02=Host type                                                                                 |
| Uptime      | 193    | Alpha-Num | 12     | Computed, `X1PONLPROC.sdate`, `X1PONLPROC.stime`                                                                                |
| TxnInFlight | 205    | Alpha-Num | 10     | Computed, ITC/IOS Context file IOS: `CT_STAT` = " " ITC: `CC` = " " within the last hour                                        |
| TxnGood     | 215    | Alpha-Num | 10     | Computed, ITC Context file only ITC: `CC` like "/% " within the last hour                                                       |
| TxnTimeOut  | 225    | Alpha-Num | 10     | Computed, ITC/IOS Context file IOS: `CT_STAT` IN (‘0000’, ‘0001’, ‘0002’, ‘1000’, ‘1001’) ITC: `CC` = ".A01“ within the last hour |
| TxnBad      | 235    | Alpha-Num | 10     | Computed, ITC Context file only ITC: `CC` like '.%' AND `CC`!='.A01' within the last hour                                      |
| TPS         | 245    | Alpha-Num | 6      | Line Context file of channel interface Compute from completed transactions within the last hour                               |

---
<br>

### 3. Converting the Table to JSON 🔄

To make the data machine-readable, the visual Markdown table was transformed into a JSON array.

#### The Request 💬
> Parse the table to Json

#### The Transformation ✨
Each row from the Markdown table was converted into a structured object within a JSON array.

> **_Before: Refined Table 📋_**
> ```md
> | Name        | Offset | Data Type | ... |
> | :---------- | :----- | :-------- | :-- |
> ```
<br>

After: Complete JSON with `Description` 📄_**
> ```json
> [
>   {
>     "Name": "Id",
>     "Offset": 169,
>     "Data Type": "Alpha-Num",
>     "Length": 2,
>     "Description": "X1PPGROUP.Pgroup_id"
>   },
>   {
>     "Name": "Name",
>     "Offset": 171,
>     "Data Type": "Alpha-Num",
>     "Length": 20,
>     "Description": "X1PPGROUP.group_name"
>   },
>   {
>     "Name": "Type",
>     "Offset": 191,
>     "Data Type": "Alpha-Num",
>     "Length": 2,
>     "Description": "X1PPGROUP.type 01=Channel type 02=Host type"
>   },
>   {
>     "Name": "Uptime",
>     "Offset": 193,
>     "Data Type": "Alpha-Num",
>     "Length": 12,
>     "Description": "Computed, X1PONLPROC.sdate, X1PONLPROC.stime"
>   },
>   {
>     "Name": "TxnInFlight",
>     "Offset": 205,
>     "Data Type": "Alpha-Num",
>     "Length": 10,
>     "Description": "Computed, ITC/IOS Context file IOS: CT_STAT = \" \" ITC: CC = \" \" within the last hour"
>   },
>   {
>     "Name": "TxnGood",
>     "Offset": 215,
>     "Data Type": "Alpha-Num",
>     "Length": 10,
>     "Description": "Computed, ITC Context file only ITC: CC like \"/% \" within the last hour"
>   },
>   {
>     "Name": "TxnTimeOut",
>     "Offset": 225,
>     "Data Type": "Alpha-Num",
>     "Length": 10,
>     "Description": "Computed, ITC/IOS Context file IOS: CT_STAT IN (‘0000’, ‘0001’, ‘0002’, ‘1000’, ‘1001’) ITC: CC = “.A01“ within the last hour"
>   },
>   {
>     "Name": "TxnBad",
>     "Offset": 235,
>     "Data Type": "Alpha-Num",
>     "Length": 10,
>     "Description": "Computed, ITC Context file only ITC: CC like '.%' AND CC!='.A01' within the last hour"
>   },
>   {
>     "Name": "TPS",
>     "Offset": 245,
>     "Data Type": "Alpha-Num",
>     "Length": 6,
>     "Description": "Line Context file of channel interface Compute from completed transactions within the last hour"
>   }
> ]
> ```

---
<br>

