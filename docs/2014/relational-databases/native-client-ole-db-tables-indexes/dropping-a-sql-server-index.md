---
title: SQL Server 인덱스 삭제 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 148565f2866e571ba783c58d1ff10413510ef6db
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37422232"
---
# <a name="dropping-a-sql-server-index"></a>SQL Server 인덱스 삭제
  합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 노출 하는 **iindexdefinition:: Dropindex** 함수입니다. 이렇게 하면 인덱스를 제거 하려면 소비자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블입니다.  
  
 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인덱스와 PRIMARY KEY 및 UNIQUE 제약 조건입니다. 테이블 소유자, 데이터베이스 소유자 및 일부 관리 역할 멤버를 수정할 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블, 제약 조건 삭제 합니다. 기본적으로 테이블 소유자만 기존 인덱스를 삭제할 수 있습니다. 따라서 **DropIndex** 표시 된 인덱스의 유형에 따라 뿐 아니라 응용 프로그램 사용자의 액세스 권한 뿐만 아니라에 따라 달라 집니다 성공 또는 실패 합니다.  
  
 소비자에서 유니코드 문자열로 테이블 이름을 지정 합니다 *pwszName* 의 멤버는 *uName* 공용 구조체의 *pTableID* 매개 변수입니다. 합니다 *eKind* 소속 *pTableID* DBKIND_NAME 이어야 합니다.  
  
 소비자에서 유니코드 문자열로 인덱스 이름을 지정 합니다 *pwszName* 의 멤버는 *uName* 공용 구조체의 *pIndexID* 매개 변수입니다. 합니다 *eKind* 소속 *pIndexID* DBKIND_NAME 이어야 합니다. 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 테이블에서 모든 인덱스를 삭제는 OLE DB 기능을 지원 하지 않습니다 때 *pIndexID* null입니다. 하는 경우 *pIndexID* 가 null 이면 E_INVALIDARG가 반환 됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [테이블 및 인덱스](tables-and-indexes.md)   
 [ALTER TABLE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)   
 [DROP INDEX&#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-index-transact-sql)  
  
  
