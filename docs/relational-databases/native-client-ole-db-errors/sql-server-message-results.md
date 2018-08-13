---
title: SQL Server 메시지 결과 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
ms.assetid: 6663c6f9-def1-4d9e-845b-2085e5efc401
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 371183fab5ba9781a425cc757df895fa7311c6d0
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39542234"
---
# <a name="sql-server-message-results"></a>SQL Server 메시지 결과
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 생성 하지 않는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 OLE DB 공급자 행 집합 또는 실행 될 때 행에 영향을.  
  
-   PRINT  
  
-   심각도가 10 이하인 RAISERROR  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 이러한 문은 하나 이상의 정보 메시지를 반환하거나, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 행 집합이나 개수 결과 대신 정보 메시지를 반환하도록 합니다. 성공한 실행에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 OLE DB 공급자는 S_OK를 반환 하 고 메시지를 사용할 수는 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 OLE DB 공급자 소비자.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 OLE DB 공급자 S_OK를 반환 하 고 하나 이상의 정보 메시지 사용할 수 있는 많은 실행에 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 또는 소비자를 실행 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 OLE DB 공급자 구성원 함수입니다.  
  
 해당 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 텍스트의 동적 지정 하므로 네이티브 클라이언트 OLE DB 공급자 소비자 인터페이스 오류 반환 코드, 존재 여부의 반환 된 의값에관계없이모든멤버함수실행후확인**IRowset** 또는 **IMultipleResults** 인터페이스 참조 또는 영향을 받는 행의 수입니다.  
  
## <a name="see-also"></a>관련 항목  
 [오류](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
  
