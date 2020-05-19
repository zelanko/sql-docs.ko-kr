---
title: SQL Server 메시지 결과 | Microsoft Docs
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 19c0c3b044943e51c6d791e962fa830f0b6d0144
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704929"
---
# <a name="sql-server-message-results"></a>SQL Server 메시지 결과
  다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 행 집합 또는 실행 시 영향을 받는 행의 수를 생성 하지 않습니다.  
  
-   PRINT  
  
-   심각도가 10 이하인 RAISERROR  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 이러한 문은 하나 이상의 정보 메시지를 반환하거나, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 행 집합이나 개수 결과 대신 정보 메시지를 반환하도록 합니다. 성공적으로 실행 되 면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native client OLE DB 공급자가 S_OK을 반환 하 고, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기본 클라이언트 OLE DB 공급자 소비자가 메시지를 사용할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native client OLE DB 공급자는 S_OK를 반환 하 고, 여러 문을 실행 한 후에 사용할 수 있는 하나 이상의 정보 메시지를 포함 [!INCLUDE[tsql](../../includes/tsql-md.md)] 하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client OLE DB 공급자 멤버 함수의 소비자 실행을 수행 합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]쿼리 텍스트의 동적 지정을 허용 하는 Native Client OLE DB 공급자 소비자는 반환 코드의 값, 반환 된 **IRowset** 또는 **IMultipleResults** 인터페이스 참조가 있는지 여부 또는 영향을 받는 행의 수에 관계 없이 모든 멤버 함수 실행 후 오류 인터페이스를 확인 해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Errors](errors.md)  
  
  
