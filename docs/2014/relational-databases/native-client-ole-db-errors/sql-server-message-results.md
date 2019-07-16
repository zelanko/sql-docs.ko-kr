---
title: SQL Server 메시지 결과 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
ms.assetid: 6663c6f9-def1-4d9e-845b-2085e5efc401
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ff604f4c5d66a5742868e25ba05ca6b4528ddb1a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68206714"
---
# <a name="sql-server-message-results"></a>SQL Server 메시지 결과
  다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 생성 하지 않는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 OLE DB 공급자 행 집합 또는 실행 될 때 행에 영향을.  
  
-   PRINT  
  
-   심각도가 10 이하인 RAISERROR  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 이러한 문은 하나 이상의 정보 메시지를 반환하거나, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 행 집합이나 개수 결과 대신 정보 메시지를 반환하도록 합니다. 실행에 성공 하면 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 S_OK를 반환 하 고 메시지를 사용할 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 소비자입니다.  
  
 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 S_OK를 반환 있고 하나 이상의 정보 메시지 많은 실행 후 사용 가능한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 또는 소비자 실행을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 멤버 함수입니다.  
  
 해당 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 텍스트의 동적 지정 하므로 네이티브 클라이언트 OLE DB 공급자 소비자 인터페이스 오류 반환 코드, 존재 여부의 반환 된 의값에관계없이모든멤버함수실행후확인**IRowset** 또는 **IMultipleResults** 인터페이스 참조 또는 영향을 받는 행의 수입니다.  
  
## <a name="see-also"></a>관련 항목  
 [오류](errors.md)  
  
  
