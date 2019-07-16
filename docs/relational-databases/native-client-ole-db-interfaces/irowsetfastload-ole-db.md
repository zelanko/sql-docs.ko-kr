---
title: IRowsetFastLoad (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: COM
helpviewer_keywords:
- IRowsetFastLoad interface
ms.assetid: d19a7097-48d9-409a-aff9-277891b7aca7
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c88a3d0a71305362acdf0ae28ef7eb4d75f5470f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68051067"
---
# <a name="irowsetfastload-ole-db"></a>IRowsetFastLoad(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **IRowsetFastLoad** 인터페이스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리 기반 대량 복사 작업에 대한 지원을 제공합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 소비자 인터페이스를 사용 하 여 기존 데이터를 신속 하 게 추가할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블입니다.  
  
 세션에 대해 SSPROP_ENABLEFASTLOAD를 VARIANT_TRUE로 설정하면 해당 세션에서 반환된 행 집합의 데이터를 읽을 수 없습니다. SSPROP_ENABLEFASTLOAD를 VARIANT_TRUE로 설정하면 세션에서 생성되는 모든 행 집합이 IRowsetFastLoad 형식으로 설정되는데, IRowsetFastLoad 행 집합은 행 집합 인출 기능을 지원하지 않기 때문에 이러한 행 집합의 데이터는 읽을 수 없습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|메서드|설명|  
|------------|-----------------|  
|[Irowsetfastload:: Commit &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-commit-ole-db.md)|일괄 삽입되는 행의 끝을 표시하고 행을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 씁니다.|  
|[Irowsetfastload:: Insertrow &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-insertrow-ole-db.md)|대량 복사 행 집합에 행을 추가합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [인터페이스 &#40;OLE DB&#41;](https://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)   
 [IRowsetFastLoad&#40;OLE DB&#41;를 사용한 데이터 대량 복사](../../relational-databases/native-client-ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md)   
 [IROWSETFASTLOAD 및 ISEQUENTIALSTREAM&#40;OLE DB&#41;을 사용하여 BLOB 데이터를 SQL Server로 보내기](../../relational-databases/native-client-ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md)  
  
  
