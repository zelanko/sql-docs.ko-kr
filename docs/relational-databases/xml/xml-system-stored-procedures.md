---
title: XML 시스템 저장 프로시저 | Microsoft 문서
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- system stored procedures [SQL Server], XML
- sp_xml_removedocument
- OPENXML statement, system stored procedures
- sp_xml_preparedocument
- XML [SQL Server], system stored procedures
ms.assetid: e60c7f85-6823-4d28-93d6-b053d08cc830
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ab7d7429485972d93408dd04023e3f1f6f3c9584
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33013740"
---
# <a name="xml-system-stored-procedures"></a>XML 시스템 저장 프로시저
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  SQL Server는 OPENXML과 함께 사용되는 다음 시스템 저장 프로시저를 제공합니다.  
  
-   [sp_xml_preparedocument&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xml-preparedocument-transact-sql.md)  
  
-   [sp_xml_removedocument&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xml-removedocument-transact-sql.md)  
  
 OPENXML을 사용하여 쿼리를 작성하려면 먼저 **sp_xml_preparedocument**를 호출하여 XML 문서의 내부 표현을 만들어야 합니다. 저장 프로시저는 XML 문서의 내부 표현에 대한 핸들을 반환합니다. 그런 다음 이 핸들은 OPENXML에 전달됩니다. OPENXML은 XPath를 기반으로 문서의 행 집합 뷰를 제공합니다. 특히 OPENXML은 하나의 행 패턴과 하나 이상의 열 패턴입니다.  
  
> [!NOTE]  
>  **sp_xml_preparedocument** 가 반환한 문서 핸들은 세션 기간 동안 유효합니다.  
  
 **sp_xml_removedocument** 시스템 저장 프로시저를 호출하여 XML 문서의 내부 표현을 메모리에서 제거할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [OPENXML&#40;Transact-SQL&#41;](../../t-sql/functions/openxml-transact-sql.md)   
 [OPENXML&#40;SQL Server&#41;](../../relational-databases/xml/openxml-sql-server.md)  
  
  
