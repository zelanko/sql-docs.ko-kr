---
title: SQL Server 인덱스를 삭제 하는 중 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- removing indexes
- deleting indexes
- DropIndex function
- dropping indexes
- SQL Server Native Client OLE DB provider, indexes
- indexes [OLE DB]
ms.assetid: add3ba14-10b1-4723-b7c0-3e83689e9fdd
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 38e103cd19950846dd9c88d0b4bdc0d5d385ba1f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36088612"
---
# <a name="dropping-a-sql-server-index"></a>SQL Server 인덱스 삭제
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 노출 된 **iindexdefinition:: Dropindex** 함수입니다. 이렇게 하면 인덱스를 제거 하려면 소비자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블입니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 노출 일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인덱스와 PRIMARY KEY 및 UNIQUE 제약 조건입니다. 테이블 소유자, 데이터베이스 소유자 및 일부 관리 역할 멤버를 수정할 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블, 제약 조건 삭제 합니다. 기본적으로 테이블 소유자만 기존 인덱스를 삭제할 수 있습니다. 따라서 **DropIndex** 표시 된 인덱스의 형식에도 응용 프로그램 사용자의 액세스 권한 뿐만 아니라에 따라 달라 집니다 성공 또는 실패 합니다.  
  
 소비자의 유니코드 문자열에서 테이블 이름을 지정는 *pwszName* 의 멤버는 *uName* 공용 구조체는 *pTableID* 매개 변수입니다. *eKind* 소속 *pTableID* DBKIND_NAME 이어야 합니다.  
  
 인덱스 이름을 유니코드 문자열에으로 지정 하는 소비자는 *pwszName* 의 멤버는 *uName* 공용 구조체의 *pIndexID* 매개 변수. *eKind* 소속 *pIndexID* DBKIND_NAME 이어야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자의 테이블에서 모든 인덱스를 삭제 하는 OLE DB 기능을 지원 하지 않습니다 때 *pIndexID* null입니다. 경우 *pIndexID* 가 null 이면 E_INVALIDARG가 반환 됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [테이블 및 인덱스](tables-and-indexes.md)   
 [ALTER TABLE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)   
 [DROP INDEX&#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-index-transact-sql)  
  
  
