---
title: '@@SERVERNAME (Transact SQL) | Microsoft Docs'
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 525da30f048b8d6ca405783c98eea6bcb0f55671
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="servername-transact-sql"></a>@@SERVERNAME (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  실행 중인 로컬 서버의 이름을 반환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
@@SERVERNAME  
```  
  
## <a name="return-types"></a>반환 형식  
 **nvarchar**  
  
## <a name="remarks"></a>주의  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 설치 중에 서버 이름을 컴퓨터 이름으로 설정합니다. 서버 이름을 변경 하려면 사용 하 여 **sp_addserver**, 한 다음 다시 시작 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
 여러 인스턴스에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] @ 설치@SERVERNAME 설치 후 로컬 서버 이름을 변경 되지 않은 경우 다음과 같은 로컬 서버 이름 정보를 반환 합니다.  
  
|인스턴스|서버 정보|  
|--------------|------------------------|  
|기본 인스턴스|'*servername*'|  
|명명된 인스턴스|'*servername*\\*instancename*'|  
|장애 조치(Failover) 클러스터형 인스턴스 - 기본 인스턴스|'*virtualservername이*'|  
|장애 조치(Failover) 클러스터형 인스턴스 - 명명된 인스턴스|'*virtualservername이*\\*instancename*'|  
  
 하지만 @@SERVERNAME 함수와 SERVERPROPERTY 함수의 SERVERNAME 속성이 비슷한 형식의 문자열을 반환할 수 있습니다, 정보는 다를 수 있습니다. SERVERNAME 속성은 컴퓨터의 네트워크 이름 변경을 자동으로 보고합니다.  
  
 이와 달리 @@SERVERNAME 이런 변경을 보고 하지 않습니다. @@SERVERNAME 사용 하 여 로컬 서버 이름 변경을 보고는 **sp_addserver** 또는 **sp_dropserver** 저장 프로시저입니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [구성 함수&#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [SERVERPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
 [sp_addserver &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)  
  
  
