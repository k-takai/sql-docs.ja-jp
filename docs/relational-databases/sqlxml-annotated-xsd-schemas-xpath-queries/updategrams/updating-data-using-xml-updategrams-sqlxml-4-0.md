---
title: XML アップデート グラム (SQLXML 4.0) を使用してデータの更新 |Microsoft ドキュメント
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDREF type attribute [SQLXML]
- before attribute
- <sync> block
- <after> block
- id attribute
- <before> block
- updg:after attribute
- mapping-schema attribute
- IDREFS type attribute [SQLXML]
- updg:id attribute
- multiple record updates
- after attribute
- updategrams [SQLXML], updating data
- updg:before attribute
- record updates [SQLXML]
ms.assetid: 90ef8a33-5ae3-4984-8259-608d2f1d727f
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e9db70d57cca76574f5f3e5e1aa77decade35392
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "32973727"
---
# <a name="updating-data-using-xml-updategrams-sqlxml-40"></a>XML アップデートグラムを使用した、データの更新 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  既存のデータを更新すると、両方を指定する必要があります、 **\<する前に >** と**\<後 >** ブロックします。 指定した要素を**\<する前に >** と**\<後 >** ブロックが、必要な変更について説明します。 アップデート グラムで指定されている要素を使用して、 **\<する前に >** ブロックをデータベースの既存のレコードを識別します。 対応する要素で、 **\<後 >** ブロックは、更新操作を実行した後、レコードの外観を示します。 この情報から、アップデート グラムが一致する SQL ステートメントを作成、 **\<後 >** ブロックします。 そのステートメントによってデータベースが更新されます。  
  
 更新操作のアップデートグラムの形式は次のとおりです。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync [mapping-schema="SampleSchema.xml"]  >  
   <updg:before>  
      <ElementName [updg:id="value"] .../>  
      [<ElementName [updg:id="value"] .../> ... ]  
   </updg:before>  
   <updg:after>  
      <ElementName [updg:id="value"] ... />  
      [<ElementName [updg:id="value"] .../> ...]  
   </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
 **\<updg:before>**  
 内の要素、 **\<する前に >** ブロックは、データベース テーブルの既存のレコードを識別します。  
  
 **\<updg:after>**  
 内の要素、 **\<後 >** ブロックにレコードを指定する方法を説明する、 **\<する前に >** ブロックは、更新プログラムが適用された後になります。  
  
 **マッピング スキーマ**属性は、アップデート グラムで使用するマッピング スキーマを識別します。 要素と属性名がで指定された、アップデート グラムでマッピング スキーマを指定する場合、 **\<する前に >** と**\<後 >** ブロックは、スキーマの名前と一致する必要があります。 マッピング スキーマでは、これらの要素または属性の名前がデータベース テーブルと列の名前にマップされます。  
  
 アップデートグラムにスキーマを指定しない場合は、アップデートグラムで既定のマッピングが使用されます。 既定のマッピングで、  **\<ElementName >** アップデート グラムで、データベース テーブルにマップし、子要素または属性にマップ、データベースの列で指定します。  
  
 内の要素、 **\<する前に >** ブロックは、データベース内の 1 つのテーブルの行と一致する必要があります。 アップデート グラムがエラーが返され、全体を取り消す場合は、要素は、複数のテーブルの行と一致するか、または任意のテーブルの行と一致しません、 **\<同期 >** ブロックします。  
  
 アップデート グラムでは、複数を含めることができます**\<同期 >** ブロックします。 各**\<同期 >** ブロックはトランザクションとして扱われます。 各**\<同期 >** ブロックでは複数**\<する前に >** と**\<後 >** ブロックします。 たとえば、2 つの既存のレコードを更新する場合可能性がありますを指定する 2 つ**\<する前に >** と**\<後 >** 更新するレコードごとに 1 つのペアします。  
  
