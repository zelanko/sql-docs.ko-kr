---
title: 변경 유형 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301608"
---
# <a name="types-of-changes"></a>변경 형식
ODBC 3.x 및 모든 버전의 ODBC에서는 세 가지 유형의 변경 내용이 적용 *됩니다.* 이러한 각각은 이전 버전과의 호환성에 영향을 주며 다른 방식으로 처리 됩니다. 이러한 변경 내용은 다음 표에 설명 되어 있습니다.  
  
|변경 유형|설명|  
|--------------------|-----------------|  
|새 기능|이는 인라인 바인딩 또는 설명자와 같이 *ODBC 3.x*의 새로운 기능입니다. 이러한 작업은 응용 프로그램 및 드라이버와 드라이버 관리자 *의 버전이 2.x 인 경우*에만 구현 되므로 이러한 이전 버전과의 호환성을 위해 시도 하지 않습니다.|  
|중복 기능|이러한 기능은 ODBC *2.x 및 odbc* 3.x *에 있지만 각각* 다른 방식으로 구현 됩니다. **SQLAllocHandle** 및 **sqlallocstmt** 함수는 예입니다. 이러한 기능 및 기타 중복 된 기능에 대 한 이전 버전과의 호환성 문제는 대부분 드라이버 관리자의 매핑에 의해 처리 됩니다.|  
|동작 변경|이러한 기능은 ODBC *2.x와 odbc* *3(sp3)* 에서 다르게 처리 됩니다. Datetime **#define** 은 예입니다. 이러한 기능은 환경 특성 설정에 따라 *ODBC 3.x* 드라이버에 의해 처리 됩니다. 자세한 내용은 [동작 변경 내용](../../../odbc/reference/develop-app/behavioral-changes.md) 을 참조 하세요.|
