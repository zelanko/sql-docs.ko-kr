---
title: 오류 인터페이스의 정보 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error interfaces
- ISQLErrorInfo interface
- errors [OLE DB], error interfaces
ms.assetid: 4620f03f-1193-43e7-ba19-ad022737d300
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7a0d18e8adff256ab9bc29e4c763989e008adeec
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87941865"
---
# <a name="information-in-ole-db-defined-error-interfaces"></a>OLE DB 정의 오류 인터페이스의 정보
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 OLE DB 정의 오류 인터페이스 **IErrorInfo**, **Ierrorrecords**및 **ISQLErrorInfo**에 일부 오류 및 상태 정보를 보고 합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 다음과 같이 **IErrorInfo** 멤버 함수를 지원 합니다.  
  
|멤버 함수|Description|  
|---------------------|-----------------|  
|**GetDescription**|설명적인 오류 메시지 문자열입니다.|  
|**GetGUID**|오류를 정의한 인터페이스의 GUID입니다.|  
|**GetHelpContext**|지원되지 않습니다. 항상 0을 반환합니다.|  
|**GetHelpFile**|지원되지 않습니다. 항상 NULL을 반환합니다.|  
|**GetSource**|"Microsoft SQL Server Native Client" 문자열입니다.|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 다음과 같이 소비자가 사용할 수 있는 **Ierrorrecords** 멤버 함수를 지원 합니다.  
  
|멤버 함수|Description|  
|---------------------|-----------------|  
|**GetBasicErrorInfo**|ERRORINFO 구조에 오류에 대한 기본 정보를 채웁니다. ERRORINFO 구조에는 오류에 대한 HRESULT 반환 값을 식별하는 멤버와 오류가 적용되는 공급자 및 인터페이스가 포함됩니다.|  
|**GetCustomErrorObject**|**ISQLErrorInfo** 및 [ISQLServerErrorInfo](https://docs.microsoft.com/sql/connect/oledb/ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db?view=sql-server-ver15) 인터페이스에 대한 참조를 반환합니다.|  
|**GetErrorInfo**|**IErrorInfo** 인터페이스에 대한 참조를 반환합니다.|  
|**GetErrorParameters**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 **geterrorparameters**를 통해 소비자에 게 매개 변수를 반환 하지 않습니다.|  
|**GetRecordCount**|사용할 수 있는 오류 레코드 수입니다.|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 다음과 같이 **ISQLErrorInfo:: GetSQLInfo** 매개 변수를 지원 합니다.  
  
|매개 변수|Description|  
|---------------|-----------------|  
|*pbstrSQLState*|오류의 SQLSTATE 값을 반환합니다. SQLSTATE 값은 SQL-92, ODBC 및 ISO SQL, API 사양에서 정의됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 구현 별 SQLSTATE 값을 정의 하지 않습니다.|  
|*plNativeError*|사용 가능한 경우 **master.dbo.sysmessages**의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 번호를 반환합니다. Native [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client OLE DB 공급자 데이터 원본을 성공적으로 초기화 한 후 네이티브 오류를 사용할 수 있습니다. 시도 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 항상 0을 반환 합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Errors](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
  
