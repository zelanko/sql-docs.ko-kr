---
title: ISQLServerErrorInfo::GetErrorInfo(OLE DB 드라이버) | Microsoft Docs
description: ISQLServerErrorInfo::GetErrorInfo 메서드가 SQL Server 오류 정보를 포함하는 OLE DB Driver for SQL Server SSERRORINFO 구조체에 대한 포인터를 반환하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISQLServerErrorInfo::GetErrorInfo (OLE DB)
apitype: COM
helpviewer_keywords:
- GetErrorInfo method
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e6c025b5832299867be8b611756b5e15d54109c2
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88860084"
---
# <a name="isqlservererrorinfogeterrorinfo-ole-db"></a>ISQLServerErrorInfo::GetErrorInfo(OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 오류 정보가 포함된 OLE DB Driver for SQL Server SSERRORINFO에 대한 포인터를 반환합니다.  
  
 OLE DB Driver for SQL Server는 **ISQLServerErrorInfo** 오류 인터페이스를 정의합니다. 이 인터페이스는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 오류의 심각도 및 상태를 비롯하여 오류에 대한 자세한 정보를 반환합니다.  

  
## <a name="syntax"></a>구문  
  
```  
  
HRESULT GetErrorInfo(  
   SSERRORINFO**ppSSErrorInfo,  
   OLECHAR**ppErrorStrings);  
```  
  
## <a name="arguments"></a>인수  
 *ppSSErrorInfo*[out]  
 SSERRORINFO 구조에 대한 포인터입니다. 메서드가 실패하거나 오류와 연관된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 정보가 없는 경우 공급자는 메모리를 할당하지 않고 출력에서 *ppSSErrorInfo* 인수가 Null 포인터인지 확인합니다.  
  
 *ppErrorStrings*[out]  
 유니코드 문자열 포인터에 대한 포인터입니다. 메서드가 실패하거나 오류와 연관된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 정보가 없는 경우 공급자는 메모리를 할당하지 않고 출력에서 *ppErrorStrings* 인수가 Null 포인터인지 확인합니다. **IMalloc::Free** 메서드를 사용하여 *ppErrorStrings* 인수를 해제하면 메모리가 블록에 할당될 때 반환된 SSERRORINFO 구조에 있는 세 개의 각 문자열 멤버가 해제됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 S_OK  
 메서드가 성공했습니다.  
  
 E_INVALIDARG  
 *ppSSErrorInfo* 또는 *ppErrorStrings* 인수는 NULL입니다.  
  
 E_OUTOFMEMORY  
 OLE DB Driver for SQL Server에서 요청을 완료하기에 충분한 메모리를 할당할 수 없습니다.  
  
## <a name="remarks"></a>설명  
 SQL Server용 OLE DB 드라이버가 소비자에 의해 전달된 포인터를 통해 반환된 SSERRORINFO 및 OLECHAR 문자열을 위한 메모리를 할당했습니다. 소비자는 오류 데이터에 액세스할 필요가 없게 되면 **IMalloc::Free** 메서드를 사용하여 이 메모리의 할당을 취소해야 합니다.  
  
 SSERRORINFO 구조는 다음과 같이 정의됩니다.  
  
```  
typedef struct tagSSErrorInfo  
   {  
   LPOLESTR pwszMessage;  
   LPOLESTR pwszServer;  
   LPOLESTR pwszProcedure;  
   LONG lNative;  
   BYTE bState;  
   BYTE bClass;  
   WORD wLineNumber;  
   }  
SSERRORINFO;  
```  
  
|멤버|Description|  
|------------|-----------------|  
|*pwszMessage*|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 전달하는 오류 메시지입니다. 이 메시지는 **IErrorInfo::GetDescription** 메서드를 통해 반환됩니다.|  
|*pwszServer*|오류가 발생한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|  
|*pwszProcedure*|오류가 저장 프로시저에서 발생한 경우에는 오류를 생성한 저장 프로시저의 이름이고, 그렇지 않으면 빈 문자열입니다.|  
|*lNative*|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 오류 번호입니다. 오류 번호는 **ISQLErrorInfo::GetSQLInfo** 메서드의 *plNativeError* 매개 변수에 반환되는 번호와 동일합니다.|  
|*bState*|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 오류의 상태입니다.|  
|*bClass*|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 오류의 심각도입니다.|  
|*wLineNumber*|해당되는 경우 오류 메시지가 발생한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 저장 프로시저의 줄입니다. 저장 프로시저가 연관되지 않은 경우 기본값은 1입니다.|  
  
 *ppErrorStrings* 인수에 반환된 문자열의 구조 참조 주소에 있는 포인터입니다.  
  
## <a name="see-also"></a>참고 항목  
 [ISQLServerErrorInfo &#40;OLE DB&#41;](https://docs.microsoft.com/sql/connect/oledb/ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db?view=sql-server-ver15)   
 [RAISERROR&#40;Transact-SQL&#41;](../../../t-sql/language-elements/raiserror-transact-sql.md)  
  
  
