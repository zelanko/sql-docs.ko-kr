---
description: sp_xml_removedocument(Transact-SQL)
title: sp_xml_removedocument (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_xml_removedocument_TSQL
- sp_xml_removedocument
dev_langs:
- TSQL
helpviewer_keywords:
- sp_xml_removedocument
ms.assetid: f9dca50a-8baf-4170-90bc-e72783ce5b73
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 42f4c9f09846d590752e282dc19af9312236cecd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463963"
---
# <a name="sp_xml_removedocument-transact-sql"></a>sp_xml_removedocument(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  문서 핸들로 지정된 XML 문서의 내부 표현을 제거하고 문서 핸들을 무효로 만듭니다.  
  
> [!NOTE]  
>  구문 분석된 문서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 내부 캐시에 저장됩니다. MSXML 파서(Msxmlsql.dll)는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 사용할 수 있는 총 메모리의 8분의 1을 사용합니다. 메모리 부족을 방지 하려면 **sp_xml_removedocument** 를 실행 하 여 메모리를 확보 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_xml_removedocument hdoc  
```  
  
## <a name="arguments"></a>인수  
 *hdoc*  
 새로 생성된 문서의 핸들입니다. 유효하지 않은 핸들은 오류를 반환합니다. *hdoc* 는 정수입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0 (성공) 또는 >0 (실패)  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 XML 문서의 내부 표현을 제거합니다. 문서의 핸들은 입력으로 제공됩니다.  
  
```  
EXEC sp_xml_removedocument @hdoc;  
```  
  
## <a name="see-also"></a>참고 항목      
 <br>[시스템 저장 프로시저 (Transact-sql)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)
 <br>[XML 저장 프로시저 (Transact-sql)](../../relational-databases/system-stored-procedures/xml-stored-procedures-transact-sql.md)
 <br>[sys. dm_exec_xml_handles (Transact-sql)](../system-dynamic-management-views/sys-dm-exec-xml-handles-transact-sql.md)
 <br>[sp_xml_preparedocument (Transact-sql)](../../relational-databases/system-stored-procedures/sp-xml-preparedocument-transact-sql.md)
 <br>[OPENXML(Transact-SQL)](../../t-sql/functions/openxml-transact-sql.md)
  
  
