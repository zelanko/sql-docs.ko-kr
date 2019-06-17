---
title: 변경 유형에 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], types of changes
- backward compatibility [ODBC], types of changes
ms.assetid: 6a7db81a-20aa-4915-aed8-429711a36f49
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac92c6d40ea9ead6b8875e3338bb740b4bdf8523
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63473182"
---
# <a name="types-of-changes"></a>변경 형식
ODBC 3에서 세 가지 유형의 변경이 됩니다. *x* (및 ODBC의 모든 버전). 이러한 각 이전 버전과 호환성을 다르게 영향을 받으며 다른 방식으로 처리 됩니다. 이러한 변경 내용은 다음과에서 같습니다.  
  
|형식 변경|Description|  
|--------------------|-----------------|  
|새로운 기능|이들은 ODBC 3에 새로 추가 된 기능입니다. *x*등 아웃오브 라인 바인딩 설명자입니다. 이러한 드라이버 관리자 뿐만 아니라 응용 프로그램 및 드라이버 버전 3 가지 경우에 구현 됩니다 *.x*이므로 이러한 이전 버전과 호환성을 확인 하지 않습니다.|  
|중복 된 기능|이러한 기능은 ODBC 2에 존재 *.x* 고 ODBC 3. *x* 에 각각 다른 방식으로 구현 됩니다. 함수 **SQLAllocHandle** 하 고 **SQLAllocStmt** 예입니다. 이전 버전과 호환성에 대 한 문제 및 다른 중복 된 기능 드라이버 관리자의 매핑을에서 처리 하는 대부분입니다.|  
|동작 변경 내용|이러한 기능은 ODBC 2에서 다르게 처리 됩니다 *.x* 고 ODBC 3. *x*합니다. 날짜/시간 **#define** 은 예입니다. 이러한 기능 ODBC 3에서 처리 됩니다. *x* 환경 특성 설정을 기반으로 하는 드라이버입니다. (참조 [동작 변경 내용](../../../odbc/reference/develop-app/behavioral-changes.md) 자세한.)|
