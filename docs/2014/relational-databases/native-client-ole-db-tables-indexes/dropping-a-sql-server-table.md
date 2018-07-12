---
title: SQL Server 테이블 삭제 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- tables [OLE DB]
- deleting tables
- SQL Server Native Client OLE DB provider, tables
- removing tables
- dropping tables
ms.assetid: b6d6c4de-43c6-473e-92aa-34ffddd58cbe
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c6bb2446d395b7c913653f7ac70805c5b0c5c050
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37408971"
---
# <a name="dropping-a-sql-server-table"></a>SQL Server 테이블 삭제
  합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 노출 하는 **ITableDefinition::DropTable** 함수입니다. 이 통해 제거 하려면 소비자는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의에서 테이블을 합니다.  
  
 소비자에서 유니코드 문자열로 테이블 이름을 지정 합니다 *pwszName* 의 멤버는 *uName* 공용 구조체의 *pTableID* 매개 변수입니다. 합니다 *eKind* 소속 *pTableID* DBKIND_NAME 이어야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [테이블 및 인덱스](tables-and-indexes.md)  
  
  
