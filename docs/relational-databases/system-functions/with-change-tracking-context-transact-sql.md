---
title: WITH CHANGE_TRACKING_CONTEXT (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- WITH_CHANGE_TRACKING_CONTEXT_TSQL
- WITH CHANGE_TRACKING_CONTEXT
dev_langs:
- TSQL
helpviewer_keywords:
- WITH CHANGE_TRACKING_CONTEXT
- change tracking [SQL Server], WITH CHANGE_TRACKING_CONTEXT
ms.assetid: 885e33a1-602a-4b94-8380-a63ac935a683
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: aa900fcf6bd142c5f3d5eddde85df0a41419efa1
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85752820"
---
# <a name="with-change_tracking_context-transact-sql"></a>WITH CHANGE_TRACKING_CONTEXT(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  데이터가 변경된 경우 주관자 ID와 같은 변경 컨텍스트가 지정되도록 설정합니다. 예를 들어 변경 내용 추적을 사용할 경우 애플리케이션은 애플리케이션 자체의 변경 내용과 애플리케이션 외부 데이터의 변경 내용을 구분할 수 있습니다.  

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
WITH CHANGE_TRACKING_CONTEXT ( context )  
```  
  
#### <a name="parameters"></a>매개 변수  
 *context*  
 호출 애플리케이션에서 제공되고 변경에 대한 변경 내용 추적 정보와 함께 저장되는 컨텍스트 정보입니다. *context* 가 **varbinary (128)** 입니다.  
  
 값은 상수 또는 변수가 될 수 있지만 NULL이 될 수는 없습니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 데이터 변경에 대한 변경 내용 추적 컨텍스트를 설정합니다.  
  
```  
WITH CHANGE_TRACKING_CONTEXT ( context )  
```  
  
## <a name="see-also"></a>참고 항목  
 [변경 내용 추적 함수 &#40;Transact-sql&#41;](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)   
 [CHANGETABLE &#40;Transact-sql&#41;](../../relational-databases/system-functions/changetable-transact-sql.md)   
 [데이터 변경 내용 추적&#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
  
