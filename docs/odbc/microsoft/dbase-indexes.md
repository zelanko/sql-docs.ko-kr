---
title: "dBASE 인덱스 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DBase indexes [ODBC]
- DBase driver [ODBC], indexes
ms.assetid: fdfa56f5-e324-4ec2-9267-fdf95ab99373
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b71b043667708c69494d5b057436f35b7d1a288d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="dbase-indexes"></a>dBASE 인덱스
ODBC dBASE 드라이버가 자동으로 열리고 dBASE IV 인덱스 파일을 업데이트 합니다. 사용 해야 합니다는 **인덱스 선택** dBASE 파일 dBASE III.ndx 파일과 연결 하려면 ODBC 데이터 원본 관리자를 통해 표시 되는 대화 상자.  
  
 DBASE 인덱스 만들기에는 다음과 같은 제한 사항이 적용 됩니다.  
  
-   모든 열 이름은 유효 해야 합니다.  
  
-   모든 열은 동일한 오름차순 또는 내림차순 되어야 합니다.  
  
-   단일 텍스트 열 길이 100 바이트 미만 이어야 합니다.  
  
-   둘 이상의 열이 있으면 열의 모든 텍스트 열 있어야 하며 열 크기의 합계는 100 바이트 미만 이어야 합니다.  
  
-   메모 필드를 인덱싱할 수 없습니다.  
  
-   필드의 현재 집합에 대 한 인덱스를 지정 하지 해야 (즉, 중복 인덱스 허용 되지 않음).  
  
-   인덱스 이름 dBASE 인덱스 명명 규칙을 일치 해야 합니다. dBASE III 각은 확장명이.ndx 별도 파일에 각 인덱스 요구 합니다. DBASE IV 단일.mdx 파일에 저장 된 태그 이름으로 인덱스를 만듭니다. .Mdx 파일은 데이터베이스 파일과 동일한 기본 이름 (예를 들어 Emp.mdx는 Emp.dbf 데이터베이스에 대 한 인덱스 파일).  
  
-   dBASE 정의 고유 인덱스를 동일한 키 값을 가진 집합에서 레코드를 하나만 인덱스에 추가 됩니다.
