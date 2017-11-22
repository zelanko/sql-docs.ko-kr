---
title: "연결을 끊고 다시 연결 하는 레코드 집합 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Recordset object [ADO], disconnecting and reconnecting
ms.assetid: c5134af7-81d6-4de4-9fd1-cfe29973545e
caps.latest.revision: "4"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 761b1e37cd8f51e53bc486de460f43212d33df1a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="disconnecting-and-reconnecting-the-recordset"></a>연결을 끊고 다시 연결 하는 레코드 집합
ADO에서 볼 수 있는 가장 강력한 기능 중 하나에 데이터 원본에서 클라이언트 레코드 집합을 연 다음 데이터 원본에서 레코드 집합을 분리 하는 기능입니다. 레코드 집합의 연결이 끊어지면 데이터 원본에 대 한 연결 종료 되므로 유지 관리 하는 데 사용 하는 서버에 있는 리소스를 해제 합니다. 보고 연결이 끊어져도 레코드 집합의 데이터를 편집 하 계속 지정 하 고 나중에 데이터 원본에 연결 한 일괄 처리 모드에서 업데이트를 보냅니다.  
  
 레코드 집합의 연결을 끊을 adUseClient의 커서 위치를 열고 ActiveConnection 속성 Nothing으로 설정 합니다. (C + + 사용자 설정 해야는 ActiveConnection null 연결을 끊을 합니다.)  
  
 사용 합니다 연결이 끊긴된 레코드 집합 나중에이 섹션에는 클라이언트 컴퓨터가 네트워크에 연결 되지 되어 있는 동안 응용 프로그램에 사용할 수 있는 레코드 집합의 데이터를 보유 해야 하는 시나리오를 해결 하기 위해 지 속성 레코드 집합을 설명할 때.  
  
## <a name="see-also"></a>관련 항목:  
 [일괄 처리 모드](../../../ado/guide/data/batch-mode.md)
