---
title: 캐시 위치 | 마이크로 소프트 문서
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
ms.openlocfilehash: 13510332ae8bfab07a13d7831f9f74a048551214
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288621"
---
# <a name="location-of-cache"></a>캐시의 위치
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.  
  
 커서 라이브러리는 메모리와 Windows® 임시 파일에서 데이터를 캐시합니다. 이렇게 하면 커서 라이브러리에서 사용 가능한 디스크 공간에서만 처리할 수 있는 결과 집합의 크기가 제한됩니다. 임시 파일은 캐시할 데이터가 커서 라이브러리 캐시의 끝에 삽입된 경우 세그먼트 경계를 교차할 때 사용됩니다. 대신 캐시할 데이터가 캐시에 마지막으로 저장된 데이터 블록 대신 추가됩니다. 마지막으로 저장된 데이터 블록이 임시 파일에 저장됩니다. 커서 라이브러리가 전원이 끊어지면 Windows 임시 파일을 디스크에 남길 수 있습니다. 이러한 이름은 ~CTT*nnnn*.tmp이며 현재 디렉터리에서 만들어집니다.  
  
> [!NOTE]  
>  Microsoft® WindowsNT®/Windows2000의 커서 라이브러리에서 응용 프로그램이 읽기 전용 공유 또는 소형 디스크(예: Microsoft Foundation 클래스 라이브러리 샘플)에서 실행되는 동안 현재 디렉터리에서 임시 파일에 데이터를 캐시하려고 시도하는 경우 SQLSTATE HY000(파일 버퍼를 만들 수 없음)이 반환됩니다.
