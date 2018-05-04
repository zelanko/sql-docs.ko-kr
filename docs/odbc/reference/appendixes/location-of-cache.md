---
title: 캐시 위치 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: 240d6162-4da6-4b1f-96c7-f379f4ecb16f
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 78e4378e5895e68e8eeb461560faa88ef9cef837
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="location-of-cache"></a>캐시의 위치
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 마십시오 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하세요. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 커서 라이브러리 Windows® 임시 파일 및 메모리에 데이터를 캐시합니다. 커서 라이브러리 사용 가능한 디스크 공간 까지로 처리할 수 있는 결과 집합의 크기를 제한 합니다. 커서 라이브러리 캐시의 끝에 삽입 하는 경우 데이터를 캐시 세그먼트 경계 교차 하는 경우 임시 파일 사용 됩니다. 대신, 데이터를 캐시 대신 마지막으로 저장 된 데이터 블록의 캐시에 추가 됩니다. 마지막으로 저장 된 데이터 블록의 임시 파일에 저장 됩니다. 커서 라이브러리는 비정상적으로 종료 되는 Windows 임시 디스크 파일을 둘 수는 정전 시와 같은 합니다. 행 그룹의 이름은 ~ CTT*nnnn*.tmp 되며 현재 디렉터리에 생성 합니다.  
  
> [!NOTE]  
>  응용 프로그램은 읽기 전용 공유 (예: Microsoft Foundation Class 라이브러리 샘플) 컴팩트 디스크에서 실행 되는 동안 커서 라이브러리의 Microsoft® WindowsNT®/windows 2000 찾으려 현재 디렉터리에 임시 파일에 데이터를 캐시 하는 경우 SQLSTATE HY000 (일반 오류-없습니다 파일 버퍼를 만들) 반환 됩니다.
