---
title: Command 개체 개요 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- command object [ADO]
ms.assetid: e84a14b1-3c2a-4f7d-a966-9e08a93948df
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ef68a36f64fbaf72f18af9fba6f2e2781422574c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925852"
---
# <a name="command-object-overview"></a>명령 개체 개요
**Command** 개체를 사용 하 여 다음을 수행할 수 있습니다.  
  
-   **CommandText** 속성을 사용 하 여 명령의 실행 파일 텍스트 (예: SQL 문 또는 저장 프로시저)를 정의 합니다.  
  
-   **매개 변수** 개체 및 **매개 변수** 컬렉션을 사용 하 여 매개 변수가 있는 쿼리 또는 저장 프로시저 인수를 정의 합니다.  
  
-   명령을 실행 하 고 해당 하는 경우 **execute** 메서드를 사용 하 여 **레코드 집합** 개체를 반환 합니다.  
  
-   성능을 최적화 하기 위해 실행 전에 **CommandType** 속성을 사용 하 여 명령의 유형을 지정 합니다.  
  
-   **명령 개체의** **언어** 속성을 사용 하 여 명령 텍스트에 대 한 특정 정보를 지정 합니다.  
  
-   **준비** 된 속성을 사용 하 여 실행 전에 공급자가 명령의 준비 된 버전 (또는 컴파일)을 저장할지 여부를 제어 합니다.  
  
-   공급자가 **CommandTimeout** 속성을 사용 하 여 명령이 실행 될 때까지 대기 하는 시간 (초)을 설정 합니다.  
  
-   **ActiveConnection** 속성을 설정 하 여 열린 연결을 **명령** 개체와 연결 합니다.  
  
-   **이름** 속성을 설정 하 여 연결 된 **연결** 개체에 대 한 메서드로 **명령** 개체를 식별 합니다.  
  
-   데이터를 가져오기 위해 **명령** 개체를 **레코드 집합** 의 **원본** 속성에 전달 합니다.  
  
-   명령을 포함 하는 **스트림** 개체 (예: XML 명령)를 지 원하는 공급자에 전달 합니다.
