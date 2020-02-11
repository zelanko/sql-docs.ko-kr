---
title: IRowsetFastLoad (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- IRowsetFastLoad interface
ms.assetid: d19a7097-48d9-409a-aff9-277891b7aca7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 35cee52e9a85989123bcb10d998d37ce86a28601
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63209820"
---
# <a name="irowsetfastload-ole-db"></a>IRowsetFastLoad(OLE DB)
  인터페이스 `IRowsetFastLoad` 는 메모리 기반 대량 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복사 작업에 대 한 지원을 노출 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자 소비자는 인터페이스를 사용 하 여 기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 데이터를 빠르게 추가 합니다.  
  
 세션에 대해 SSPROP_ENABLEFASTLOAD를 VARIANT_TRUE로 설정하면 해당 세션에서 반환된 행 집합의 데이터를 읽을 수 없습니다. SSPROP_ENABLEFASTLOAD를 VARIANT_TRUE로 설정하면 세션에서 생성되는 모든 행 집합이 IRowsetFastLoad 형식으로 설정되는데, IRowsetFastLoad 행 집합은 행 집합 인출 기능을 지원하지 않기 때문에 이러한 행 집합의 데이터는 읽을 수 없습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|방법|Description|  
|------------|-----------------|  
|[IRowsetFastLoad:: Commit &#40;OLE DB&#41;](irowsetfastload-commit-ole-db.md)|일괄 삽입되는 행의 끝을 표시하고 행을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 씁니다.|  
|[IRowsetFastLoad:: InsertRow &#40;OLE DB&#41;](irowsetfastload-insertrow-ole-db.md)|대량 복사 행 집합에 행을 추가합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [인터페이스 &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)   
 [IRowsetFastLoad &#40;OLE DB을 사용 하 여 대량 데이터 복사&#41;](../native-client-ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md)   
 [IROWSETFASTLOAD 및 ISEQUENTIALSTREAM &#40;OLE DB를 사용 하 여 BLOB 데이터를 SQL SERVER로 보냅니다&#41;](../native-client-ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md)  
  
  
