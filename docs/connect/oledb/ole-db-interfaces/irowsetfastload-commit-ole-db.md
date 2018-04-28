---
title: 'Irowsetfastload:: Commit (OLE DB) | Microsoft Docs'
description: IRowsetFastLoad::Commit(OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IRowsetFastLoad::Commit (OLE DB)
apitype: COM
helpviewer_keywords:
- Commit method
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fb4ed770c7f6b3921e2e02aa50aeb2bda44bdda8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="irowsetfastloadcommit-ole-db"></a>IRowsetFastLoad::Commit(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  일괄 삽입되는 행의 끝을 표시하고 행을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블에 씁니다. 샘플을 보려면 [대량 복사 데이터를 사용 하 여 IRowsetFastLoad &#40;OLE DB&#41; ](../../oledb/ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md) 및 [BLOB 데이터를 SQL SERVER를 사용 하 여 IROWSETFASTLOAD 및 ISEQUENTIALSTREAM을 보내기 &#40;OLE DB&#41;](../../oledb/ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
HRESULT Commit(  
      BOOL fDone);  
```  
  
## <a name="arguments"></a>인수  
 *fDone*[in]  
 FALSE인 경우 행 집합은 계속 유효하며 소비자가 행을 추가로 삽입할 수 있습니다. TRUE인 경우 행 집합은 유효하지 않게 되며 소비자가 행을 추가로 삽입할 수 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 S_OK  
 메서드가 성공했으며 삽입한 모든 데이터가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블에 기록되었습니다.  
  
 E_FAIL  
 공급자 관련 오류가 발생했습니다. 오류 정보에서 공급자 관련 오류 텍스트를 검색하십시오.  
  
 E_UNEXPECTED  
 이전에 무효화 된 대량 복사 행 집합에서 호출 되는 **irowsetfastload:: Commit** 메서드.  
  
## <a name="remarks"></a>주의  
 OLE DB Driver for SQL Server 대량 복사 행 집합은 지연 업데이트 모드 행 집합으로 동작합니다. 행 집합을 통해 행 데이터를 삽입 하는 사용자, 삽입 된 행은 처리 되는 동일한 방식으로 삽입 지 원하는 행 집합에서 보류 중인 **IRowsetUpdate**합니다.  
  
 소비자를 호출 해야는 **커밋** 작성 된 행을 삽입된 하는 대량 복사 행 집합에 대 한 메서드는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 동일한 방식으로 테이블의 **irowsetupdate:: Update** 메서드는 보류 중인 행을 제출 하는 데 사용 됩니다는 SQL Server의 인스턴스입니다.  
  
 소비자는 호출 하지 않고 대량 복사 행 집합에서 참조를 해제 하는 경우는 **커밋** 메서드를 삽입된 한 모든 작성 된 적이 없는 행이 손실 됩니다.  
  
 소비자를 호출 하 여 삽입 된 행 일괄 처리 수 있습니다는 **커밋** 메서드는 *fDone* 인수가 FALSE로 설정 합니다. 때 *fDone*가 TRUE로 설정 된 행 집합은 유효 하지 않게 합니다. 잘못 된 대량 복사 행 집합 지원는 **ISupportErrorInfo** 인터페이스 및 **irowsetfastload:: Release** 메서드.  
  
## <a name="see-also"></a>관련 항목:  
 [IRowsetFastLoad &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md)  
  
  