## <a name="using-the-updgid-attribute"></a>updg:id 属性の使用  
 複数の要素が指定されている場合、 **\<する前に >** と**\<後 >** 、ブロックを使用して、 **updg:id**属性内の行をマークする、**\<する前に >** と**\<後 >** ブロックします。 処理ロジックでは、この情報を使用して、内のどのレコードを確認、 **\<する前に >** ブロックの組内のレコードと、 **\<後 >** ブロックします。  
  
 **Updg:id**属性は、次のいずれかが存在する場合 (推奨) が必要ではありません。  
  
-   指定したマッピング スキーマ内の要素が、 **sql:key-フィールド**に定義されている属性です。  
  
-   アップデートグラムのキー フィールドに特定の値が 1 つ以上提供されている。  
  
 かどうかかは、アップデート グラムで指定されているキーの列を使用して、 **sql:key-フィールド**内の要素を組み合わせる、 **\<する前に >** と **\<後 >** ブロックします。  
  
 マッピング スキーマでキー列が識別されない場合 (を使用して**sql:key-フィールド**) 必要がありますを指定する場合は、アップデート グラムには、キー列の値が更新中、または**updg:id**です。  
  
 指定されているレコード、 **\<する前に >** と**\<後 >** ブロックは、同じ順序で指定する必要はありません。 **Updg:id**属性で指定されている要素間の関係が強制的、 **\<する前に >** と**\<後 >** ブロックです。  
  
 1 つの要素を指定する場合、 **\<する前に >** ブロックとの対応する要素を 1 つだけ、 **\<後 >** を使用して、ブロック**updg:id**必要はありません。 ただし、これはお勧めを指定する**updg:id**もあいまいにならないようにします。  
  
## <a name="examples"></a>使用例  
 アップデートグラムの例を使用する前に、次のことに注意してください。  
  
-   ほとんどの例では、アップデートグラムでマッピング スキーマを指定せず、既定のマッピングを使用します。 マッピング スキーマを使用するアップデート グラムの例については、次を参照してください。[アップデート グラムの注釈付きマッピング スキーマの指定&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)です。  
  
-   ほとんどの例では、AdventureWorks サンプル データベースを使用します。 すべての更新内容は、このデータベースのテーブルに適用されます。 AdventureWorks データベースは復元できます。  
  
### <a name="a-updating-a-record"></a>A. レコードを更新する  
 次のアップデートグラムでは、AdventureWorks データベースの Person.Contact テーブルで、従業員の姓を Fuller に更新します。 アップデートグラムにマッピング スキーマは指定しないので、既定のマッピングが使用されます。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
<updg:before>  
   <Person.Contact ContactID="1" />  
</updg:before>  
<updg:after>  
   <Person.Contact LastName="Abel-Achong" />  
