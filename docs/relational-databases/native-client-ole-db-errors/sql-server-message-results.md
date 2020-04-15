---
title: SQL Server 메시지 결과 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
ms.assetid: 6663c6f9-def1-4d9e-845b-2085e5efc401
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 577b609fd2f878e6c97010cac004e0b10b3a4e4e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300980"
---
# <a name="sql-server-message-results"></a>SQL Server 메시지 결과
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 네이티브 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 OLE DB 공급자 행 집합 또는 실행 될 때 영향을 받는 행의 수를 생성 하지 않습니다.  
  
-   PRINT  
  
-   심각도가 10 이하인 RAISERROR  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 이러한 문은 하나 이상의 정보 메시지를 반환하거나, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 행 집합이나 개수 결과 대신 정보 메시지를 반환하도록 합니다. 성공적인 실행시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 OLE DB 공급자는 S_OK 반환하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메시지는 네이티브 클라이언트 OLE DB 공급자 소비자가 사용할 수 있습니다.  
  
 네이티브 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 OLE DB 공급자는 S_OK 반환하며 많은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 OLE DB 공급자 함수의 소비자 실행 후 사용할 수 있는 하나 이상의 정보 메시지가 있습니다.  
  
 쿼리 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 텍스트의 동적 사양을 허용하는 네이티브 클라이언트 OLE DB 공급자 소비자는 반환 코드값, 반환된 **IRowset** 또는 **IMultipleResults** 인터페이스 참조또는 영향을 받는 행의 수에 관계없이 모든 멤버 함수 실행 후 오류 인터페이스를 확인해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [오류](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
  
