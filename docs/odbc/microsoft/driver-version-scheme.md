---
title: 드라이버 버전 구성표 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], versions
ms.assetid: e4a8d9d7-8aba-48ab-8be6-1a6129adfb8f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 864a8bd892315b060fc6fcf42dbe69dfea61ae59
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303454"
---
# <a name="driver-version-scheme"></a>드라이버 버전 구성표
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 오라클에서 제공하는 ODBC 드라이버를 사용합니다.  
  
 다음 표에는 오라클용 Microsoft ODBC 드라이버의 릴리스된 모든 버전이 나열되어 있습니다.  
  
|드라이버 버전|빌드 번호|가용성 기록|  
|--------------------|------------------|--------------------------|  
|1.0|2.00.6235|비주얼 C ++ 4.2 및 비주얼 기본 5.0, 엔터프라이즈 에디션|  
|2.0|2.73.7269|비주얼 스튜디오 97 및 MDAC 1.5a|  
|2.0 업데이트|2.73.7283.01|IIS 4.0|  
|2.0 업데이트|2.73.7283.03|MDAC 1.5b 및 1.5c|  
|2.0 업데이트|2.73.7356|ODBC 3.5 SDK|  
|2.5|2.573.2927|비주얼 스튜디오 6.0 및 MDAC 2.0|  
|2.5 업데이트|2.573.3513|SQL 서버 7.0<br /><br /> SQL 서버 6.5 SP5|  
  
 빌드 2.00.6235 (버전 1)는 오라클에 대한 마이크로 소프트 ODBC 드라이버의 첫 번째 릴리스였다. 첫 번째 버전이 릴리스된 후 새 명명 규칙이 채택되었습니다.  
  
 예를 들어 2.73.7283.03은 다음과 같은 별개의 구성 요소로 나눌 수 있습니다.  
  
-   2 = 버전 번호입니다.  
  
-   73 = 드라이버가 설계된 Oracle 서버 버전입니다.  
  
-   7283.03 = 드라이버의 빌드 수입니다.  
  
> [!NOTE]  
>  릴리스 2.573.2973을 사용하면 명명 규칙이 2.573이 2.73보다 이전 릴리스라는 혼동을 일으켰지만 빌드 번호의 각 섹션은 개별적으로 고려해야 합니다. 숫자 573은 73보다 크므로 최신 버전입니다. 또한 "2.5"는 드라이버의 버전 번호를 나타냅니다.
