---
title: '@@SERVERNAME (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- '@@SERVERNAME'
- '@@SERVERNAME_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@SERVERNAME function'
- local servers [SQL Server]
ms.assetid: b0ef33fb-954a-4294-b05b-a87c14ce25a3
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 7b59ab089a0e2782a326d2d3f913f109869ef32f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="x40x40servername-transact-sql"></a>&#x40;&#x40;SERVERNAME(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]을 실행하는 로컬 서버의 이름을 반환합니다.  

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]

 ![문서 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
@@SERVERNAME  
```  
  
## <a name="return-types"></a>반환 형식  
 **nvarchar**  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 설치 중에 서버 이름을 컴퓨터 이름으로 설정합니다. 서버 이름을 변경하려면 **sp_addserver**를 사용한 다음, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]을 다시 시작합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 여러 인스턴스가 설치되어 있는 경우 로컬 서버 이름이 설치 후 변경되지 않으면 @@SERVERNAME은 다음 로컬 서버 이름 정보를 반환합니다.  
  
|인스턴스|서버 정보|  
|--------------|------------------------|  
|기본 인스턴스|'*servername*'|  
|명명된 인스턴스|'*servername*\\*instancename*'|  
|장애 조치(failover) 클러스터형 인스턴스 - 기본 인스턴스|'*virtualservername*'|  
|장애 조치(failover) 클러스터형 인스턴스 - 명명된 인스턴스|'*virtualservername*\\*instancename*'|  
  
 @@SERVERNAME 함수와 SERVERPROPERTY 함수의 SERVERNAME 속성이 비슷한 형식의 문자열을 반환하더라도 정보는 다를 수 있습니다. SERVERNAME 속성은 컴퓨터의 네트워크 이름 변경을 자동으로 보고합니다.  
  
 이와 달리 @@SERVERNAME은 이런 변경을 보고하지 않습니다. @@SERVERNAME은 **sp_addserver** 또는 **sp_dropserver** 저장 프로시저를 사용하여 로컬 서버 이름 변경을 보고합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `@@SERVERNAME`를 사용하는 방법을 보여 줍니다.  
  
```  
SELECT @@SERVERNAME AS 'Server Name'  
```  
  
 결과 집합의 예는 다음과 같습니다.  
  
```  
Server Name  
---------------------------------  
ACCTG  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [구성 함수&#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [SERVERPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
 [sp_addserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)  
  
  
