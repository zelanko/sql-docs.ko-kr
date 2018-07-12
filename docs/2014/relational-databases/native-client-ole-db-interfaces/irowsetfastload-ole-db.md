---
title: IRowsetFastLoad (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- IRowsetFastLoad interface
ms.assetid: d19a7097-48d9-409a-aff9-277891b7aca7
caps.latest.revision: 36
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 60d4d982eb88498cf3d56f14efdffae05a71d26a
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37415092"
---
# <a name="irowsetfastload-ole-db"></a>IRowsetFastLoad(OLE DB)
  합니다 `IRowsetFastLoad` 인터페이스에 대 한 지원을 노출 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리 기반 대량 복사 작업입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 소비자 인터페이스를 사용 하 여 기존 데이터를 신속 하 게 추가할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블입니다.  
  
 세션에 대해 SSPROP_ENABLEFASTLOAD를 VARIANT_TRUE로 설정하면 해당 세션에서 반환된 행 집합의 데이터를 읽을 수 없습니다. SSPROP_ENABLEFASTLOAD를 VARIANT_TRUE로 설정 하는 경우에 세션에서 생성 하는 모든 행 집합 IRowsetFastLoad 형식의 됩니다. IRowsetFastLoad 행 집합은 행 집합 인출 기능을 지원 하지 않습니다. 따라서 이러한 행 집합의 데이터를 읽을 수 없습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|메서드|Description|  
|------------|-----------------|  
|[Irowsetfastload:: Commit &#40;OLE DB&#41;](irowsetfastload-commit-ole-db.md)|일괄 삽입되는 행의 끝을 표시하고 행을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 씁니다.|  
|[Irowsetfastload:: Insertrow &#40;OLE DB&#41;](irowsetfastload-insertrow-ole-db.md)|대량 복사 행 집합에 행을 추가합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [인터페이스 &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)   
 [IRowsetFastLoad를 통한 복사본 데이터를 대량으로 &#40;OLE DB&#41;](../native-client-ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md)   
 [IROWSETFASTLOAD 및 ISEQUENTIALSTREAM을 사용 하 여 SQL SERVER에 BLOB 데이터를 보낼 &#40;OLE DB&#41;](../native-client-ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md)  
  
  
