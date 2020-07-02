---
title: NULL 처리 (SQLXML)
description: 'Updg: nullvalue 특성을 사용 하 여 SQLXML 4.0 updategram에서 NULL 특성 또는 요소를 지정 하는 방법에 대해 알아봅니다.'
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- updg:nullvalue attribute
- updategrams [SQLXML], null values
- nullvalue attribute
- null values [SQLXML]
ms.assetid: 5e11eebb-d94e-4ce6-a6d0-870225706bc1
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 57a0517bc698d2969d1ee1808cb52769fa8ef4ae
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85790574"
---
# <a name="null-handling-sqlxml-40"></a>NULL 처리(SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  XML 구문에서는 NULL을 부재로 해석합니다. 예를 들어 특성 또는 요소 값이 NULL 이면 해당 특성이 나 요소가 XML 문서에 없는 것입니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)]SQLXML에서 **updg: nullvalue** 특성은 요소 또는 특성 값에 NULL을 지정할 수 있도록 합니다.  
  
 예를 들어 다음 updategram은 **ContactID** 가 64 인 연락처의 **TITLE** 값이 NULL 인지 확인 하 고 **title** 값을 "Mr"로 업데이트 합니다. 업데이트합니다.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync updg:nullvalue="IsNULL"  >  
    <updg:before>  
       <Person.Contact ContactID="64" Title="IsNULL" />  
    </updg:before>  
    <updg:after>  
       <Person.Contact ContactID="64" Title="Mr." />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 매개 변수가 Updategram으로 전달되는 경우 NULL도 매개 변수 값으로 전달될 수 있습니다. 이 작업은 블록에서 **nullvalue** 특성을 지정 하 여 수행 됩니다 **\<updg:header>** . 예제는 [Updategrams &#40;SQLXML 4.0&#41;에 매개 변수 전달 ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/passing-parameters-to-updategrams-sqlxml-4-0.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Updategram 보안 고려 사항은 SQLXML 4.0&#41;&#40;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
