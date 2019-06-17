---
title: 캐시 위치 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: 240d6162-4da6-4b1f-96c7-f379f4ecb16f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4b1ffd8c56a6727a892cb518222c961bbb6c794c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63181339"
---
# <a name="location-of-cache"></a>캐시의 위치
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 커서 라이브러리 Windows® 임시 파일 및 메모리에 데이터를 캐시합니다. 이 커서 라이브러리 사용 가능한 디스크 공간에 의해서만 처리할 수 있는 결과 집합의 크기를 제한 합니다. 임시 파일에는 커서 라이브러리 캐시의 끝에 삽입 하는 경우 데이터를 캐시 세그먼트 경계를 교차 하는 경우 사용 됩니다. 대신, 데이터 캐시를 마지막으로 저장 된 데이터 블록의 캐시에 대신 추가 됩니다. 마지막으로 저장 된 데이터 블록의 임시 파일에 저장 됩니다. 커서 라이브러리 기능 실패할 경우 같은 비정상적으로 종료 되 면 Windows 임시 디스크의 파일을 두어도 됩니다. 명명 된 ~ CTT*nnnn*.tmp 되며 현재 디렉터리에 만들어집니다.  
  
> [!NOTE]  
>  응용 프로그램은 읽기 전용 공유 또는 compact 디스크 (예: Microsoft Foundation Class 라이브러리 샘플)에서 실행 되는 동안 Microsoft® WindowsNT®/Windows2000 커서 라이브러리를 현재 디렉터리에 임시 파일에 데이터를 캐시 하려고 하는 경우 SQLSTATE HY000 (일반 오류-수 없습니다 파일의 버퍼를 만들려면) 반환 됩니다.
