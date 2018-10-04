---
title: 연결을 끊고 다시 연결 하는 레코드 집합 | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 0cefdb81aa9e9a1a5f7ad7ba1f6db86d1ae95e2d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47772001"
---
# <a name="disconnecting-and-reconnecting-the-recordset"></a>레코드 집합 연결 끊기 및 다시 연결
ADO의 가장 강력한 기능 중 하나에 데이터 원본에서 클라이언트 쪽 레코드 집합을 열고 다음 데이터 원본에서 레코드 집합을 분리 하는 기능입니다. 레코드 집합의 연결이 끊어지면 데이터 원본에 대 한 연결 닫히게 되므로 유지 관리를 사용 하는 서버 리소스가 해제 됩니다. 계속 보고 연결이 끊어진 동안 레코드 집합에서 데이터를 편집 하 고 및 데이터 원본에 나중에 다시 연결 하 고, 일괄 처리 모드에서 업데이트를 보낼 수 있습니다.  
  
 레코드 집합의 연결을 끊으려면 adUseClient, 커서 위치를 사용 하 여 열고 nothing ActiveConnection 속성을 설정 합니다. (C + + 사용자 설정 해야 합니다 ActiveConnection 연결을 끊을 NULL 같음.)  
  
 나중에 사용할 연결이 끊긴된 레코드 집합이이 섹션에 있는 데이터 응용 프로그램에 사용할 수 있는 레코드 집합에 있고 클라이언트 컴퓨터는 네트워크에 연결 되어 있지 해야 하는 시나리오를 해결 하기 위해 지 속성 레코드 집합을 설명할 때.  
  
## <a name="see-also"></a>관련 항목  
 [일괄 처리 모드](../../../ado/guide/data/batch-mode.md)
