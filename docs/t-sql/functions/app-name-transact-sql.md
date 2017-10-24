---
title: APP_NAME (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 35
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c4f63ae216bad0269415ac5e0aa57a7543500f0c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="appname-transact-sql"></a>APP_NAME(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

응용 프로그램에 의해 설정된 경우 현재 세션의 응용 프로그램 이름을 반환합니다.
  
> [!IMPORTANT]  
>  클라이언트가 제공한 응용 프로그램 이름이며 확인되지 않습니다. 사용 하지 마십시오 **APP_NAME** 보안 검사의 일환으로 합니다.  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
  
APP_NAME  ( )  
```  
  
## <a name="return-types"></a>반환 형식  
**nvarchar (128)**
  
## <a name="remarks"></a>주의  
사용 하 여 **APP_NAME** 서로 다른 응용 프로그램에 대 한 다른 작업을 수행 하려는 경우. 예를 들어 다른 응용 프로그램에 대해 날짜 형식을 다르게 지정하거나 특정 응용 프로그램에 정보 메시지를 반환하는 경우입니다.
  
응용 프로그램 이름을 설정 하려면 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에 **데이터베이스 엔진에 연결** 대화 상자를 클릭 **옵션**합니다. 에 **추가 연결 매개 변수** 탭에서 제공 된 **앱** 형식에서 특성`;app='application_name'`
  
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
  
## <a name="see-also"></a>참고 항목
[시스템 함수 &#40; Transact SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
[함수](../../t-sql/functions/functions.md)
  
  

