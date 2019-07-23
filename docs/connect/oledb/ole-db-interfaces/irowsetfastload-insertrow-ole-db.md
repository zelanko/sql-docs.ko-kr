---
title: 'IRowsetFastLoad:: InsertRow (OLE DB) | Microsoft Docs'
description: IRowsetFastLoad::InsertRow(OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- IRowsetFastLoad::InsertRow (OLE DB)
apitype: COM
helpviewer_keywords:
- InsertRow method
author: pmasl
ms.author: pelopes
ms.openlocfilehash: b01c63e74ee26cea327a01e3bf9a3595bc5012d8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015455"
---
# <a name="irowsetfastloadinsertrow-ole-db"></a>IRowsetFastLoad::InsertRow(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  대량 복사 행 집합에 행을 추가합니다. 샘플은 [IRowsetFastLoad &#40;OLE DB&#41; 를 사용 하 여 대량 데이터 복사](../../oledb/ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md) 및 [IRowsetFastLoad 및 ISEQUENTIALSTREAM &#40;OLE DB&#41;를 사용 하 여 BLOB 데이터를 SQL SERVER로 전송](../../oledb/ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md)을 참조 하세요.  
  
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
 데이터 값이 포함된 소비자가 소유한 메모리에 대한 포인터입니다. 자세한 내용은 [DBBINDING 구조](https://go.microsoft.com/fwlink/?LinkId=65955)를 참조하세요.  
  
## <a name="return-code-values"></a>반환 코드 값  
 S_OK  
 메서드가 성공했습니다. 모든 열의 바인딩된 상태 값은 DBSTATUS_S_OK 또는 DBSTATUS_S_NULL입니다.  
  
 E_FAIL  
 오류가 발생했습니다. 행 집합의 오류 인터페이스에서 오류 정보를 볼 수 있습니다.  
  
 E_INVALIDARG  
 *pData* 인수가 NULL 포인터로 설정되었습니다.  
  
 E_OUTOFMEMORY  
 MSOLEDBSQL에서 요청을 완료하기에 충분한 메모리를 할당할 수 없었습니다.  
  
 E_UNEXPECTED  
 이전에 [IRowsetFastLoad::Commit](../../oledb/ole-db-interfaces/irowsetfastload-commit-ole-db.md) 메서드에 의해 무효화된 대량 복사 행 집합에서 메서드가 호출되었습니다.  
  
 DB_E_BADACCESSORHANDLE  
 소비자가 제공한 *hAccessor* 인수가 잘못되었습니다.  
  
 DB_E_BADACCESSORTYPE  
 지정된 접근자는 행 접근자가 아니거나, 소비자가 소유한 메모리를 지정하지 않았습니다.  
  
## <a name="remarks"></a>Remarks  
 소비자 데이터를 열의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식으로 변환하는 동안 오류가 발생하면 SQL Server용 OLE DB 드라이버에서 E_FAIL이 반환됩니다. 모든 **InsertRow** 메서드나 **Commit** 메서드에서만 데이터를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]로 전송할 수 있습니다. 소비자 애플리케이션은 데이터 형식 변환 오류가 있다는 알림을 받기 전에 오류가 있는 데이터로 **InsertRow** 메서드를 여러 번 호출할 수 있습니다. **Commit** 메서드에서 소비자가 모든 데이터를 올바르게 지정했는지 확인하기 때문에 소비자는 필요에 따라 **Commit** 메서드를 적절하게 사용하여 데이터의 유효성을 검사할 수 있습니다.  
  
 SQL Server 대량 복사 행 집합에 대 한 OLE DB 드라이버는 쓰기 전용입니다. SQL Server에 대 한 OLE DB 드라이버는 행 집합의 소비자 쿼리를 허용 하는 메서드를 노출 하지 않습니다. 처리를 종료하기 위해 소비자는 **Commit** 메서드를 호출하지 않고 [IRowsetFastLoad](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md) 인터페이스에서 해당 참조를 해제할 수 있습니다. 행 집합에 있는 소비자가 삽입한 행에 액세스하여 해당 값을 변경하거나 행 집합에서 개별적으로 행을 제거하는 기능은 없습니다.  
  
 대량 복사된 행은 서버에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 맞게 형식이 지정됩니다. 행 형식은 연결이나 세션에 대해 설정된 모든 옵션(예: ANSI_PADDING)의 영향을 받습니다. 이 옵션은 SQL Server에 대 한 OLE DB 드라이버를 통해 생성 된 모든 연결에 대해 기본적으로 설정 되어 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [IRowsetFastLoad &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md)  
  
  
