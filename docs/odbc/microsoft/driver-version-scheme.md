---
title: 드라이버 버전 구성표 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d8a155f5d76e8a250c64d3d59e160fbb5863414f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68071851"
---
# <a name="driver-version-scheme"></a>드라이버 버전 구성표
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 다음 표에는 Oracle 용 Microsoft ODBC Driver의 모든 릴리스된 버전이 나와 있습니다.  
  
|드라이버 버전|빌드 번호|가용성 기록|  
|--------------------|------------------|--------------------------|  
|1.0|2.00.6235|Visual C++ 4.2 및 Visual Basic 5.0, Enterprise Edition|  
|2.0|2.73.7269|Visual Studio 97 및 MDAC 1.5 a|  
|2.0 업데이트 됨|2.73.7283.01|IIS 4.0|  
|2.0 업데이트 됨|2.73.7283.03|MDAC 1.5 b 및 1.5 c|  
|2.0 업데이트 됨|2.73.7356|ODBC 3.5 SDK|  
|2.5|2.573.2927|Visual Studio 6.0 및 MDAC 2.0|  
|2.5 업데이트 됨|2.573.3513|SQL Server 7.0<br /><br /> SQL Server 6.5 SP5|  
  
 Build 2.00.6235 (버전 1)은 Microsoft ODBC Driver for Oracle의 첫 번째 릴리스입니다. 첫 번째 버전의 릴리스 후 새 명명 규칙을 채택 했습니다.  
  
 예를 들어 2.73.7283.03는 다음과 같은 고유한 구성 요소로 나눌 수 있습니다.  
  
-   2 = 버전 번호입니다.  
  
-   73 = 드라이버가 디자인 된 Oracle Server의 버전입니다.  
  
-   7283.03 = 드라이버의 빌드 번호입니다.  
  
> [!NOTE]  
>  Release 2.573.2973를 사용 하는 경우 명명 규칙은 2.573가 2.73 보다 이전 버전인 경우 혼동을 빌드 번호의 각 섹션은 개별적으로 고려해 야 합니다. 숫자 573는 73 보다 크므로 최신 버전입니다. 또한 "2.5"은 드라이버의 버전 번호를 나타냅니다.
