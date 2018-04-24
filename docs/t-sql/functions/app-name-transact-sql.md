---
title: APP_NAME(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a6bb367cd82ca52e50b6ce6f79d7d0d4897f81ab
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="appname-transact-sql"></a>APP_NAME(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

함수는 응용 프로그램이 해당 이름 값을 설정하는 경우 현재 세션의 응용 프로그램 이름을 반환합니다.
  
> [!IMPORTANT]  
>  클라이언트는 응용 프로그램 이름을 제공하고 응용 프로그램 이름 값은 어떤 방식으로도 확인되지 않습니다. 보안 확인의 일환으로 **APP_NAME**을 사용하지 않습니다.  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
  
APP_NAME  ( )  
```  
  
## <a name="return-types"></a>반환 형식  
**nvarchar(128)**
  
## <a name="remarks"></a>Remarks  
**APP_NAME**을 사용하여 해당 응용 프로그램에 대한 다른 작업을 수행하는 방법으로 서로 다른 응용 프로그램을 구별합니다. 예를 들어 **APP_NAME**은 각 응용 프로그램에 대한 다른 날짜 형식을 허용하도록 서로 다른 응용 프로그램을 구별할 수 있습니다. 특정 응용 프로그램에 정보 메시지를 반환할 수도 있습니다.
  
[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 응용 프로그램 이름을 설정하려면 **데이터베이스 엔진에 연결** 대화 상자에서 **옵션**을 클릭합니다. **추가 연결 매개 변수** 탭에서 `;app='application_name'` 형식에 **앱** 특성을 제공합니다.
  
## <a name="example"></a>예제  
이 예에서는 이 프로세스를 시작한 클라이언트 응용 프로그램이 `SQL Server Management Studio` 세션인지 여부를 확인하고 US 또는 ANSI 형식으로 날짜를 지정합니다.
  
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
  
  
