---
title: SQL Server 메시지 결과 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
ms.assetid: 6663c6f9-def1-4d9e-845b-2085e5efc401
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f5db120da45f57debacd2717983fe4ea4118cabe
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37431842"
---
# <a name="sql-server-message-results"></a>SQL Server 메시지 결과
  다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 생성 하지 않는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 영향을 받는 행 실행할 때 Native Client OLE DB 공급자 행 집합이 나 개수:  
  
-   PRINT  
  
-   심각도가 10 이하인 RAISERROR  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 이러한 문은 하나 이상의 정보 메시지를 반환하거나, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 행 집합이나 개수 결과 대신 정보 메시지를 반환하도록 합니다. 실행에 성공 하면 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 S_OK를 반환 하 고 메시지를 사용할 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 소비자입니다.  
  
 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 S_OK를 반환 있고 하나 이상의 정보 메시지 많은 실행 후 사용 가능한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 또는 소비자 실행을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 멤버 함수입니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 텍스트의 동적 지정을 허용 하는 Native Client OLE DB 공급자 소비자는 반환 코드, 유무 반환된 의의값에관계없이모든멤버함수실행후오류인터페이스를확인해야**IRowset** 나 **IMultipleResults** 인터페이스 참조 또는 영향을 받는 행의 수입니다.  
  
## <a name="see-also"></a>관련 항목  
 [오류](errors.md)  
  
  
