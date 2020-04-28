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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9300a38a0e36da771a238f73b77d3dda527334ae
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307674"
---
# <a name="dbase-indexes"></a>dBASE 인덱스
ODBC dBASE 드라이버가 dBASE IV 인덱스 파일을 자동으로 열고 업데이트 합니다. ODBC 데이터 원본 관리자를 통해 표시 되는 **인덱스 선택** 대화 상자를 사용 하 여 dbase III. ndx 파일을 dbase 파일과 연결 해야 합니다.  
  
 DBASE 인덱스 생성에는 다음과 같은 제한 사항이 적용 됩니다.  
  
-   모든 열 이름은 유효 해야 합니다.  
  
-   모든 열은 오름차순 또는 내림차순으로 정렬 되어야 합니다.  
  
-   단일 텍스트 열의 길이는 100 바이트 미만 이어야 합니다.  
  
-   둘 이상의 열이 있는 경우 모든 열은 텍스트 열 이어야 하며 열 크기의 합계는 100 바이트 미만 이어야 합니다.  
  
-   메모 필드는 인덱싱할 수 없습니다.  
  
-   현재 필드 집합에 대해서는 인덱스를 지정 하지 않아야 합니다. 즉, 중복 된 인덱스는 허용 되지 않습니다.  
  
-   인덱스 이름은 dBASE 인덱스 명명 규칙과 일치 해야 합니다. dBASE III을 사용 하려면 각 인덱스가 별도의 파일에 있어야 하며 각각은 확장명이 ndx입니다. DBASE IV에서는 단일 mdx 파일에 저장 된 태그 이름으로 인덱스가 생성 됩니다. . N e s 파일은 데이터베이스 파일과 동일한 기본 이름을 갖습니다. 예를 들어, emp는 Emp. .dbf 데이터베이스의 인덱스 파일입니다.  
  
-   dBASE는 동일한 키 값을 가진 집합에서 하나의 레코드만 인덱스에 추가 되는 고유 인덱스를 정의 합니다.
