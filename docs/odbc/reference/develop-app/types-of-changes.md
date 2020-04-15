---
title: 변경 유형 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f44adb59aa9b0f25475a76a97fe3670de0228c08
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301608"
---
# <a name="types-of-changes"></a>변경 형식
ODBC *3.x(및* 모든 버전의 ODBC)에서 세 가지 유형의 변경이 이루어집니다. 이들 각각은 이전 버전과의 호환성에 다르게 영향을 미치며 다른 방식으로 처리됩니다. 이러한 변경 내용은 다음 표에 설명되어 있습니다.  
  
|변경 유형|설명|  
|--------------------|-----------------|  
|새로운 기능|이러한 기능은 ODBC *3.x에*새로 접하는 기능(예: 줄 바이면 바인딩 또는 설명자)입니다. 이러한 응용 프로그램 및 드라이버뿐만 아니라 드라이버 관리자가 버전 *3.x인*경우에만 구현되므로 이전 버전과 호환되도록 만들지 않습니다.|  
|중복된 피처|ODBC *2.x* 및 ODBC *3.x에* 존재하지만 각각 다른 방식으로 구현되는 기능입니다. **함수 SQLAllocHandle** 및 **SQLAllocStmt는** 예입니다. 이러한 기능 및 기타 중복된 기능에 대한 이전 버전과의 호환성 문제는 대부분 드라이버 관리자의 매핑에 의해 처리됩니다.|  
|동작 변경|ODBC *2.x* 및 ODBC *3.x에서*다르게 처리되는 기능입니다. 날짜 **시간 #define** 예입니다. 이러한 기능은 환경 특성 설정에 따라 ODBC *3.x* 드라이버에서 처리됩니다. (자세한 내용은 [행동 변경](../../../odbc/reference/develop-app/behavioral-changes.md) 사항을 참조하십시오.)|
