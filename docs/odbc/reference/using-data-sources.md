---
title: 데이터 원본을 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], about data sources
ms.assetid: d5550619-22b2-4b16-bd08-fbabb6554c40
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 52015cb202f46c50c16dcab408bed7761f0925db
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67951807"
---
# <a name="using-data-sources"></a>데이터 원본 사용
데이터 원본을 일반적으로 최종 사용자가 만든 또는 프로그램을 사용 하 여 기술자 라는 합니다 *ODBC 관리자*합니다. ODBC 관리자를 사용 하는 드라이버에 대 한 라는 하 고 해당 드라이버를 호출 합니다. 드라이버는 데이터 원본에 연결 하는 데 필요한 정보를 요청 하는 대화 상자를 표시 합니다. 사용자가 정보를 입력 한 후 드라이버 시스템에 저장 합니다.  
  
 나중에 응용 프로그램 드라이버 관리자를 호출 하는 컴퓨터 데이터 원본의 이름 또는 파일 데이터 원본을 포함 하는 파일의 경로 전달 합니다. 컴퓨터 데이터 원본 이름에 전달 되 면 드라이버 관리자는 시스템 데이터 원본에서 사용 되는 드라이버를 찾을 수를 검색 합니다. 그런 다음 드라이버를 로드 하 고 데이터 원본 이름에 전달 합니다. 드라이버는 데이터 원본에 연결 하는 데 필요한 정보를 찾을 데이터 원본 이름을 사용 합니다. 마지막으로, 일반적으로 저장 되지 않습니다는 사용자 ID 및 암호를 사용자에 게 일반적으로 데이터 원본에 연결 합니다.  
  
 파일 데이터 원본에 전달 되 면 드라이버 관리자는 파일이 열리고 지정된 된 드라이버를 로드 합니다. 파일 또한 연결 문자열에 있으면 것이 드라이버를 전달 합니다. 드라이버 정보를 사용 하 여 연결 문자열에, 데이터 원본에 연결 합니다. 연결 문자열을 전달 된 경우 드라이버는 일반적으로 필요한 정보에 대 한 사용자를 묻습니다.
