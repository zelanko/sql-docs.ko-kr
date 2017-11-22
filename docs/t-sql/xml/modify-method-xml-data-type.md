---
title: "modify () 메서드 (xml 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- modify() method
- modify method
ms.assetid: 52430735-51f4-46d1-a308-9aecf8648fda
caps.latest.revision: "35"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 4e84f23554fa43f5163b11fe52d0e0ab97835df9
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="modify-method-xml-data-type"></a>modify() 메서드(xml 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  XML 문서의 내용을 수정합니다. 이 메서드를 사용 하 여의 내용을 수정 하는 **xml** 형식 변수 또는 열입니다. 이 메서드는 XML DML 문을 사용하여 XML 데이터에서 노드를 삽입, 업데이트 또는 삭제합니다. **modify ()** 의 메서드는 **xml** UPDATE 문의 SET 절에서 데이터 형식 에서만 사용할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
modify (XML_DML)  
```  
  
## <a name="arguments"></a>인수  
 XML_DML  
 XML DML(데이터 조작 언어)에 있는 문자열입니다. XML 문서는 이 식에 따라 업데이트됩니다.  
  
> [!NOTE]  
>  경우 오류가 반환 되는 **modify ()** 메서드를 null 값에 호출 하거나 null 값을 반환 합니다.  
  
## <a name="examples"></a>예  
 때문에 **modify ()** 방법을 문자열에는 XML DML 데이터 조작 언어 ()에 대 한 샘플을 사용 하려면 **modify ()** XML DML 문을 설명 하는 항목에 포함 됩니다. 이러한 예제를 보려면 [insert&#40; XML DML &#41; ](../../t-sql/xml/insert-xml-dml.md), [delete&#40; XML DML &#41; ](../../t-sql/xml/delete-xml-dml.md) 및 [값으로 &#40; 바꾸기 XML DML &#41; ](../../t-sql/xml/replace-value-of-xml-dml.md).  
  
## <a name="see-also"></a>관련 항목:  
 [XML 데이터 인스턴스 만들기](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 데이터 형식 메서드](../../t-sql/xml/xml-data-type-methods.md)   
 [XML 데이터 수정 언어 &#40; XML DML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
