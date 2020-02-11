---
title: UDT 테이블 및 열 정의 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 1b87e497c6610a2d75daa9432246e4f4b4690bab
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62874445"
---
# <a name="defining-udt-tables-and-columns"></a>UDT 테이블 및 열 정의
  UDT (사용자 정의 형식) 정의를 포함 하는 어셈블리를 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 등록 한 후에는 열 정의에서 사용할 수 있습니다.  
  
## <a name="creating-tables-with-udts"></a>UDT를 사용하여 테이블 만들기  
 테이블에 UDT 열을 만드는 데 사용하는 특별한 구문은 없습니다. UDT 이름을 기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식처럼 열 정의에 사용하면 됩니다. 다음 CREATE TABLE [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 id 열로 `int` 정의 된 **Id** 라는 열이 있는 **Points**라는 테이블을 만들고 테이블의 기본 키로 정의 합니다. 두 번째 열은 데이터 형식이 **Point**인 **pointvalue**로 지정 됩니다. 이 예에 사용 된 스키마 이름은 **dbo**입니다. 스키마 이름을 지정하려면 필요한 권한이 있어야 합니다. 스키마 이름을 생략하면 데이터베이스 사용자에 대한 기본 스키마가 사용됩니다.  
  
```  
CREATE TABLE dbo.Points   
(ID int IDENTITY(1,1) PRIMARY KEY, PointValue Point)  
```  
  
## <a name="creating-indexes-on-udt-columns"></a>UDT 열에 대한 인덱스 만들기  
 UDT 열에 대한 인덱스를 만들 수 있는 옵션은 두 가지가 있습니다.  
  
-   전체 값을 인덱싱합니다. 이 경우 UDT가 이진 순서로 정렬되어 있으면 CREATE INDEX [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용하여 전체 UDT 열에 대해 인덱스를 만들 수 있습니다.  
  
-   UDT 식을 인덱싱합니다. UDT 식을 통해 지속형 계산 열에 대한 인덱스를 만들 수 있습니다. UDT 식은 UDT의 속성, 메서드 또는 필드일 수 있습니다. 식은 결정적이어야 하고 데이터 액세스를 수행하지 않아야 합니다.  
  
 자세한 내용은 [CLR 사용자 정의 형식](clr-user-defined-types.md) 및 [CREATE INDEX &#40;transact-sql&#41;](/sql/t-sql/statements/create-index-transact-sql)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQL 서버의 사용자 정의 형식 작업](working-with-user-defined-types-in-sql-server.md)  
  
  
