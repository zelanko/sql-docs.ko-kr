---
title: IRowsetFastLoad (OLE DB) | Microsoft Docs
description: IRowsetFastLoad(OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: COM
helpviewer_keywords:
- IRowsetFastLoad interface
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: eea2e77e5280044a8bb17a0eca33ed68da0c054d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="irowsetfastload-ole-db"></a>IRowsetFastLoad(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **IRowsetFastLoad** 인터페이스에 대 한 지원을 노출 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 메모리 기반 대량 복사 작업입니다. OLE DB Driver SQL Server 소비자가 사용 하기 위한 인터페이스를 신속 하 게 하 여 추가 데이터를 기존 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블입니다.  
  
 세션에 대해 SSPROP_ENABLEFASTLOAD를 VARIANT_TRUE로 설정하면 해당 세션에서 반환된 행 집합의 데이터를 읽을 수 없습니다. SSPROP_ENABLEFASTLOAD를 VARIANT_TRUE로 설정 하면 세션에서 생성 하는 모든 행 집합 IRowsetFastLoad 형식의 됩니다. IRowsetFastLoad 행 집합 행 집합 인출 기능을 지원 하지 않습니다. 따라서 이러한 행 집합의 데이터를 읽을 수 없습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|메서드|Description|  
|------------|-----------------|  
|[Irowsetfastload:: Commit &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/irowsetfastload-commit-ole-db.md)|일괄 삽입되는 행의 끝을 표시하고 행을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블에 씁니다.|  
|[Irowsetfastload:: Insertrow &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/irowsetfastload-insertrow-ole-db.md)|대량 복사 행 집합에 행을 추가합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [인터페이스 & #40; OLE db& #41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)   
 [데이터 대량 복사 IRowsetFastLoad를 사용 하 여 &#40;OLE DB&#41;](../../oledb/ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md)   
 [IROWSETFASTLOAD 및 ISEQUENTIALSTREAM & #40; OLE db& #41;를 사용 하 여 SQL SERVER BLOB 데이터 보내기](../../oledb/ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md)  
  
  
