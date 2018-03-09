---
title: "데이터 소스를 사용 하 여 | Microsoft Docs"
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
helpviewer_keywords: data sources [ODBC], about data sources
ms.assetid: d5550619-22b2-4b16-bd08-fbabb6554c40
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a9ef21a59be0b292912a6ca4b4fc75a67dc952fb
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="using-data-sources"></a>데이터 원본 사용
호출 프로그램으로 기술 지원 담당자 또는 데이터 원본 일반적으로 최종 사용자가 만든는 *ODBC 관리자*합니다. ODBC 관리자를 사용 하도록 드라이버에 대 한 사용자를 해당 드라이버를 호출 합니다. 드라이버는 데이터 원본에 연결 하는 데 필요한 정보를 요청 하는 대화 상자를 표시 합니다. 사용자가 정보를 입력 한 후 드라이버가 시스템에 저장 합니다.  
  
 이상에서는 응용 프로그램 드라이버 관리자를 호출 하는 컴퓨터 데이터 원본의 이름 또는 파일 데이터 원본을 포함 하는 파일의 경로 전달 합니다. 시스템 데이터 원본 이름 전달 되는 경우 드라이버 관리자는 시스템 데이터 원본에 의해 사용 되는 드라이버를 찾을 수를 검색 합니다. 다음 드라이버를 로드 하 고 데이터 원본 이름에 전달 합니다. 드라이버는 데이터 원본 이름을 사용 하 여 데이터 원본에 연결 하는 데 필요한 정보를 찾을 수 있습니다. 마지막으로, 일반적으로 일반적으로 저장 되지 않은 사용자 ID와 암호를 사용자에 게 확인 데이터 원본에 연결 합니다.  
  
 파일 데이터 원본을 전달 되는 경우 드라이버 관리자는 파일을 열고 지정된 된 드라이버를 로드 합니다. 파일 연결 문자열도 있으면 것이 드라이버에 전달 합니다. 드라이버 정보를 사용 하 여 연결 문자열에, 데이터 원본에 연결 합니다. 연결 문자열이 전달 된 경우 드라이버 메시지 일반적으로 사용자에 게 필요한 정보를 표시 합니다.
