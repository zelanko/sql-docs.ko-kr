---
title: NEWSEQUENTIALID(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- NEWSEQUENTIALID
- NEWSEQUENTIALID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- NEWSEQUENTIALID function
- GUIDs [SQL Server]
ms.assetid: e06d2cab-f1ff-42f1-8550-6aaec57be36f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 19c9caf543f7db84cbf71f76832176118d262f60
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65944178"
---
# <a name="newsequentialid-transact-sql"></a>NEWSEQUENTIALID(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Windows가 시작된 이후에 지정한 컴퓨터에서 이 함수가 이전에 생성한 모든 GUID보다 큰 GUID를 만듭니다. Windows를 다시 시작한 후 GUID가 더 낮은 범위에서 다시 시작될 수 있지만 여전히 전역적으로 고유합니다. GUID 열이 행 식별자로 사용되는 경우 NEWSEQUENTIALID를 사용하면 NEWID 함수를 사용할 때보다 더 빠를 수 있습니다. 그 이유는 NEWID 함수의 경우 임의 작업이 발생하고 캐시된 데이터 페이지를 거의 사용하지 않기 때문입니다. 또한 NEWSEQUENTIALID를 사용하면 데이터 및 인덱스 페이지를 완전히 채울 수 있습니다.  
  
> [!IMPORTANT]  
>  개인 정보 보호가 중요한 경우에는 이 함수를 사용하지 마십시오. 다음번에 생성되는 GUID 값을 추측할 수 있으므로 이 GUID와 관련된 데이터에 액세스할 수 있습니다.  
  
 NEWSEQUENTIALID는 Windows [UuidCreateSequential](https://go.microsoft.com/fwlink/?LinkId=164027) 함수(일부 [바이트 셔플 적용됨](https://blogs.msdn.microsoft.com/dbrowne/2012/07/03/how-to-generate-sequential-guids-for-sql-server-in-net/))에 대한 래퍼입니다.
  
> [!WARNING]  
>  UuidCreateSequential 함수는 하드웨어 종속성이 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터베이스(예: 포함된 데이터베이스)를 다른 컴퓨터로 이동할 때 순차 값의 클러스터가 나타날 수 있습니다. Always On 및 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] 사용 시 데이터베이스가 다른 컴퓨터로 장애 조치되면 순차 값의 클러스터가 나타날 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
NEWSEQUENTIALID ( )  
```  
  
## <a name="return-type"></a>반환 형식  
 **uniqueidentifier**  
  
## <a name="remarks"></a>Remarks  
 NEWSEQUENTIALID()는 **uniqueidentifier** 형식의 테이블 열에서 DEFAULT 제약 조건과 함께만 사용할 수 있습니다. 예를 들어  
  
```  
CREATE TABLE myTable (ColumnA uniqueidentifier DEFAULT NEWSEQUENTIALID());   
```  
  
 DEFAULT 식에서 NEWSEQUENTIALID()를 사용하면 다른 스칼라 연산자와 함께 사용할 수 없습니다. 예를 들어 다음을 실행할 수 없습니다.  
  
```  
CREATE TABLE myTable (ColumnA uniqueidentifier DEFAULT dbo.myfunction(NEWSEQUENTIALID()));  
```  
  
 앞의 예에서 `myfunction()`은 `uniqueidentifier` 값을 받아서 반환하는 사용자 정의 스칼라 함수입니다.  
  
 NEWSEQUENTIALID는 쿼리에서 참조할 수 없습니다.  
  
 NEWSEQUENTIALID를 사용하여 GUID를 생성하면 인덱스의 리프 수준에서 페이지 분할 및 임의 IO를 줄일 수 있습니다.  
  
 NEWSEQUENTIALID를 사용하여 생성된 각 GUID는 해당 컴퓨터에서 고유합니다. NEWSEQUENTIALID를 사용하여 생성된 GUID는 원본 컴퓨터에 네트워크 카드가 있는 경우에만 여러 컴퓨터에서 고유합니다.  
  
## <a name="see-also"></a>참고 항목  
 [NEWID&#40;Transact-SQL&#41;](../../t-sql/functions/newid-transact-sql.md)   
 [비교 연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/comparison-operators-transact-sql.md)  
  
  
