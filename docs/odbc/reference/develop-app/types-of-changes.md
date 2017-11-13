---
title: "변경 내용 유형의 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- compatibility [ODBC], types of changes
- backward compatibility [ODBC], types of changes
ms.assetid: 6a7db81a-20aa-4915-aed8-429711a36f49
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9a494595625d264159fbb39db03818d50ed97876
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="types-of-changes"></a>유형의 변경
ODBC 3에서 세 가지 유형의 변경 내용 수행 됩니다. *x* (및 ODBC의 모든 버전). 이러한 각 이전 버전과 호환성을 다르게 영향을 받으며를 다른 방식으로 처리 됩니다. 이러한 변경 내용은 다음 표에 설명 되어 있습니다.  
  
|변경의 유형|Description|  
|--------------------|-----------------|  
|새 기능|이들은 ODBC 3으로 새로운 기능입니다. *x*등 아웃오브 라인 바인딩 설명자입니다. 이러한 경우에 응용 프로그램 및 드라이버를 뿐 아니라 드라이버 관리자 버전 3의 작업 구현 됩니다*.x*, 되므로 이러한 이전 버전과 호환성을 확인 하려고 하지 않습니다.|  
|중복 된 기능|ODBC 2에 존재 하는 기능*.x* 고 ODBC 3. *x* 있지만에 각각 다른 방식으로 구현 합니다. 함수 **SQLAllocHandle** 및 **SQLAllocStmt** 은 예입니다. 이러한 이전 버전과 호환성 및 다른 중복 된 기능 매핑 드라이버 관리자에서에서 대부분 처리 합니다.|  
|동작 변경 내용|ODBC 2에서 다르게 처리 하는 기능*.x* 고 ODBC 3. *x*합니다. 날짜/시간 **#define** 은 예입니다. 이러한 기능은 ODBC 3에서 처리 됩니다. *x* 환경 특성 설정을 기반으로 하는 드라이버입니다. (참조 [변경 된 동작](../../../odbc/reference/develop-app/behavioral-changes.md) 자세한 정보에 대 한 합니다.)|

