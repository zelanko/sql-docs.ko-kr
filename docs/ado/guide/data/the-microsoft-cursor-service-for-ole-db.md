---
description: OLE DB용 Microsoft 커서 서비스
title: OLE DB에 대 한 Microsoft Cursor Service | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursor service for ole db [ADO]
- cursors [ADO], cursor service for OLE DB
ms.assetid: 1ac3bd9b-2d45-4cc8-88ec-bd8a218cfb49
author: rothja
ms.author: jroth
ms.openlocfilehash: ce59aa28e8db4716b0e27c848ce774b489ff5891
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979374"
---
# <a name="the-microsoft-cursor-service-for-ole-db"></a>OLE DB용 Microsoft 커서 서비스
클라이언트 쪽 커서를 선택 하거나 **CursorLocation** 속성을 **adUseClient**로 설정 하는 경우 OLE DB에 대해 Microsoft cursor Service를 호출 하 게 됩니다. "클라이언트 커서 엔진"에 대 한 참조도 표시 될 수 있으며,이는 기본적으로 ADO의 컨텍스트에서 동일 합니다. 이 서비스는 데이터 공급자의 커서 지원 기능을 보완 합니다. 결과적으로 모든 데이터 공급자의 상대적으로 일관 된 기능을 얻을 수 있습니다.  
  
 OLE DB에 대 한 커서 서비스는 동적 속성을 사용할 수 있도록 하 고 특정 메서드의 동작을 향상 시킵니다. 예를 들어 **Optimize** dynamic 속성을 사용 하면 임시 인덱스를 만들어 **Find** 메서드와 같은 특정 작업을 쉽게 수행할 수 있습니다.  
  
 Cursor Service를 사용 하면 모든 경우에서 일괄 업데이트를 지원할 수 있습니다. 데이터 공급자가 정적 커서와 같이 지원 되지 않는 커서만 제공할 수 있는 경우에도 동적 커서와 같은 더 강력한 커서 유형을 시뮬레이트할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [OLE DB에 대 한 Microsoft Cursor Service (ADO 서비스 구성 요소)](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)
