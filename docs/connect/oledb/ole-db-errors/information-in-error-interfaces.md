---
title: 오류 인터페이스의 정보 | Microsoft Docs
description: 오류 인터페이스의 정보
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-errors
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error interfaces
- ISQLErrorInfo interface
- errors [OLE DB], error interfaces
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 732dc76e63b1503aa0294a3381b53f592fbf25ce
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="information-in-error-interfaces"></a>오류 인터페이스의 정보
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  OLE DB Driver for SQL Server OLE DB에서 정의 된 오류 인터페이스에서 일부 오류 및 상태 정보를 보고 **IErrorInfo**, **IErrorRecords**, 및 **ISQLErrorInfo**합니다.  
  
 OLE DB driver for SQL Server **IErrorInfo** 멤버는 다음과 같이 작동 합니다.  
  
|멤버 함수|설명|  
|---------------------|-----------------|  
|**GetDescription**|설명적인 오류 메시지 문자열입니다.|  
|**GetGUID**|오류를 정의한 인터페이스의 GUID입니다.|  
|**GetHelpContext**|지원되지 않습니다. 항상 0을 반환합니다.|  
|**GetHelpFile**|지원되지 않습니다. 항상 NULL을 반환합니다.|  
|**GetSource**|문자열 "Microsoft OLE DB Driver for SQL Server"입니다.|  
  
 OLE DB Driver for SQL Server 소비자가 사용할 수 있는 지원 **IErrorRecords** 멤버는 다음과 같이 작동 합니다.  
  
|멤버 함수|설명|  
|---------------------|-----------------|  
|**GetBasicErrorInfo**|ERRORINFO 구조에 오류에 대한 기본 정보를 채웁니다. ERRORINFO 구조에는 오류에 대한 HRESULT 반환 값을 식별하는 멤버와 오류가 적용되는 공급자 및 인터페이스가 포함됩니다.|  
|**GetCustomErrorObject**|인터페이스에 대 한 참조를 반환 **ISQLErrorInfo,** 및 [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1)합니다.|  
|**GetErrorInfo**|에 대 한 참조를 반환 된 **IErrorInfo** 인터페이스입니다.|  
|**GetErrorParameters**|OLE DB Driver for SQL Server를 통해 소비자에 게 매개 변수를 반환 하지 않는 **GetErrorParameters**합니다.|  
|**GetRecordCount**|사용할 수 있는 오류 레코드 수입니다.|  
  
 OLE DB driver for SQL Server **isqlerrorinfo:: Getsqlinfo** 다음과 같이 매개 변수입니다.  
  
|매개 변수|설명|  
|---------------|-----------------|  
|*pbstrSQLState*|오류의 SQLSTATE 값을 반환합니다. SQLSTATE 값은 SQL-92, ODBC 및 ISO SQL, API 사양에서 정의됩니다. 모두 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 또는 OLE DB Driver for SQL Server 구현 별 SQLSTATE 값을 정의 합니다.|  
|*plNativeError*|반환 된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 오류 번호를 **master.dbo.sysmessages** 사용 가능한 경우. 네이티브 오류를 성공적으로 초기화는 OLE DB Driver for SQL Server 데이터 원본에 사용할 수 있습니다. 초기화 전에 OLE DB Driver for SQL Server 항상 0을 반환 합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [오류](../../oledb/ole-db-errors/errors.md)  
  
  
