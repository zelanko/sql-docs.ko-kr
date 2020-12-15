---
description: 'IRowsetFastLoad:: InsertRow (Native Client OLE DB 공급자)'
title: 'IRowsetFastLoad:: InsertRow (Native Client OLE DB 공급자) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- IRowsetFastLoad::InsertRow (OLE DB)
apitype: COM
helpviewer_keywords:
- InsertRow method
ms.assetid: 594d3461-34d2-41e7-8ad4-bd2753601ab6
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 633e9d77a30dae3b140a4b4cf6f8ff36daf402a6
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97462164"
---
# <a name="irowsetfastloadinsertrow-native-client-ole-db-provider"></a>IRowsetFastLoad:: InsertRow (Native Client OLE DB 공급자)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  대량 복사 행 집합에 행을 추가합니다. 샘플은 [IRowsetFastLoad를 사용한 데이터 대량 복사&#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md) 및 [IROWSETFASTLOAD와 ISEQUENTIALSTREAM을 사용하여 SQL SERVER로 BLOB 데이터 전송&#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md)을 참조하세요.  
  
## <a name="syntax"></a>구문  
  
```  
  
HRESULT InsertRow(  
      HACCESSOR hAccessor,  
      void* pData);  
```  
  
## <a name="arguments"></a>인수  
 *hAccessor*[in]  
 대량 복사에 대한 행 데이터를 정의하는 접근자의 핸들입니다. 참조되는 접근자는 행 접근자로, 데이터 값이 포함된 소비자가 소유한 메모리를 바인딩합니다.  
  
 *pData*[in]  
 데이터 값이 포함된 소비자가 소유한 메모리에 대한 포인터입니다. 자세한 내용은 [DBBINDING 구조](/previous-versions/windows/desktop/ms716845(v=vs.85))를 참조하세요.  
  
## <a name="return-code-values"></a>반환 코드 값  
 S_OK  
 메서드가 성공했습니다. 모든 열의 바인딩된 상태 값은 DBSTATUS_S_OK 또는 DBSTATUS_S_NULL입니다.  
  
 E_FAIL  
 오류가 발생했습니다. 행 집합의 오류 인터페이스에서 오류 정보를 볼 수 있습니다.  
  
 E_INVALIDARG  
 *pData* 인수가 NULL 포인터로 설정되었습니다.  
  
 E_OUTOFMEMORY  
 SQLNCLI11에서 요청을 완료하기에 충분한 메모리를 할당할 수 없습니다.  
  
 E_UNEXPECTED  
 이전에 [IRowsetFastLoad::Commit](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-commit-ole-db.md) 메서드에 의해 무효화된 대량 복사 행 집합에서 메서드가 호출되었습니다.  
  
 DB_E_BADACCESSORHANDLE  
 소비자가 제공한 *hAccessor* 인수가 잘못되었습니다.  
  
 DB_E_BADACCESSORTYPE  
 지정된 접근자는 행 접근자가 아니거나, 소비자가 소유한 메모리를 지정하지 않았습니다.  
  
## <a name="remarks"></a>설명  
 소비자 데이터를 열 데이터 형식으로 변환 하는 동안 오류가 발생 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자에서 E_FAIL 반환 됩니다. 모든 **InsertRow** 메서드나 **Commit** 메서드에서만 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 전송할 수 있습니다. 소비자 애플리케이션은 데이터 형식 변환 오류가 있다는 알림을 받기 전에 오류가 있는 데이터로 **InsertRow** 메서드를 여러 번 호출할 수 있습니다. **Commit** 메서드에서 소비자가 모든 데이터를 올바르게 지정했는지 확인하기 때문에 소비자는 필요에 따라 **Commit** 메서드를 적절하게 사용하여 데이터의 유효성을 검사할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자 대량 복사 행 집합은 쓰기 전용입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 행 집합의 소비자 쿼리를 허용 하는 메서드를 노출 하지 않습니다. 처리를 종료하기 위해 소비자는 **Commit** 메서드를 호출하지 않고 [IRowsetFastLoad](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) 인터페이스에서 해당 참조를 해제할 수 있습니다. 행 집합에 있는 소비자가 삽입한 행에 액세스하여 해당 값을 변경하거나 행 집합에서 개별적으로 행을 제거하는 기능은 없습니다.  
  
 대량 복사된 행은 서버에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 맞게 형식이 지정됩니다. 행 형식은 연결이나 세션에 대해 설정된 모든 옵션(예: ANSI_PADDING)의 영향을 받습니다. 이 옵션은 Native Client OLE DB 공급자를 통해 생성 된 모든 연결에 대해 기본적으로 설정 되어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [IRowsetFastLoad &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md)  
  
