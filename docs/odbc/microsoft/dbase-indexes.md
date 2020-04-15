---
title: dBASE 지수 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9300a38a0e36da771a238f73b77d3dda527334ae
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307674"
---
# <a name="dbase-indexes"></a>dBASE 인덱스
ODBC dBASE 드라이버가 자동으로 열리고 dBASE IV 인덱스 파일을 업데이트합니다. ODBC 데이터 원본 관리자를 통해 표시되는 **인덱스 선택** 대화 상자를 사용하여 dBASE III .ndx 파일을 dBASE 파일과 연결해야 합니다.  
  
 dBASE 인덱스 생성에는 다음과 같은 제한 사항이 적용됩니다.  
  
-   모든 열 이름은 유효해야 합니다.  
  
-   모든 열은 오름차순 또는 내림차순이어야 합니다.  
  
-   단일 텍스트 열의 길이는 100바이트 미만이어야 합니다.  
  
-   두 개 이상의 열이 있는 경우 모든 열은 텍스트 열이어야 하며 열 크기의 합계는 100바이트 미만이어야 합니다.  
  
-   메모 필드는 인덱싱할 수 없습니다.  
  
-   현재 필드 집합에 대해 인덱스를 지정할 수 없습니다(즉, 중복 인덱스는 허용되지 않음).  
  
-   인덱스 이름은 dBASE 인덱스 명명 규칙과 일치해야 합니다. dBASE III에는 각 인덱스가 .ndx 확장인 별도의 파일에 있어야 합니다. dBASE IV에서 인덱스는 단일 .mdx 파일에 저장된 태그 이름으로 만들어집니다. .mdx 파일은 데이터베이스 파일과 동일한 기본 이름을 가며(예: Emp.mdx는 Emp.dbf 데이터베이스의 인덱스 파일임).  
  
-   dBASE는 고유 인덱스를 동일한 키 값을 가진 집합의 레코드 하나만 인덱스에 추가되는 인덱스로 정의합니다.
