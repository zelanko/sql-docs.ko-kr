---
title: "명령 개체 개요 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: command object [ADO]
ms.assetid: e84a14b1-3c2a-4f7d-a966-9e08a93948df
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8f1f01c7ca7a378faaaabf11099b97b0dfa0c7a2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="command-object-overview"></a>Command 개체 개요
와 **명령** 개체를 다음을 수행할 수 있습니다.  
  
-   명령 (예를 들어 SQL 문 또는 저장된 프로시저)의 실행 텍스트를 사용 하 여 정의 된 **CommandText** 속성입니다.  
  
-   매개 변수가 있는 쿼리 또는 저장된 프로시저 인수를 사용 하 여 정의 **매개 변수** 개체 및 **매개 변수** 컬렉션입니다.  
  
-   명령을 실행 하 고 반환 된 **레코드 집합** 를 사용 하 여 개체를 적절 하 게 하는 경우는 **Execute** 메서드.  
  
-   명령의 형식을 사용 하 여 지정 된 **CommandType** 성능을 최적화 하기 위해 실행 전에 속성입니다.  
  
-   명령 텍스트에 대 한 특정 정보를 사용 하 여 지정 된 **언어** 속성의는 **명령** 개체입니다.  
  
-   공급자를 사용 하 여 실행 하기 전에 명령의 준비 된 (또는 컴파일된) 버전을 저장 하는지 여부를 제어는 **Prepared** 속성입니다.  
  
-   공급자에서 사용 하 여를 실행 하는 명령에 대 한 대기 하는 시간 (초)의 수를 설정 된 **CommandTimeout** 속성입니다.  
  
-   연결 된 열려 있는 연결을 **명령** 개체를 설정 하 여 해당 **ActiveConnection** 속성입니다.  
  
-   설정의 **이름** 속성을 식별 하는 **명령** 개체에 연결 된 메서드로 **연결** 개체입니다.  
  
-   전달는 **명령** 개체는 **소스** 속성의는 **레코드 집합** 데이터를 수집 하려면.  
  
-   전달 된 **스트림** 인터페이스를 지 원하는 공급자에 명령 (예: XML 명령)을 포함 하는 개체입니다.
