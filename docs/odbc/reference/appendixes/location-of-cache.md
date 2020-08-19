---
description: 캐시의 위치
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 29a0c5507c1b8f581d85b0524784f8ccf1695a5f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429625"
---
# <a name="location-of-cache"></a>캐시의 위치
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 커서 라이브러리는 메모리 및 Windows® 임시 파일에 데이터를 캐시 합니다. 이는 커서 라이브러리가 사용 가능한 디스크 공간을 기준 으로만 처리할 수 있는 결과 집합의 크기를 제한 합니다. 캐시 될 데이터가 커서 라이브러리 캐시의 끝에 삽입 된 경우 세그먼트 경계가 교차 하는 경우 임시 파일이 사용 됩니다. 대신 캐시에 저장 된 데이터의 마지막 블록 대신 캐시 될 데이터가 추가 됩니다. 마지막으로 저장 된 데이터 블록은 임시 파일에 저장 됩니다. 전원에 오류가 발생 한 경우와 같이 커서 라이브러리가 비정상적으로 종료 되 면 디스크에 Windows 임시 파일을 그대로 둘 수 있습니다. 이러한 이름은 ~ CTT*nnnn*. .tmp 이며 현재 디렉터리에 만들어집니다.  
  
> [!NOTE]  
>  응용 프로그램이 읽기 전용 공유 또는 컴팩트 디스크 (예: MFC 라이브러리 샘플)에서 실행 되는 동안 Microsoft® Windows nt®/Windows2000의 커서 라이브러리가 현재 디렉터리에 있는 임시 파일의 데이터를 캐시 하려고 하면 SQLSTATE HY000 (일반 오류-파일 버퍼를 만들 수 없음)이 반환 됩니다.
