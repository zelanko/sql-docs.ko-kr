---
title: APP_NAME(Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- APP_NAME_TSQL
- APP_NAME
dev_langs:
- TSQL
helpviewer_keywords:
- name checking for current session [SQL Server]
- sessions [SQL Server], application names
- applications [SQL Server], names
- current session application names
- APP_NAME function
ms.assetid: e491e192-9b30-4243-bc19-33c133fe08a8
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b2b65f2380cc52c7a1d084dedad5fdb744d377bf
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="appname-transact-sql"></a>APP_NAME(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

응용 프로그램에 의해 설정된 경우 현재 세션의 응용 프로그램 이름을 반환합니다.
  
> [!IMPORTANT]  
>  클라이언트가 제공한 응용 프로그램 이름이며 확인되지 않습니다. 보안 확인의 일환으로 **APP_NAME**을 사용하지 않습니다.  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
  
APP_NAME  ( )  
```  
  
## <a name="return-types"></a>반환 형식  
**nvarchar(128)**
  
## <a name="remarks"></a>Remarks  
다른 응용 프로그램에 대해 다른 작업을 수행하려면 **APP_NAME**을 사용하세요. 예를 들어 다른 응용 프로그램에 대해 날짜 형식을 다르게 지정하거나 특정 응용 프로그램에 정보 메시지를 반환하는 경우입니다.
  
[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 응용 프로그램 이름을 설정하려면 **데이터베이스 엔진에 연결** 대화 상자에서 **옵션**을 클릭합니다. **추가 연결 매개 변수** 탭에서 `;app='application_name'` 형식에 **앱** 특성을 제공합니다.
  
## <a name="examples"></a>예  
다음 예에서는 이 프로세스를 시작한 클라이언트 응용 프로그램이 `SQL Server Management Studio` 세션인지 여부를 확인하고 US 또는 ANSI 형식으로 날짜를 지정합니다.
  
```sql
USE AdventureWorks2012;  
GO  
IF APP_NAME() = 'Microsoft SQL Server Management Studio - Query'  
PRINT 'This process was started by ' + APP_NAME() + '. The date is ' + CONVERT ( varchar(100) , GETDATE(), 101) + '.';  
ELSE   
PRINT 'This process was started by ' + APP_NAME() + '. The date is ' + CONVERT ( varchar(100) , GETDATE(), 102) + '.';  
GO  
```  
  
## <a name="see-also"></a>관련 항목:
[시스템 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
[함수](../../t-sql/functions/functions.md)
  
  
