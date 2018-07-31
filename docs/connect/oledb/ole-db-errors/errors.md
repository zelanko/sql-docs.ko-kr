---
title: 오류 | Microsoft Docs
description: 오류
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-errors
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- OLE/COM errors
- errors [OLE DB]
- OLE DB error handling, about error handling
- OLE DB error handling
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 477c89e8d058d2f2971dc295c3bf8e1449c5a3d9
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2018
ms.locfileid: "39105859"
---
# <a name="errors"></a>오류
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE/COM 개체는 개체 멤버 함수의 HRESULT 반환 코드를 통해 오류를 보고합니다. OLE/COM HRESULT는 비트 압축 구조입니다. OLE는 구조 멤버를 역참조하는 매크로를 제공합니다.  
  
 OLE/COM은 **IErrorInfo** 인터페이스를 지정합니다. 이 인터페이스는 **GetDescription**과 같은 메서드를 제공합니다. 이 인터페이스를 사용하여 클라이언트는 OLE/COM 서버에서 오류 정보를 추출합니다. OLE DB는 단일 멤버 함수 실행에 대해 여러 개의 오류 정보 패킷 반환을 지원하기 위해 **IErrorInfo**를 확장합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 여러 오류를 반환합니다. 응용 프로그램은 ISQLErrorInfo 및 IErrorRecords를 조합한 [IMultipleResults::GetResult](http://go.microsoft.com/fwlink/?LinkId=129630)를 호출하여 한 번에 하나씩 서버 오류를 검색할 수 있습니다.  
  
 SQL Server용 OLE DB 드라이버는 OLE DB 레코드로 향상된 **IErrorInfo**, 사용자 지정 **ISQLErrorInfo** 및 공급자별 [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) 오류 개체 인터페이스를 제공합니다.  
  
 오류 추적에 대한 자세한 내용은 [데이터 액세스 추적](http://go.microsoft.com/fwlink/?LinkId=125805)을 참조하십시오. 에 추가 하는 오류 추적 향상 기능에 대 한 자세한 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]를 참조 하세요 [확장 이벤트 로그의 진단 정보 액세스](../../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md)합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [반환 코드](../../oledb/ole-db-errors/return-codes.md)  
  
-   [오류 인터페이스의 정보](../../oledb/ole-db-errors/information-in-error-interfaces.md)  
  
-   [SQL Server 오류 세부 정보](../../oledb/ole-db-errors/sql-server-error-detail.md)  
  
-   [오류 정보 검색](../../oledb/ole-db-errors/retrieving-error-information.md)  
  
-   [SQL Server 메시지 결과](../../oledb/ole-db-errors/sql-server-message-results.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 프로그래밍용 OLE DB 드라이버](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
