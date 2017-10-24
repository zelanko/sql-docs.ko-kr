---
title: "OLE DB에 대 한 Microsoft 커서 서비스 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cursor service for ole db [ADO]
- cursors [ADO], cursor service for OLE DB
ms.assetid: 1ac3bd9b-2d45-4cc8-88ec-bd8a218cfb49
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ce4deae8dc07c546fc777a6fa86d159b404c60f9
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="the-microsoft-cursor-service-for-ole-db"></a>OLE DB에 대 한 Microsoft 커서 서비스
클라이언트 쪽 커서를 선택 하거나 설정 하면는 **앞** 속성을 **adUseClient**, OLE DB에 대 한 Microsoft 커서 서비스를 호출 하는 합니다. 또한 표시는 "클라이언트 커서"는 엔진을 ADO의 컨텍스트에서 동일한 작업에 대 한 참조가 있습니다. 이 서비스는 데이터 공급자의 커서 지원 기능을 보완합니다. 결과적으로, 모든 데이터 공급자의 기능을 비교적 안정적으로 인식할 수 있습니다.  
  
 OLE DB에 대 한 커서 서비스 동적 속성을 사용할 수 있도록을 특정 메서드의 동작을 향상 시킵니다. 예를 들어는 **최적화** 동적 속성와 같은 특정 작업을 용이 하 게 임시 인덱스를 만들 수는 **찾을** 메서드.  
  
 커서 서비스에는 항상에서 일괄 처리 업데이트 지원할을 수 있습니다. 또한 데이터 공급자는 정적 커서와 같은 기능이 적은 커서를 제공할 수 때 동적 커서 등 더욱 강력한 커서 유형 시뮬레이션 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [OLE DB (ADO 서비스 구성 요소)에 대 한 Microsoft 커서 서비스](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)

