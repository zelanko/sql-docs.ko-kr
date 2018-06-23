---
title: ISSAbort (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- ISSAbort interface
ms.assetid: 7c4df482-4a83-4da0-802b-3637b507693a
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 53c6e2c7c06331ce75883f86a8935d4d1c2419c4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36089118"
---
# <a name="issabort-ole-db"></a>ISSAbort(OLE DB)
  **ISSAbort** 에서 공개 된 인터페이스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB provider는 [issabort:: Abort](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md) 메서드는 현재 행 집합 및 모든 명령을 취소 하는 데 사용 되는 일괄 처리 처음에 행 집합을 생성 하 고 실행을 아직 완료 되지 않은 명령입니다.  
  
 **ISSAbort** 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 공급자별 인터페이스를 사용 하 여 사용할 수 있는 **QueryInterface** 에 **IMultipleResults** 에서 반환 된 개체  **Icommand:: Execute** 또는 **iopenrowset:: Openrowset**합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|메서드|Description|  
|------------|-----------------|  
|[Issabort:: Abort &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md)|현재 행 집합 및 현재 명령과 연결된 일괄 처리되는 명령을 취소합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [인터페이스 &#40;OLE DB&#41;](../../../2014/database-engine/dev-guide/interfaces-ole-db.md)  
  
  