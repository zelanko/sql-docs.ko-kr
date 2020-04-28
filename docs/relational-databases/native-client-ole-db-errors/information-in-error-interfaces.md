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
ms.openlocfilehash: a19a2189aa28bb5ebf50a0533ed4bfb30b52deea
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306116"
---
# <a name="information-in-error-interfaces"></a>오류 인터페이스의 정보
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Native [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client OLE DB 공급자는 OLE DB 정의 오류 인터페이스 **IErrorInfo**, **ierrorrecords**및 **ISQLErrorInfo**에 일부 오류 및 상태 정보를 보고 합니다.  
  
 Native [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client OLE DB 공급자는 다음과 같이 **IErrorInfo** 멤버 함수를 지원 합니다.  
  
|멤버 함수|설명|  
|---------------------|-----------------|  
|**GetDescription**|설명적인 오류 메시지 문자열입니다.|  
|**GetGUID**|오류를 정의한 인터페이스의 GUID입니다.|  
|**GetHelpContext**|지원 안 됨 항상 0을 반환합니다.|  
|**GetHelpFile**|지원 안 됨 항상 NULL을 반환합니다.|  
|**GetSource**|"Microsoft SQL Server Native Client" 문자열입니다.|  
  
 Native [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client OLE DB 공급자는 다음과 같이 소비자가 사용할 수 있는 **ierrorrecords** 멤버 함수를 지원 합니다.  
  
|멤버 함수|설명|  
|---------------------|-----------------|  
|**GetBasicErrorInfo**|ERRORINFO 구조에 오류에 대한 기본 정보를 채웁니다. ERRORINFO 구조에는 오류에 대한 HRESULT 반환 값을 식별하는 멤버와 오류가 적용되는 공급자 및 인터페이스가 포함됩니다.|  
|**GetCustomErrorObject**|**ISQLErrorInfo** 및 [ISQLServerErrorInfo](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) 인터페이스에 대한 참조를 반환합니다.|  
|**GetErrorInfo**|**IErrorInfo** 인터페이스에 대한 참조를 반환합니다.|  
|**GetErrorParameters**|Native [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client OLE DB 공급자는 **geterrorparameters**를 통해 소비자에 게 매개 변수를 반환 하지 않습니다.|  
|**GetRecordCount**|사용할 수 있는 오류 레코드 수입니다.|  
  
 Native [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client OLE DB 공급자는 다음과 같이 **ISQLErrorInfo:: GetSQLInfo** 매개 변수를 지원 합니다.  
  
|매개 변수|설명|  
|---------------|-----------------|  
|*pbstrSQLState*|오류의 SQLSTATE 값을 반환합니다. SQLSTATE 값은 SQL-92, ODBC 및 ISO SQL, API 사양에서 정의됩니다. 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLE DB 공급자는 구현 별 SQLSTATE 값을 정의 하지 않습니다.|  
|*plNativeError*|사용 가능한 경우 **master.dbo.sysmessages**의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 번호를 반환합니다. Native Client OLE DB 공급자 데이터 원본을 성공적으로 초기화 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 한 후 네이티브 오류를 사용할 수 있습니다. 시도 전에 Native Client OLE DB 공급자 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 항상 0을 반환 합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [오류](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
  
