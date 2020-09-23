---
title: SQL Server 오류 정보(OLE DB 드라이버)
description: SQL Server 오류에 대한 세부 정보를 반환하는 OLE DB Driver for SQL Server의 공급자별 오류 인터페이스 ISQLServerErrorInfo에 대해 알아봅니다.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- errors [OLE DB], error details
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error details
- ISQLServerErrorInfo interface
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f532b124fa23a65a71480b4bcb1bf31272a3081e
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862227"
---
# <a name="sql-server-error-detail"></a>SQL Server 오류 세부 정보
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server는 공급자 관련 오류 인터페이스인 [ISQLServerErrorInfo](https://docs.microsoft.com/sql/connect/oledb/ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db?view=sql-server-ver15)를 정의합니다. 이 인터페이스는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 오류에 대한 세부 정보를 반환하며 명령 실행이나 행 집합 작업이 실패할 경우에 유용합니다.  
  
 **ISQLServerErrorInfo** 인터페이스에 액세스하는 두 가지 방법이 있습니다.  
  
 소비자는 다음 코드 예제와 같이 **IErrorRecords::GetCustomerErrorObject**를 호출하여 **ISQLServerErrorInfo** 포인터를 얻을 수 있습니다. (**ISQLErrorInfo**를 얻을 필요는 없습니다.) **ISQLErrorInfo** 및 **ISQLServerErrorInfo**는 모두 사용자 지정 OLE DB 오류 개체이고, **ISQLServerErrorInfo**는 프로시저 이름 및 줄 번호와 같은 세부 정보를 비롯하여 서버 오류 정보를 얻기 위해 사용하는 인터페이스입니다.  
  
```  
// Get the SQL Server custom error object.  
if(FAILED(hr=pIErrorRecords->GetCustomErrorObject(  
   nRec, IID_ISQLServerErrorInfo,  
   (IUnknown**)&pISQLServerErrorErrorInfo)))  
```  
  
 **ISQLServerErrorInfo** 포인터를 가져오는 다른 방법은 이미 얻은 **ISQLErrorInfo** 포인터에서 **QueryInterface** 메서드를 호출하는 것입니다. **ISQLServerErrorInfo**에는 **ISQLErrorInfo**에서 사용할 수 있는 정보의 상위 집합이 포함되어 있으므로 **GetCustomerErrorObject**를 통해 **ISQLServerErrorInfo**로 직접 이동하는 것이 좋습니다.  
  
 **ISQLServerErrorInfo** 인터페이스는 멤버 함수 [ISQLServerErrorInfo::GetErrorInfo](../../oledb/ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db.md)를 노출합니다. 이 함수는 SSERRORINFO 구조에 대한 포인터와 문자열 버퍼에 대한 포인터를 반환합니다. 두 포인터는 모두 소비자가 **IMalloc::Free** 메서드를 사용하여 할당 취소해야 하는 메모리를 참조합니다.  
  
 SSERRORINFO 구조 멤버는 소비자에 의해 다음과 같이 해석됩니다.  
  
|멤버|Description|  
|------------|-----------------|  
|*pwszMessage*|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 오류 메시지입니다. **IErrorInfo::GetDescription**에 반환된 문자열과 같습니다.|  
|*pwszServer*|세션에 대한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|  
|*pwszProcedure*|해당되는 경우 오류가 발생한 프로시저의 이름입니다. 그렇지 않으면 빈 문자열입니다.|  
|*lNative*|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]원시 오류 번호입니다. **ISQLErrorInfo::GetSQLInfo**의 *plNativeError* 매개 변수에 반환된 값과 같습니다.|  
|*bState*|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 오류 메시지의 상태입니다.|  
|*bClass*|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 오류 메시지의 심각도입니다.|  
|*wLineNumber*|해당되는 경우 오류가 발생한 저장 프로시저의 줄 번호입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [오류](../../oledb/ole-db-errors/errors.md)   
 [RAISERROR&#40;Transact-SQL&#41;](../../../t-sql/language-elements/raiserror-transact-sql.md)  
  
  
