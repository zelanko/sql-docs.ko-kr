---
title: 오류 인터페이스의 정보 | Microsoft Docs
description: 오류 인터페이스의 정보
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error interfaces
- ISQLErrorInfo interface
- errors [OLE DB], error interfaces
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 4ff18864e37575f78d129abb1569b0ffe83d4685
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67994936"
---
# <a name="information-in-error-interfaces"></a>오류 인터페이스의 정보
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  SQL Server용 OLE DB 드라이버는 OLE DB에서 정의된 오류 인터페이스 **IErrorInfo**, **IErrorRecords** 및 **ISQLErrorInfo**의 몇 가지 오류 및 상태 정보를 보고합니다.  
  
 SQL Server에 대 한 OLE DB 드라이버는 다음과 같이 **IErrorInfo** 멤버 함수를 지원 합니다.  
  
|멤버 함수|설명|  
|---------------------|-----------------|  
|**GetDescription**|설명적인 오류 메시지 문자열입니다.|  
|**GetGUID**|오류를 정의한 인터페이스의 GUID입니다.|  
|**GetHelpContext**|지원되지 않습니다. 항상 0을 반환합니다.|  
|**GetHelpFile**|지원되지 않습니다. 항상 NULL을 반환합니다.|  
|**GetSource**|“SQL Server용 Microsoft OLE DB 드라이버” 문자열입니다.|  
  
 SQL Server에 대 한 OLE DB 드라이버는 다음과 같이 소비자가 사용할 수 있는 **Ierrorrecords** 멤버 함수를 지원 합니다.  
  
|멤버 함수|설명|  
|---------------------|-----------------|  
|**GetBasicErrorInfo**|ERRORINFO 구조에 오류에 대한 기본 정보를 채웁니다. ERRORINFO 구조에는 오류에 대한 HRESULT 반환 값을 식별하는 멤버와 오류가 적용되는 공급자 및 인터페이스가 포함됩니다.|  
|**GetCustomErrorObject**|**ISQLErrorInfo** 및 [ISQLServerErrorInfo](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) 인터페이스에 대한 참조를 반환합니다.|  
|**GetErrorInfo**|**IErrorInfo** 인터페이스에 대한 참조를 반환합니다.|  
|**GetErrorParameters**|SQL Server에 대 한 OLE DB 드라이버는 **Geterrorparameters**를 통해 소비자에 게 매개 변수를 반환 하지 않습니다.|  
|**GetRecordCount**|사용할 수 있는 오류 레코드 수입니다.|  
  
 SQL Server에 대 한 OLE DB 드라이버는 다음과 같이 **ISQLErrorInfo:: GetSQLInfo** 매개 변수를 지원 합니다.  
  
|매개 변수|설명|  
|---------------|-----------------|  
|*pbstrSQLState*|오류의 SQLSTATE 값을 반환합니다. SQLSTATE 값은 SQL-92, ODBC 및 ISO SQL, API 사양에서 정의됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 및 SQL Server 정의 된 구현 별 SQLSTATE 값에 대 한 OLE DB 드라이버는 아닙니다.|  
|*plNativeError*|사용 가능한 경우 **master.dbo.sysmessages**의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 오류 번호를 반환합니다. 기본 오류는 SQL Server 데이터 원본에 대 한 OLE DB 드라이버를 초기화 하는 데 성공한 후에 사용할 수 있습니다. 시도 하기 전에 SQL Server에 대 한 OLE DB 드라이버는 항상 0을 반환 합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [오류](../../oledb/ole-db-errors/errors.md)  
  
  
