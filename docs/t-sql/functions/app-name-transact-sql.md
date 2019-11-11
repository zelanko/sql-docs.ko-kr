---
title: APP_NAME(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 21b49eb9638b4651ff52c6515f6e5f62177fc504
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843436"
---
# <a name="app_name-transact-sql"></a>APP_NAME(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

이 함수는 애플리케이션이 해당 이름 값을 설정하는 경우 현재 세션의 애플리케이션 이름을 반환합니다.
  
> [!IMPORTANT]  
>  클라이언트는 애플리케이션 이름을 제공하고 `APP_NAME`은 어떤 방식으로도 애플리케이션 이름 값을 확인하지 않습니다. 보안 확인의 일환으로 `APP_NAME`을 사용하지 않습니다.  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
  
APP_NAME  ( )  
```  
  
## <a name="return-types"></a>반환 형식  
**nvarchar(128)**
  
## <a name="remarks"></a>Remarks  
`APP_NAME`을 사용하여 해당 애플리케이션에 대한 다른 작업을 수행하는 방법으로 서로 다른 애플리케이션을 구별합니다. 예를 들어 `APP_NAME`은 각 애플리케이션에 대한 다른 날짜 형식을 허용하도록 서로 다른 애플리케이션을 구별할 수 있습니다. 특정 애플리케이션에 정보 메시지를 반환할 수도 있습니다.
  
[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 애플리케이션 이름을 설정하려면 **데이터베이스 엔진에 연결** 대화 상자에서 **옵션**을 클릭합니다. **추가 연결 매개 변수** 탭에서 `;app='application_name'` 형식에 **앱** 특성을 제공합니다.
  
## <a name="example"></a>예제  
이 예에서는 이 프로세스를 시작한 클라이언트 애플리케이션이 `SQL Server Management Studio` 세션인지 여부를 확인합니다. 그런 다음, US 또는 ANSI 형식으로 날짜 값을 제공합니다.
  
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
[시스템 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)  
[함수](../../t-sql/functions/functions.md)
  
  