</updg:after>  
</updg:sync>  
</ROOT>  
```  
  
 記述するレコード、 **\<する前に >** ブロックは、データベースの現在のレコードを表します。 アップデート グラムでは、すべてで指定された列の値を使用、 **\<する前に >** レコードを検索するブロック。 このアップデート グラムで、 **\<する前に >** ブロックは ContactID 列だけを提供する; そのため、アップデート グラムではレコードを検索する値だけを使用します。 仮に、このブロックに LastName 値を追加した場合は、検索に ContactID と LastName の両方の値が使用されます。  
  
 このアップデート グラムで、 **\<後 >** これは変更されている唯一の値であるために、ブロックが LastName 列の値のみを提供します。  
  
##### <a name="to-test-the-updategram"></a>アップデートグラムをテストするには  
  
1.  上のアップデートグラムのテンプレートをコピーして、テキスト ファイルに貼り付け、 UpdateLastName.xml として保存します。  
  
2.  SQLXML 4.0 テスト スクリプト (Sqlxml4test.vbs) を作成し、それを使用してアップデートグラムを実行します。  
  
     詳細については、次を参照してください。 [SQLXML 4.0 クエリの実行に使用する ADO](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)です。  
  
### <a name="b-updating-multiple-records-by-using-the-updgid-attribute"></a>B. updg:id 属性を使用して複数のレコードを更新する  
 この例では、アップデートグラムで、AdventureWorks データベースの HumanResources.Shift テーブルに次の 2 つの更新操作を行います。  
  
-   7:00AM から始まる勤務時間の名前を "Day" から "Early Morning" に変更する。  
  
-   10:00AM から始まる、"Late Morning" という名前の新しい勤務時間を挿入する。  
  
 アップデート グラムで、 **updg:id**属性内の要素間の関連付けの作成、 **\<する前に >** と**\<後 >** ブロックします。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
       <HumanResources.Shift updg:id="x" Name="Day" />  
    </updg:before>  
    <updg:after>  
      <HumanResources.Shift updg:id="y" Name="Late Morning"   
                            StartTime="1900-01-01 10:00:00.000"  
                            EndTime="1900-01-01 18:00:00.000"  
                            ModifiedDate="2004-06-01 00:00:00.000"/>  
      <HumanResources.Shift updg:id="x" Name="Early Morning" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 通知方法、 **updg:id**属性のペアの最初のインスタンス、 \<HumanResources.Shift > 内の要素、 **\<する前に >** の2つ目のインスタンスのブロック\<HumanResources.Shift > 内の要素、 **\<後 >** ブロックします。  
  
##### <a name="to-test-the-updategram"></a>アップデートグラムをテストするには  
  
1.  上のアップデートグラムのテンプレートをコピーして、テキスト ファイルに貼り付け、 UpdateMultipleRecords.xml として保存します。  
  
2.  SQLXML 4.0 テスト スクリプト (Sqlxml4test.vbs) を作成し、それを使用してアップデートグラムを実行します。  
  
     詳細については、次を参照してください。 [SQLXML 4.0 クエリの実行に使用する ADO](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)です。  
  
### <a name="c-specifying-multiple-before-and-after-blocks"></a>C. 複数の指定\<する前に > と\<後 > ブロック  
 あいまいさを避けるためには、作成、アップデート グラムで例 B の複数を使用して、 **\<する前に >** と**\<後 >** ブロックの組。 指定する**\<する前に >** と**\<後 >** ペアは混乱を最小限に抑えて、複数の更新プログラムを指定する 1 つの方法です。 また、各場合の**\<する前に >** と**\<後 >** ブロックが最大で 1 つの要素を指定して、使用する必要はありません、 **updg:id**属性.  
  
> [!NOTE]  
>  、ペアを形成する、 **\<後 >** タグは、それに対応するすぐに従う必要があります**\<する前に >** タグ。  
  
 次のアップデート グラムでは、最初の**\<する前に >** と**\<後 >** ペアは、勤務時間のシフト名を更新します。 2 番目の組によって新しい勤務時間のレコードが挿入されます。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
       <HumanResources.Shift ShiftID="1" Name="Day" />  
    </updg:before>  
    <updg:after>  
      <HumanResources.Shift Name="Early Morning" />  
    </updg:after>  
    <updg:before>  
    </updg:before>  
    <updg:after>  
      <HumanResources.Shift Name="Late Morning"   
                            StartTime="1900-01-01 10:00:00.000"  
                            EndTime="1900-01-01 18:00:00.000"  
                            ModifiedDate="2004-06-01 00:00:00.000"/>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>アップデートグラムをテストするには  
  
1.  上のアップデートグラムのテンプレートをコピーして、テキスト ファイルに貼り付け、 UpdateMultipleBeforeAfter.xml として保存します。  
  
2.  SQLXML 4.0 テスト スクリプト (Sqlxml4test.vbs) を作成し、それを使用してアップデートグラムを実行します。  
  
     詳細については、次を参照してください。 [SQLXML 4.0 クエリの実行に使用する ADO](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)です。  
  
### <a name="d-specifying-multiple-sync-blocks"></a>D. 複数の指定\<sync > ブロック  
 複数を指定することができます**\<同期 >** アップデート グラムではブロックされます。 各**\<同期 >** が指定されているブロックは、独立したトランザクション。  
  
 次のアップデート グラムでは、最初の**\<同期 >** ブロックが、Sales.Customer テーブルのレコードを更新します。 簡素化するため、アップデートグラムでは ID 値 (CustomerID) と更新する値 (SalesPersonID) の 2 つの必要な値だけを指定します。  
  
 2 番目**\<同期 >** ブロックは、Sales.SalesOrderHeader テーブルに 2 つのレコードを追加します。 このテーブルで、SalesOrderID は IDENTITY 型の列です。 したがって、アップデート グラムではない SalesOrderID の値に指定の各、 \<Sales.SalesOrderHeader > 要素。  
  
 倍数を指定する**\<同期 >** ブロック役に立つため場合、2 つ目**\<同期 >** ブロック (トランザクション) は、Sales.SalesOrderHeader テーブルにレコードを追加が失敗した、最初**\<同期 >** ブロックは、Sales.Customer テーブル内の顧客レコードを更新できます。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
      <Sales.Customer CustomerID="1" SalesPersonID="280" />  
    </updg:before>  
    <updg:after>  
      <Sales.Customer CustomerID="1" SalesPersonID="283" />  
    </updg:after>  
  </updg:sync>  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after>  
   <Sales.SalesOrderHeader   
             CustomerID="1"  
             RevisionNumber="1"  
             OrderDate="2004-07-01 00:00:00.000"  
             DueDate="2004-07-13 00:00:00.000"  
             OnlineOrderFlag="0"  
             ContactID="378"  
             BillToAddressID="985"  
             ShipToAddressID="985"  
             ShipMethodID="5"  
             SubTotal="24643.9362"  
             TaxAmt="1971.5149"  
             Freight="616.0984"  
             rowguid="01010101-2222-3333-4444-556677889900"  
             ModifiedDate="2004-07-08 00:00:00.000" />  
   <Sales.SalesOrderHeader  
             CustomerID="1"  
             RevisionNumber="1"  
             OrderDate="2004-07-01 00:00:00.000"  
             DueDate="2004-07-13 00:00:00.000"  
             OnlineOrderFlag="0"  
             ContactID="378"  
             BillToAddressID="985"  
             ShipToAddressID="985"  
             ShipMethodID="5"  
             SubTotal="1000.0000"  
             TaxAmt="0.0000"  
             Freight="0.0000"  
             rowguid="10101010-2222-3333-4444-556677889900"  
             ModifiedDate="2004-07-09 00:00:00.000" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>アップデートグラムをテストするには  
  
1.  上のアップデートグラムのテンプレートをコピーして、テキスト ファイルに貼り付け、 UpdateMultipleSyncs.xml として保存します。  
  
2.  SQLXML 4.0 テスト スクリプト (Sqlxml4test.vbs) を作成し、それを使用してアップデートグラムを実行します。  
  
     詳細については、次を参照してください。 [SQLXML 4.0 クエリの実行に使用する ADO](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)です。  
  
### <a name="e-using-a-mapping-schema"></a>E. マッピング スキーマを使用する  
 この例では、アップデート グラムでスキーマを指定します、マッピングを使用して、**マッピング スキーマ**属性。 ここでは既定のマッピングはなく、アップデートグラム内の要素および属性と、データベースのテーブルおよび列の間の必要なマッピングはマッピング スキーマによって指定します。  
  
 アップデートグラムで指定する要素と属性は、マッピング スキーマ内の要素と属性を参照します。  
  
 次の XSD マッピング スキーマには**\<顧客 >**、 **\<順序 >**、および **\<OD >** 要素にマップされる、データベースの Sales.Customer、Sales.SalesOrderHeader、および Sales.SalesOrderDetail テーブル。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustomerOrder"  
          parent="Sales.Customer"  
          parent-key="CustomerID"  
          child="Sales.SalesOrderHeader"  
          child-key="CustomerID" />  
  
    <sql:relationship name="OrderOD"  
          parent="Sales.SalesOrderHeader"  
          parent-key="SalesOrderID"  
          child="Sales.SalesOrderDetail"  
          child-key="SalesOrderID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer" sql:relation="Sales.Customer" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader"  
                     sql:relationship="CustomerOrder" >  
           <xsd:complexType>  
              <xsd:sequence>  
                <xsd:element name="OD"   
                             sql:relation="Sales.SalesOrderDetail"  
                             sql:relationship="OrderOD" >  
                 <xsd:complexType>  
                  <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
                  <xsd:attribute name="ProductID" type="xsd:integer" />  
                  <xsd:attribute name="UnitPrice" type="xsd:decimal" />  
                  <xsd:attribute name="OrderQty" type="xsd:integer" />  
                  <xsd:attribute name="UnitPriceDiscount" type="xsd:decimal" />   
                 </xsd:complexType>  
                </xsd:element>  
              </xsd:sequence>  
              <xsd:attribute name="CustomerID" type="xsd:string" />  
              <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
              <xsd:attribute name="OrderDate" type="xsd:date" />  
           </xsd:complexType>  
        </xsd:element>  
      </xsd:sequence>  
      <xsd:attribute name="CustomerID"   type="xsd:string" />   
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 このマッピング スキーマ (UpdategramMappingSchema.xml) を次のアップデートグラムで指定します。 このアップデートグラムでは、Sales.SalesOrderDetail テーブルの特定の注文アイテムに、注文明細アイテムを追加します。 アップデート グラムには、入れ子になった要素が含まれています。  **\<OD >** 要素内にネスト、 **\<順序 >** 要素。 これら 2 つの要素の主キーと外部キーのリレーションシップは、マッピング スキーマで指定されます。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync mapping-schema="UpdategramMappingSchema.xml" >  
    <updg:before>  
       <Order SalesOrderID="43659" />  
    </updg:before>  
    <updg:after>  
      <Order SalesOrderID="43659" >  
          <OD ProductID="776" UnitPrice="2329.0000"  
              OrderQty="2" UnitPriceDiscount="0.0" />  
      </Order>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>アップデートグラムをテストするには  
  
1.  上のマッピング スキーマをコピーして、テキスト ファイルに貼り付け、 UpdategramMappingSchema.xml として保存します。  
  
2.  上のアップデートグラムのテンプレートをコピーして、テキスト ファイルに貼り付け、 マッピング スキーマ (UpdategramMappingSchema.xml) と同じフォルダーに UpdateWithMappingSchema.xml として保存します。  
  
3.  SQLXML 4.0 テスト スクリプト (Sqlxml4test.vbs) を作成し、それを使用してアップデートグラムを実行します。  
  
     詳細については、次を参照してください。 [SQLXML 4.0 クエリの実行に使用する ADO](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)です。  
  
 マッピング スキーマを使用するアップデート グラムの例については、次を参照してください。[アップデート グラムの注釈付きマッピング スキーマの指定&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)です。  
  
### <a name="f-using-a-mapping-schema-with-idrefs-attributes"></a>F. マッピング スキーマを IDREFS 属性と共に使用する  
 この例では、アップデートグラムでマッピング スキーマ内の IDREFS 属性を使用して、複数のテーブルのレコードを更新する方法を示します。 この例では、データベースは次のテーブルから構成されるものとします。  
  
-   Student (StudentID、LastName)  
  
-   Course (CourseID、CourseName)  
  
-   Enrollment (StudentID、CourseID)  
  
 学生 (Student) は複数の講座 (Course) に登録できるので、Course には複数の Student を含めることができます。3 番目のテーブル Enrollment は、この M:N リレーションシップを表すために必要です。  
  
 次の XSD マッピング スキーマを使用して、テーブルの XML ビューを提供する、  **\<Student >**、 **\<コース >**、および**\<登録>** 要素。 **IDREFS**マッピング スキーマで属性は、これらの要素間のリレーションシップを指定します。 **StudentIDList**属性を**\<コース >** 要素は、 **IDREFS**属性を Enrollment テーブルの StudentID 列を参照します。 同様に、 **EnrolledIn**属性を **\<Student >** 要素は、 **IDREFS**登録の CourseID 列を参照型の属性テーブルです。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="StudentEnrollment"  
          parent="Student"  
          parent-key="StudentID"  
          child="Enrollment"  
          child-key="StudentID" />  
  
    <sql:relationship name="CourseEnrollment"  
          parent="Course"  
          parent-key="CourseID"  
          child="Enrollment"  
          child-key="CourseID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Course" sql:relation="Course"   
                             sql:key-fields="CourseID" >  
    <xsd:complexType>  
    <xsd:attribute name="CourseID"  type="xsd:string" />   
    <xsd:attribute name="CourseName"   type="xsd:string" />   
    <xsd:attribute name="StudentIDList" sql:relation="Enrollment"  
                 sql:field="StudentID"  
                 sql:relationship="CourseEnrollment"   
                                     type="xsd:IDREFS" />  
  
    </xsd:complexType>  
  </xsd:element>  
  <xsd:element name="Student" sql:relation="Student" >  
    <xsd:complexType>  
    <xsd:attribute name="StudentID"  type="xsd:string" />   
    <xsd:attribute name="LastName"   type="xsd:string" />   
    <xsd:attribute name="EnrolledIn" sql:relation="Enrollment"  
                 sql:field="CourseID"  
                 sql:relationship="StudentEnrollment"   
                                     type="xsd:IDREFS" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 アップデートグラムでこのスキーマを指定して Course テーブルにレコードを挿入すると、Course テーブルには常に新しい講座レコードが挿入されます。 StudentIDList 属性に 1 つ以上の新しい学生 ID を指定すると、アップデートグラムでは Enrollment テーブルにも新しい学生ごとのレコードが挿入され、 重複した値が追加されていないことが Enrollment テーブルで確認されます。  
  
##### <a name="to-test-the-updategram"></a>アップデートグラムをテストするには  
  
1.  仮想ルートに指定したデータベースに、これらのテーブルを作成します。  
  
    ```  
    CREATE TABLE Student(StudentID varchar(10) primary key,   
                         LastName varchar(25))  
    CREATE TABLE Course(CourseID varchar(10) primary key,   
                        CourseName varchar(25))  
    CREATE TABLE Enrollment(StudentID varchar(10)   
                                      references Student(StudentID),  
                           CourseID varchar(10)   
                                      references Course(CourseID))  
    ```  
  
2.  次のサンプル データを追加します。  
  
    ```  
    INSERT INTO Student VALUES ('S1','Davoli')  
    INSERT INTO Student VALUES ('S2','Fuller')  
  
    INSERT INTO Course VALUES  ('CS101', 'C Programming')  
    INSERT INTO Course VALUES  ('CS102', 'Understanding XML')  
  
    INSERT INTO Enrollment VALUES ('S1', 'CS101')  
    INSERT INTO Enrollment VALUES ('S1', 'CS102')  
    ```  
  
3.  上のマッピング スキーマをコピーして、テキスト ファイルに貼り付け、 SampleSchema.xml として保存します。  
  
4.  上の手順のマッピング スキーマと同じフォルダーに、アップデートグラム (SampleUpdategram) を保存します。 このアップデートグラムでは、講座 CS102 から StudentID="1" の学生を削除します。  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
      <updg:sync mapping-schema="SampleSchema.xml" >  
        <updg:before>  
            <Student updg:id="x" StudentID="S1" LastName="Davolio"  
                                 EnrolledIn="CS101 CS102" />  
        </updg:before>  
        <updg:after >  
            <Student updg:id="x" StudentID="S1" LastName="Davolio"  
                                 EnrolledIn="CS101" />  
        </updg:after>  
      </updg:sync>  
    </ROOT>  
    ```  
  
