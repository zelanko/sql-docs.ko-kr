---
title: 오류 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-ole-db-errors
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- OLE/COM errors
- errors [OLE DB]
- OLE DB error handling, about error handling
- OLE DB error handling
ms.assetid: bd0612f4-96ef-4919-b0f9-b5447210fe93
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f5f0564044ed1f4e7eed39165486350b3e6575d3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="errors"></a>오류
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  OLE/COM 개체는 개체 멤버 함수의 HRESULT 반환 코드를 통해 오류를 보고합니다. OLE/COM HRESULT는 비트 압축 구조입니다. OLE는 구조 멤버를 역참조하는 매크로를 제공합니다.  
  
 OLE/COM 지정는 **IErrorInfo** 인터페이스입니다. 인터페이스와 같은 메서드를 노출 **GetDescription**합니다. 이 인터페이스를 사용하여 클라이언트는 OLE/COM 서버에서 오류 정보를 추출합니다. OLE DB 확장 **IErrorInfo** 단일 멤버 함수를 실행에서 여러 오류 정보 패킷의 반환을 지원 하도록 합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 여러 오류를 반환합니다. 응용 프로그램 호출 하 여 한 번에 하나씩 서버 오류를 검색할 수 [imultipleresults:: Getresult](http://go.microsoft.com/fwlink/?LinkId=129630) ISQLErrorInfo IErrorRecords와 결합 합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 OLE DB 레코드로 향상 된 표시 **IErrorInfo**, 사용자 지정 **ISQLErrorInfo**, 및 공급자 관련 [ISQLServerErrorInfo ](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) error 개체 인터페이스입니다.  
  
 오류 추적에 대 한 정보를 참조 하십시오. [데이터 액세스 추적](http://go.microsoft.com/fwlink/?LinkId=125805)합니다. 에 추가 된 오류 추적 향상 된 기능에 대 한 내용은 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], 참조 [확장 이벤트 로그의 진단 정보에 액세스](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [반환 코드](../../relational-databases/native-client-ole-db-errors/return-codes.md)  
  
-   [오류 인터페이스의 정보](../../relational-databases/native-client-ole-db-errors/information-in-error-interfaces.md)  
  
-   [SQL Server 오류 세부 정보](../../relational-databases/native-client-ole-db-errors/sql-server-error-detail.md)  
  
-   [오류 정보 검색](../../relational-databases/native-client-ole-db-errors/retrieving-error-information.md)  
  
-   [SQL Server 메시지 결과](../../relational-databases/native-client-ole-db-errors/sql-server-message-results.md)  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server Native Client&#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
