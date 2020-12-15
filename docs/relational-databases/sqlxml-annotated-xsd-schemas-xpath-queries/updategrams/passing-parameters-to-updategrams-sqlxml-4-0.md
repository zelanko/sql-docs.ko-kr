---
title: Updategrams에 매개 변수 전달 (SQLXML)
description: SQLXML 4.0에서 updategram에 매개 변수를 전달 하는 방법에 대해 알아봅니다.
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- nullvalue attribute
- passing parameters [SQLXML]
- parameters [SQLXML]
- updategrams [SQLXML], passing parameters
- null values [SQLXML]
ms.assetid: 2354e6e7-1860-471f-8711-4e374c5a4ed2
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 129fceaeac7de8ca1ab44ff181dd0971b3744fa5
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97473104"
---
# <a name="passing-parameters-to-updategrams-sqlxml-40"></a>Updategram에 매개 변수 전달(SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Updategram은 템플릿이므로 Updategram에 매개 변수를 전달할 수 있습니다. 템플릿에 매개 변수를 전달 하는 방법에 대 한 자세한 내용은 [Updategram 보안 고려 사항 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)를 참조 하세요.  
  
 Updategram을 사용하면 NULL을 매개 변수 값으로 전달할 수 있습니다. NULL 매개 변수 값을 전달 하려면 **nullvalue** 특성을 지정 합니다. 그러면 **nullvalue** 특성에 할당 된 값이 매개 변수 값으로 제공 됩니다. Updategram은 이 값을 NULL로 처리합니다.  
  
> [!NOTE]  
>  **\<sql:header>** 및에서는 **\<updg:header>** **nullvalue** 를 정규화 되지 않은 값으로 지정 해야 합니다. 반면에서는 **\<updg:sync>** **nullvalue** 를 정규화 된 값으로 지정 합니다 (예 **: updg: nullvalue**).  
  
## <a name="examples"></a>예  
 다음 예제를 사용 하 여 작업 예제를 만들려면 [SQLXML 예를 실행 하기 위한 요구 사항](../../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)에 지정 된 요구 사항을 충족 해야 합니다.  
  
 Updategram 예를 사용하기 전에 다음 사항을 확인하십시오.  
  
-   이 예에서는 기본 매핑을 사용합니다. 즉, Updategram에 매핑 스키마가 지정되지 않습니다. 매핑 스키마를 사용 하는 updategram의 추가 예제는 [Updategram &#40;SQLXML 4.0&#41;에서 주석이 추가 된 매핑 스키마 지정 ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)을 참조 하세요.  
  
### <a name="a-passing-parameters-to-an-updategram"></a>A. Updategram에 매개 변수 전달  
 이 예에서 Updategram은 HumanResources.Shift 테이블에 있는 직원의 성을 변경합니다. Updategram에는 두 개의 매개 변수인 ShiftID이 전달 됩니다 .이 매개 변수는 shift 및 Name을 고유 하 게 식별 하는 데 사용 됩니다.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:header>  
  <updg:param name="ShiftID"/>  
  <updg:param name="Name" />  
</updg:header>  
  <updg:sync >  
    <updg:before>  
       <HumanResources.Shift ShiftID="$ShiftID" />  
    </updg:before>  
    <updg:after>  
      <HumanResources.Shift Name="$Name" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Updategram을 테스트하려면  
  
1.  위의 Updategram을 메모장에 복사하고 UpdategramWithParameters.xml로 파일에 저장합니다.  
  
2.  다음 줄을 추가 하 여 updategram를 실행 하기 위해 [ADO를 사용 하 여 sqlxml 4.0 쿼리를 실행](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md) 하는 sqlxml 4.0 테스트 스크립트 (Sqlxml4test.vbs)를 준비 합니다 `cmd.Properties("Output Stream").Value = outStream` .  

    ```  
    cmd.NamedParameters = True  
    ' CreateParameter arguments: Name, Type, Direction, Size, Value  
    cmd.Parameters.Append cmd.CreateParameter("@ShiftID",  2, 1,  0, 1)  
    cmd.Parameters.Append cmd.CreateParameter("@Name",   200, 1, 50, "New Name")  
    ```  
  
### <a name="b-passing-null-as-a-parameter-value-to-an-updategram"></a>B. NULL을 매개 변수 값으로 Updategram에 전달  
 Updategram을 실행하면 NULL로 설정할 매개 변수에 "isnull" 값이 할당됩니다. Updategram은 "isnulll" 매개 변수 값을 NULL로 변환하고 적절하게 처리합니다.  
  
 다음 Updategram에서는 직원 직함을 NULL로 설정합니다.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:header nullvalue="isnull" >  
  <updg:param name="EmployeeID"/>  
  <updg:param name="ManagerID" />  
</updg:header>  
  <updg:sync >  
    <updg:before>  
       <HumanResources.Employee EmployeeID="$EmployeeID" />  
    </updg:before>  
    <updg:after>  
      <HumanResources.Employee ManagerID="$ManagerID" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Updategram을 테스트하려면  
  
1.  위의 Updategram을 메모장에 복사하고 UpdategramPassingNullvalues.xml로 파일에 저장합니다.  
  
2.  다음 줄을 추가 하 여 updategram를 실행 하기 위해 [ADO를 사용 하 여 sqlxml 4.0 쿼리를 실행](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md) 하는 sqlxml 4.0 테스트 스크립트 (Sqlxml4test.vbs)를 준비 합니다 `cmd.Properties("Output Stream").Value = outStream` .  
  
    ```  
    cmd.NamedParameters = True  
    ' CreateParameter arguments: Name, Type, Direction, Size, Value   
    cmd.Parameters.Append cmd.CreateParameter("@EmployeeID", 3, 1, 0, 1)  
    cmd.Parameters.Append cmd.CreateParameter("@ManagerID",  3, 1, 0, Null)  
    ```  
  
## <a name="see-also"></a>참고 항목  
 [Updategram 보안 고려 사항은 SQLXML 4.0&#41;&#40;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
