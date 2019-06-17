---
title: 명령 개체 개요 | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: d9dd8315945d07aa4c6e99dc8661c26c7d92fb95
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66718459"
---
# <a name="command-object-overview"></a>명령 개체 개요
사용 하 여는 **명령** 개체를 다음을 수행할 수 있습니다.  
  
-   실행 텍스트 명령 (예: SQL 문 또는 저장된 프로시저)를 사용 하 여 정의 된 **CommandText** 속성입니다.  
  
-   매개 변수가 있는 쿼리 또는 저장된 프로시저 인수를 사용 하 여 정의할 **매개 변수** 개체와 **매개 변수** 컬렉션입니다.  
  
-   명령을 실행 하 고 반환 된 **레코드 집합** 사용 하 여 개체를 해당 하는 경우를 **Execute** 메서드.  
  
-   명령의 형식을 사용 하 여 지정 된 **CommandType** 성능을 최적화 하기 위해 실행 전에 속성입니다.  
  
-   명령 텍스트에 대 한 특정 정보를 사용 하 여 지정 합니다 **언어** 의 속성을 **명령** 개체.  
  
-   공급자를 사용 하 여 실행 하기 전에 명령의 준비 된 (또는 컴파일된) 버전을 저장할지 여부를 제어 합니다 **Prepared** 속성입니다.  
  
-   공급자를 사용 하 여 실행 명령에 대 한 대기 시간 (초) 수를 설정 합니다 **CommandTimeout** 속성입니다.  
  
-   와 연결 된 연결을 **명령** 개체를 설정 하 여 해당 **ActiveConnection** 속성입니다.  
  
-   설정 합니다 **이름** 식별 하는 속성을 **명령** 연결 된 방법으로 개체 **연결** 개체.  
  
-   전달를 **명령** 개체를 **원본** 속성을 **레코드 집합** 데이터를 가져오기 위해.  
  
-   전달 된 **Stream** 인터페이스를 지 원하는 공급자에 명령 (예: XML 명령)을 포함 하는 개체입니다.