5.  SQLXML 4.0 テスト スクリプト (Sqlxml4test.vbs) を作成し、それを使用してアップデートグラムを実行します。  
  
     詳細については、次を参照してください。 [SQLXML 4.0 クエリの実行に使用する ADO](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)です。  
  
6.  上の手順の説明どおり、次のアップデートグラムを保存して実行します。 このアップデートグラムでは、Enrollment テーブルにレコードを追加し、講義 CS102 に StudentID="1" の学生をもう一度追加します。  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
      <updg:sync mapping-schema="SampleSchema.xml" >  
        <updg:before>  
            <Student updg:id="x" StudentID="S1" LastName="Davolio"  
                                 EnrolledIn="CS101" />  
        </updg:before>  
        <updg:after >  
            <Student updg:id="x" StudentID="S1" LastName="Davolio"  
                                 EnrolledIn="CS101 CS102" />  
        </updg:after>  
      </updg:sync>  
    </ROOT>  
    ```  
  
7.  前の手順の説明どおり、次のアップデートグラムを保存して実行します。 このアップデートグラムでは、新しい学生を 3 人追加し、講座 CS101 に登録します。 ここでもまた、IDREFS リレーションシップによって、Enrollment テーブルにレコードが挿入されます。  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
      <updg:sync mapping-schema="SampleSchema.xml" >  
        <updg:before>  
           <Course updg:id="y" CourseID="CS101"   
                               CourseName="C Programming" />  
        </updg:before>  
        <updg:after >  
           <Student updg:id="x1" StudentID="S3" LastName="Leverling" />  
           <Student updg:id="x2" StudentID="S4" LastName="Pecock" />  
           <Student updg:id="x3" StudentID="S5" LastName="Buchanan" />  
           <Course updg:id="y" CourseID="CS101"  
                               CourseName="C Programming"  
                               StudentIDList="S3 S4 S5" />  
        </updg:after>  
      </updg:sync>  
    </ROOT>  
    ```  
  
 これは、同等の XDR スキーマです。  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <ElementType name="Enrollment" sql:relation="Enrollment" sql:key-fields="StudentID CourseID">  
    <AttributeType name="StudentID" dt:type="id" />  
    <AttributeType name="CourseID" dt:type="id" />  
  
    <attribute type="StudentID" />  
    <attribute type="CourseID" />  
  </ElementType>  
  <ElementType name="Course" sql:relation="Course" sql:key-fields="CourseID">  
    <AttributeType name="CourseID" dt:type="id" />  
    <AttributeType name="CourseName" />  
  
    <attribute type="CourseID" />  
    <attribute type="CourseName" />  
  
    <AttributeType name="StudentIDList" dt:type="idrefs" />  
    <attribute type="StudentIDList" sql:relation="Enrollment" sql:field="StudentID" >  
        <sql:relationship  
                key-relation="Course"  
                key="CourseID"  
                foreign-relation="Enrollment"  
                foreign-key="CourseID" />  
    </attribute>  
  
  </ElementType>  
  <ElementType name="Student" sql:relation="Student">  
    <AttributeType name="StudentID" dt:type="id" />  
     <AttributeType name="LastName" />  
  
    <attribute type="StudentID" />  
    <attribute type="LastName" />  
  
    <AttributeType name="EnrolledIn" dt:type="idrefs" />  
    <attribute type="EnrolledIn" sql:relation="Enrollment" sql:field="CourseID" >  
        <sql:relationship  
                key-relation="Student"  
                key="StudentID"  
                foreign-relation="Enrollment"  
                foreign-key="StudentID" />  
    </attribute>  
  
    <element type="Enrollment" sql:relation="Enrollment" >  
        <sql:relationship key-relation="Student"  
                          key="StudentID"  
                          foreign-relation="Enrollment"  
                          foreign-key="StudentID" />  
    </element>  
  </ElementType>  
  
</Schema>  
```  
  
 マッピング スキーマを使用するアップデート グラムの例については、次を参照してください。[アップデート グラムの注釈付きマッピング スキーマの指定&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)です。  
  
## <a name="see-also"></a>参照  
 [アップデート グラムのセキュリティに関する考慮事項&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
