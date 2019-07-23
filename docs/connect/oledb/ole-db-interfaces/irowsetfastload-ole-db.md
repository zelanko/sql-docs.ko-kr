---
title: IRowsetFastLoad (OLE DB) | Microsoft Docs
description: IRowsetFastLoad(OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apitype: COM
helpviewer_keywords:
- IRowsetFastLoad interface
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 2d21e270eb7e2d387201d66df0bb566c3924d53c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67994400"
---
# <a name="irowsetfastload-ole-db"></a>IRowsetFastLoad(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  **IRowsetFastLoad** 인터페이스는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 메모리 기반 대량 복사 작업에 대한 지원을 제공합니다. SQL Server 소비자를 위한 OLE DB 드라이버는 인터페이스를 사용 하 여 기존 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블에 데이터를 빠르게 추가 합니다.  
  
 세션에 대해 SSPROP_ENABLEFASTLOAD를 VARIANT_TRUE로 설정하면 해당 세션에서 반환된 행 집합의 데이터를 읽을 수 없습니다. SSPROP_ENABLEFASTLOAD를 VARIANT_TRUE로 설정하면 세션에서 생성되는 모든 행 집합이 IRowsetFastLoad 형식으로 설정되는데, IRowsetFastLoad 행 집합은 행 집합 인출 기능을 지원하지 않기 때문에 이러한 행 집합의 데이터는 읽을 수 없습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|메서드|설명|  
|------------|-----------------|  
|[IRowsetFastLoad:: Commit &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/irowsetfastload-commit-ole-db.md)|일괄 삽입되는 행의 끝을 표시하고 행을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블에 씁니다.|  
|[IRowsetFastLoad:: InsertRow &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/irowsetfastload-insertrow-ole-db.md)|대량 복사 행 집합에 행을 추가합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [인터페이스 &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)   
 [IRowsetFastLoad&#40;OLE DB&#41;를 사용한 데이터 대량 복사](../../oledb/ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md)   
 [IROWSETFASTLOAD 및 ISEQUENTIALSTREAM&#40;OLE DB&#41;을 사용하여 BLOB 데이터를 SQL Server로 보내기](../../oledb/ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md)  
  
  
