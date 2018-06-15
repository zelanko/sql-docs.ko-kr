---
title: NULL 처리 (SQLXML 4.0) | Microsoft Docs
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
- updg:nullvalue attribute
- updategrams [SQLXML], null values
- nullvalue attribute
- null values [SQLXML]
ms.assetid: 5e11eebb-d94e-4ce6-a6d0-870225706bc1
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b53c3516dbe0ee87e23e9cb13ec441ef82a499c8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32968898"
---
# <a name="null-handling-sqlxml-40"></a>NULL 처리(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XML 구문에서는 NULL을 부재로 해석합니다. 예를 들어 특성 또는 요소 값이 NULL이면 해당 특성이나 요소가 XML 문서에 없습니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML에는 **updg: nullvalue** 특성을 사용 하는 요소 또는 특성 값에 NULL을 지정 합니다.  
  
 예를 들어 다음 updategram 되도록는 **제목** 연락처에 대 한 값 **ContactID** 64가 NULL 인 한 다음 업데이트는 **제목** 값을 "Mr." 업데이트합니다.  
  
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
  
 매개 변수가 Updategram으로 전달되는 경우 NULL도 매개 변수 값으로 전달될 수 있습니다. 지정 하 여 이렇게는 **nullvalue** 특성에  **\<updg:header >** 블록입니다. 예를 들어 참조 [Updategram에 매개 변수 전달 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/passing-parameters-to-updategrams-sqlxml-4-0.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Updategram 보안 고려 사항 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
