---
title: dBASE 인덱스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBase indexes [ODBC]
- DBase driver [ODBC], indexes
ms.assetid: fdfa56f5-e324-4ec2-9267-fdf95ab99373
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 66dab60f4a9a180d2a8b74ce4d0c8f4d7bf8d242
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63240402"
---
# <a name="dbase-indexes"></a>dBASE 인덱스
ODBC dBASE 드라이버를 자동으로 열리고 dBASE IV 인덱스 파일을 업데이트 합니다. 사용 해야 합니다 **인덱스 선택** dBASE III.ndx 파일 dBASE 파일을 사용 하 여 연결 하려면 ODBC 데이터 원본 관리자를 통해 표시 되는 대화 상자.  
  
 DBASE 인덱스 생성에는 다음과 같은 제한이 적용 됩니다.  
  
-   열 이름을 모두 유효 해야 합니다.  
  
-   모든 열에 동일한 오름차순 또는 내림차순으로 정렬 해야 합니다.  
  
-   모든 단일 텍스트 열의 길이 100 바이트 미만이 이어야 합니다.  
  
-   둘 이상의 열이 있는 경우 모든 열의 텍스트 열 하며 열 크기의 합계는 100 바이트 미만이 이어야 합니다.  
  
-   메모 필드를 인덱싱할 수 없습니다.  
  
-   필드의 현재 집합에 대 한 인덱스를 지정할 수 있어야 합니다 (즉, 중복 된 인덱스는 허용 되지 않음).  
  
-   인덱스 이름을 dBASE 인덱스 명명 규칙이 일치 해야 합니다. dBASE III 개.ndx 확장 별도 파일에서 각 인덱스는 필요 합니다. DBASE IV, 인덱스는 단일.mdx 파일에 저장 된 태그 이름으로 생성 됩니다. .Mdx 파일 이름이 동일한 기본 데이터베이스 파일 (예를 들어 Emp.mdx은 Emp.dbf 데이터베이스에 대 한 인덱스 파일).  
  
-   dBASE는 인덱스에 동일한 키 값을 사용 하 여 집합에서 하나의 레코드가 추가 되는 위치 하나로 고유 인덱스를 정의 합니다.
