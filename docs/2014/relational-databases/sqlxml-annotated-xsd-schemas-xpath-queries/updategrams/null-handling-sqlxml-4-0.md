---
title: NULL 처리 (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 11f7ca96ca65ae23202b84030140e0eaef945de2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66014685"
---
# <a name="null-handling-sqlxml-40"></a>NULL 처리(SQLXML 4.0)
  XML 구문에서는 NULL을 부재로 해석합니다. 예를 들어 특성 또는 요소 값이 NULL 이면 해당 특성이 나 요소가 XML 문서에 없는 것입니다. SQLXML [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 에서는 특성을 `updg:nullvalue` 사용 하 여 요소 또는 특성 값에 NULL을 지정할 수 있습니다.  
  
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
  
 매개 변수가 Updategram으로 전달되는 경우 NULL도 매개 변수 값으로 전달될 수 있습니다. 이 작업을 수행하려면 `nullvalue` 블록에 `<updg:header>` 특성을 지정합니다. 예제는 [Updategrams &#40;SQLXML 4.0&#41;에 매개 변수 전달 ](passing-parameters-to-updategrams-sqlxml-4-0.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Updategram 보안 고려 사항은 SQLXML 4.0&#41;&#40;](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
