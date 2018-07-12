---
title: SQL Server 테이블에 열 추가 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- columns [OLE DB]
- AddColumn function
- SQL Server Native Client OLE DB provider, columns
- adding columns
ms.assetid: 22bae18a-bc9d-4617-8660-ed8b17a468d4
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e79886f09783737a392fa67899feb59cd7deb2a1
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37425272"
---
# <a name="adding-a-column-to-a-sql-server-table"></a>SQL Server 테이블에 열 추가
  합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 노출 하는 **ITableDefinition::AddColumn** 함수입니다. 이렇게 하면 소비자가 열을 추가 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블입니다.  
  
 열을 추가 하는 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 소비자는 다음과 같이 제한 됩니다.  
  
-   DBPROP_COL_AUTOINCREMENT가 VARIANT_TRUE이면 DBPROP_COL_NULLABLE은 VARIANT_FALSE여야 합니다.  
  
-   사용 하 여 열이 정의 하는 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **타임 스탬프** 데이터 형식으로 dbprop_col_nullable은 VARIANT_FALSE 여야 합니다.  
  
-   다른 모든 열 정의에서 DBPROP_COL_NULLABLE은 VARIANT_TRUE여야 합니다.  
  
 소비자에서 유니코드 문자열로 테이블 이름을 지정 합니다 *pwszName* 의 멤버는 *uName* 공용 구조체의 *pTableID* 매개 변수입니다. 합니다 *eKind* 소속 *pTableID* DBKIND_NAME 이어야 합니다.  
  
 새 열 이름에 유니코드 문자열로 지정 합니다 *pwszName* 의 멤버는 *uName* 공용 구조체의 *dbcid* DBCOLUMNDESC매개변수의멤버*pColumnDesc*합니다. 합니다 *eKind* 멤버는 DBKIND_NAME 이어야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [테이블 및 인덱스](tables-and-indexes.md)   
 [ALTER TABLE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)  
  
  
