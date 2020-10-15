---
description: SQL Server Native Client 오류
title: 오류 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- OLE/COM errors
- errors [OLE DB]
- OLE DB error handling, about error handling
- OLE DB error handling
ms.assetid: bd0612f4-96ef-4919-b0f9-b5447210fe93
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f31e215a92ac3c72da4cdd62dbe1b63b43848c5c
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081992"
---
# <a name="sql-server-native-client-errors"></a>SQL Server Native Client 오류
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  OLE/COM 개체는 개체 멤버 함수의 HRESULT 반환 코드를 통해 오류를 보고합니다. OLE/COM HRESULT는 비트 압축 구조입니다. OLE는 구조 멤버를 역참조하는 매크로를 제공합니다.  
  
 OLE/COM은 **IErrorInfo** 인터페이스를 지정합니다. 이 인터페이스는 **GetDescription**과 같은 메서드를 제공합니다. 이 인터페이스를 사용하여 클라이언트는 OLE/COM 서버에서 오류 정보를 추출합니다. OLE DB는 단일 멤버 함수 실행에 대해 여러 개의 오류 정보 패킷 반환을 지원하기 위해 **IErrorInfo**를 확장합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 여러 오류를 반환합니다. 애플리케이션은 ISQLErrorInfo 및 IErrorRecords를 조합한 [IMultipleResults::GetResult](/previous-versions/windows/desktop/ms721289(v=vs.85))를 호출하여 한 번에 하나씩 서버 오류를 검색할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 OLE DB 레코드 강화 **IErrorInfo**, 사용자 지정 **ISQLErrorInfo**및 공급자별 [ISQLServerErrorInfo](../native-client-ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db.md) error 개체 인터페이스를 제공 합니다.  
  
 오류 추적에 대한 자세한 내용은 [데이터 액세스 추적](/previous-versions/sql/sql-server-2008/cc765421(v=sql.100))을 참조하십시오. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에 추가된 오류 추적의 향상된 기능에 대한 자세한 내용은 [확장 이벤트 로그의 진단 정보 액세스](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)를 참조하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [반환 코드](../../relational-databases/native-client-ole-db-errors/return-codes.md)  
  
-   [오류 인터페이스의 정보](../../relational-databases/native-client-ole-db-errors/information-in-error-interfaces.md)  
  
-   [SQL Server 오류 세부 정보](../../relational-databases/native-client-ole-db-errors/sql-server-error-detail.md)  
  
-   [오류 정보 검색](../../relational-databases/native-client-ole-db-errors/retrieving-error-information.md)  
  
-   [SQL Server 메시지 결과](../../relational-databases/native-client-ole-db-errors/sql-server-message-results.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client&#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
