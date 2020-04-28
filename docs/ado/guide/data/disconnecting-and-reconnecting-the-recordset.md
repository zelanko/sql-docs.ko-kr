---
title: 레코드 집합 연결 끊기 및 다시 연결 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset object [ADO], disconnecting and reconnecting
ms.assetid: c5134af7-81d6-4de4-9fd1-cfe29973545e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9829ddfd7e625941c97bd3b2027c328a1fba93d6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925518"
---
# <a name="disconnecting-and-reconnecting-the-recordset"></a>레코드 집합 연결 끊기 및 다시 연결
ADO에 있는 가장 강력한 기능 중 하나는 데이터 원본에서 클라이언트 쪽 레코드 집합을 열고 데이터 원본에서 레코드 집합의 연결을 끊는 기능입니다. 레코드 집합의 연결이 끊어지면 데이터 원본에 대 한 연결을 닫아 서버에서 리소스를 유지 관리 하는 데 사용 되는 리소스를 해제할 수 있습니다. 연결이 끊어져 있는 동안에도 레코드 집합의 데이터를 계속 보고 편집할 수 있으며 나중에 데이터 원본에 다시 연결 하 여 일괄 처리 모드로 업데이트를 보낼 수 있습니다.  
  
 레코드 집합의 연결을 끊으려면 adUseClient의 커서 위치를 사용 하 여 연 다음 ActiveConnection 속성을 Nothing으로 설정 합니다. C + + 사용자는 연결을 끊으려면 ActiveConnection을 NULL로 설정 해야 합니다.  
  
 클라이언트 컴퓨터가 네트워크에 연결 되어 있지 않은 상태에서 응용 프로그램에 사용할 수 있는 데이터 집합의 데이터를 포함 해야 하는 시나리오를 해결 하기 위해 레코드 집합 지 속성에 대해 설명 하는 경우이 섹션의 뒷부분에서 연결 되지 않은 레코드 집합을 사용 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [일괄 처리 모드](../../../ado/guide/data/batch-mode.md)
