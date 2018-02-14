---
title: "&lt;xsd:redefine&gt; 요소 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- xsd:redefine element
ms.assetid: 5f3e9b65-f10e-4db2-a62c-b270ac11d04e
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3865dc2690b6d78acb0d24fc5190ab394dfc0a83
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/12/2018
---
# <a name="the-ltxsdredefinegt-element"></a>&lt;xsd:redefine&gt; 요소
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
W3C XSD **redefine** 요소를 사용하면 스키마 구성 요소를 다시 정의할 수 있습니다. 그러나 이러한 지시어를 지원하려면 성능 비용이 많이 들 수 있으며 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 다시 정의된 스키마와 연결된 **xml** 데이터 형식의 모든 인스턴스에 대해 유효성을 다시 검사해야 합니다. 따라서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 이 요소를 지원하지 않습니다. **\<xsd:redefine>** 요소를 포함하는 XML 스키마는 서버에서 거부됩니다.  
  
 스키마나 해당 구성 요소를 업데이트하려면 대신 다음을 수행합니다.  
  
1.  수정한 스키마 구성 요소를 사용하여 XML 스키마 컬렉션을 새로 만듭니다.  
  
2.  새 XML 스키마 컬렉션을 대신 사용하도록 다시 정의되기 위해 XML 스키마 컬렉션을 사용하는 모든 **xml** 데이터 형식(XML DT)을 다시 입력합니다. 이 작업을 수행하려면 ALTER TABLE 명령의 ALTER COLUMN 옵션을 사용하여 열을 다시 입력하거나 변수나 매개 변수에 XML 스키마 컬렉션 제약 조건을 변경합니다.  
  
3.  XML 스키마 컬렉션의 이전 버전을 삭제합니다.  
  
## <a name="see-also"></a>참고 항목  
 [서버의 XML 스키마 컬렉션에 대한 요구 사항 및 제한 사항](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
