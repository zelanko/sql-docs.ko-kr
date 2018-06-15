---
title: SQL Server 오류 세부 정보 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-errors
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- errors [OLE DB], error details
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error details
- ISQLServerErrorInfo interface
ms.assetid: 51500ee3-3d78-47ec-b90f-ebfc55642e06
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7dbaa5d805b8b1102e07b0e63bf269129077e539
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32945148"
---
# <a name="sql-server-error-detail"></a>SQL Server 오류 세부 정보
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 공급자별 오류 인터페이스를 정의 [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1)합니다. 이 인터페이스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류에 대한 세부 정보를 반환하며 명령 실행이나 행 집합 작업이 실패할 경우에 유용합니다.  
  
 두 가지 방법으로 액세스 권한을 얻을 수 **ISQLServerErrorInfo** 인터페이스입니다.  
  
 소비자를 호출할 수 있습니다 **ierrorrecords:: Getcustomererrorobject** 얻으려고는 **ISQLServerErrorInfo** 다음 코드 예제에 나와 있는 것 처럼 포인터입니다. (가져올 필요가 없습니다 **ISQLErrorInfo.**) 둘 다 **ISQLErrorInfo** 및 **ISQLServerErrorInfo** 와 사용자 지정 OLE DB 오류 개체는 **ISQLServerErrorInfo** 프로시저 이름 및 줄 번호와 같은 세부 정보를 포함 하 여 서버 오류 정보를 얻기 위해 사용 하는 인터페이스입니다.  
  
```  
// Get the SQL Server custom error object.  
if(FAILED(hr=pIErrorRecords->GetCustomErrorObject(  
   nRec, IID_ISQLServerErrorInfo,  
   (IUnknown**)&pISQLServerErrorErrorInfo)))  
```  
  
 가져오는 다른 방법은 **ISQLServerErrorInfo** 포인터를 호출 하는 **QueryInterface** 메서드를 이미 얻은 **ISQLErrorInfo** 포인터입니다. 되므로 **ISQLServerErrorInfo** 에서 사용할 수 있는 정보의 상위 집합이 포함 되어 **ISQLErrorInfo**, 바로 이동할 수는 의미가 **ISQLServerErrorInfo** 통해 **GetCustomerErrorObject**합니다.  
  
 **ISQLServerErrorInfo** 인터페이스 멤버 함수를 노출 [isqlservererrorinfo:: Geterrorinfo](../../relational-databases/native-client-ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db.md)합니다. 이 함수는 SSERRORINFO 구조에 대한 포인터와 문자열 버퍼에 대한 포인터를 반환합니다. 소비자를 사용 하 여 할당 취소 해야 하는 메모리를 참조 하는 두 포인터는 **imalloc:: Free** 메서드.  
  
 SSERRORINFO 구조 멤버는 소비자에 의해 다음과 같이 해석됩니다.  
  
|멤버|Description|  
|------------|-----------------|  
|*pwszMessage*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 메시지입니다. 반환 된 문자열과 동일한 **ierrorinfo:: Getdescription**합니다.|  
|*pwszServer*|세션에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|  
|*pwszProcedure*|해당되는 경우 오류가 발생한 프로시저의 이름입니다. 그렇지 않으면 빈 문자열입니다.|  
|*lNative*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]원시 오류 번호입니다. 반환 된 값과 동일한 지는 *plNativeError* 의 매개 변수 **isqlerrorinfo:: Getsqlinfo**합니다.|  
|*bState*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 메시지의 상태입니다.|  
|*bClass*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 메시지의 심각도입니다.|  
|*wLineNumber*|해당되는 경우 오류가 발생한 저장 프로시저의 줄 번호입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [오류](../../relational-databases/native-client-ole-db-errors/errors.md)   
 [Raiserror& #40; Transact SQL & #41;](../../t-sql/language-elements/raiserror-transact-sql.md)  
  
  
