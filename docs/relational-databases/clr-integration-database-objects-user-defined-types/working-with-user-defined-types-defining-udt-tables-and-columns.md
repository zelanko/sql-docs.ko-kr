---
title: UDT 테이블 및 열 정의 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- user-defined types [CLR integration], columns
- UDTs [CLR integration], columns
- columns [CLR integration]
- user-defined types [CLR integration], tables
- tables [CLR integration]
- UDTs [CLR integration], tables
- UDTs [CLR integration], indexes
- user-defined types [CLR integration], indexes
- indexes [CLR integration]
ms.assetid: aea495f4-ce26-4952-b019-38f012625f3f
author: rothja
ms.author: jroth
ms.openlocfilehash: 116857437426e8736382f80bc8c7107c19056cc3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68028242"
---
# <a name="working-with-user-defined-types---defining-udt-tables-and-columns"></a>사용자 정의 형식 작업 - UDT 테이블 및 열 정의
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  사용자 정의 형식 (UDT)를 포함 하는 어셈블리 정의에 등록 된 후에 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스, 열 정의에 사용할 수 있습니다.  
  
## <a name="creating-tables-with-udts"></a>UDT를 사용하여 테이블 만들기  
 테이블에 UDT 열을 만드는 데 사용하는 특별한 구문은 없습니다. UDT 이름을 기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식처럼 열 정의에 사용하면 됩니다. 다음 CREATE TABLE [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 라는 테이블을 만듭니다 **포인트**, 라는 열을 사용 하 여 **ID** 으로 정의 되어 있는 **int** id 열 및 테이블에 대 한 기본 키입니다. 두 번째 열 이름은 **PointValue**에서의 데이터 형식과 **지점**합니다. 이 예제에 사용 된 스키마 이름이 **dbo**합니다. 스키마 이름을 지정하려면 필요한 권한이 있어야 합니다. 스키마 이름을 생략하면 데이터베이스 사용자에 대한 기본 스키마가 사용됩니다.  
  
```  
CREATE TABLE dbo.Points   
(ID int IDENTITY(1,1) PRIMARY KEY, PointValue Point)  
```  
  
## <a name="creating-indexes-on-udt-columns"></a>UDT 열에 대한 인덱스 만들기  
 UDT 열에 대한 인덱스를 만들 수 있는 옵션은 두 가지가 있습니다.  
  
-   전체 값을 인덱싱합니다. 이 경우 UDT가 이진 순서로 정렬되어 있으면 CREATE INDEX [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용하여 전체 UDT 열에 대해 인덱스를 만들 수 있습니다.  
  
-   UDT 식을 인덱싱합니다. UDT 식을 통해 지속형 계산 열에 대한 인덱스를 만들 수 있습니다. UDT 식은 UDT의 속성, 메서드 또는 필드일 수 있습니다. 식은 결정적이어야 하고 데이터 액세스를 수행하지 않아야 합니다.  
  
 자세한 내용은 [clr user-defined Types](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md) 하 고 [CREATE INDEX &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server의 사용자 정의 형식 작업](../../relational-databases/clr-integration-database-objects-user-defined-types/working-with-user-defined-types-in-sql-server.md)  
  
  
