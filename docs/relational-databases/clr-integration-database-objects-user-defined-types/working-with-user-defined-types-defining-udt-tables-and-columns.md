---
title: UDT 테이블 및 열 정의 | 마이크로 소프트 문서
description: UDT 정의가 포함된 어셈블리를 등록한 후 열 정의에서 사용할 수 있습니다.
ms.custom: ''
ms.date: 12/05/2019
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
ms.openlocfilehash: 3f46ebc5089a4cb2fdb974df52d9bc876f925da4
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81486896"
---
# <a name="working-with-user-defined-types---defining-udt-tables-and-columns"></a>사용자 정의 형식 작업 - UDT 테이블 및 열 정의
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  사용자 정의 형식(UDT) 정의를 포함하는 어셈블리가 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 등록되면 열 정의에서 사용할 수 있습니다. 자세한 내용은 [CREATE TYPE(Transact-SQL)](../../t-sql/statements/create-type-transact-sql.md)을 참조하세요.  
  
## <a name="creating-tables-with-udts"></a>UDT를 사용하여 테이블 만들기  
 테이블에 UDT 열을 만드는 데 사용하는 특별한 구문은 없습니다. UDT 이름을 기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식처럼 열 정의에 사용하면 됩니다. 다음 CREATE [!INCLUDE[tsql](../../includes/tsql-md.md)] TABLE 문은 **int** ID 열과 테이블의 기본 키로 정의되는 **ID라는** 열이 있는 **Points라는**테이블을 만듭니다. 두 번째 열의 이름은 **PointValue로**지정되며 데이터 형식은 **Point**입니다. 이 예제에서 사용되는 스키마 이름은 **dbo**입니다. 스키마 이름을 지정하려면 필요한 권한이 있어야 합니다. 스키마 이름을 생략하면 데이터베이스 사용자에 대한 기본 스키마가 사용됩니다.  
  
```sql  
CREATE TABLE dbo.Points   
(ID int IDENTITY(1,1) PRIMARY KEY, PointValue Point)  
```  
  
## <a name="creating-indexes-on-udt-columns"></a>UDT 열에 대한 인덱스 만들기  
 UDT 열에 대한 인덱스를 만들 수 있는 옵션은 두 가지가 있습니다.  
  
-   **전체 값을 인덱싱합니다.** 이 경우 UDT가 이진 순서로 정렬되어 있으면 CREATE INDEX [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용하여 전체 UDT 열에 대해 인덱스를 만들 수 있습니다.  
  
-   **UDT 식을 인덱싱합니다.** UDT 식을 통해 지속형 계산 열에 대한 인덱스를 만들 수 있습니다. UDT 식은 UDT의 속성, 메서드 또는 필드일 수 있습니다. 식은 결정적이어야 하고 데이터 액세스를 수행하지 않아야 합니다.  
  
 자세한 내용은 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQL 서버에서 사용자 정의 유형으로 작업](../../relational-databases/clr-integration-database-objects-user-defined-types/working-with-user-defined-types-in-sql-server.md)     
 [유형 만들기(거래-SQL)](../../t-sql/statements/create-type-transact-sql.md)     
 [CLR 사용자 정의 형식](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)     
