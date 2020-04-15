---
title: '6단계: 데이터 소스에서 분리 | 마이크로 소프트 문서'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], disconnecting from data source
- data sources [ODBC], disconnecting
- disconnecting from data source [ODBC]
ms.assetid: 6ad759ba-4721-4d8f-9b26-de976d4fc1a0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: df8cd94435d74bf813b0b64be0753a0beb44d354
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302794"
---
# <a name="step-6-disconnect-from-the-data-source"></a>6단계: 데이터 원본 연결 끊기
마지막 단계는 다음 그림과 같이 데이터 원본에서 연결을 끊는 것입니다. 첫째, 응용 프로그램은 **SQLFreeHandle**을 호출하여 모든 문 핸들을 해제합니다. 자세한 내용은 [명령문 핸들 해제를](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md)참조하십시오.  
  
 ![데이터 소스에서 연결을 끊는 방법](../../../odbc/reference/develop-app/media/pr17.gif "pr17")  
  
 다음으로 응용 프로그램은 **SQLDisconnect를** 사용하여 데이터 원본에서 연결을 끊고 **SQLFreeHandle**을 사용하여 연결 핸들을 해제합니다. 자세한 내용은 [데이터 원본 또는 드라이버의 연결 끊기](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)를 참조하십시오.  
  
 마지막으로 응용 프로그램은 **SQLFreeHandle을** 사용 하 여 환경 핸들을 해제 하 고 드라이버 관리자를 언로드 합니다. 자세한 내용은 [환경 핸들 할당을](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)참조하십시오.
