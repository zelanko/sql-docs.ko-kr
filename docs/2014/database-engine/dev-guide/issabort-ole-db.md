---
title: ISSAbort (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- ISSAbort interface
ms.assetid: 7c4df482-4a83-4da0-802b-3637b507693a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 801eb84df08837ec8e49b6bb0e28fc1f1115e674
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62781039"
---
# <a name="issabort-ole-db"></a>ISSAbort(OLE DB)
  Native Client OLE DB 공급자에 노출 되는 ISSAbort 인터페이스는 현재 행 집합을 취소 하는 데 사용 되는 [ISSAbort:: Abort](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md) 메서드와, 처음에 행 집합을 생성 한 명령을 사용 하 여 일괄 처리 되 고 아직 실행이 완료 되지 않은 모든 명령을 제공 합니다. **** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 **ISSAbort** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 은 **ICommand:: Execute** 또는 **Iopenrowset:: OpenRowset**에서 반환 된 **IMultipleResults** 개체에 대해 **QueryInterface** 를 사용 하 여 사용할 수 있는 Native Client 공급자별 인터페이스입니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|방법|Description|  
|------------|-----------------|  
|[ISSAbort:: Abort &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md)|현재 행 집합 및 현재 명령과 연결된 일괄 처리되는 명령을 취소합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [인터페이스 &#40;OLE DB&#41;](../../../2014/database-engine/dev-guide/interfaces-ole-db.md)  
  
  
