---
title: 데이터 소스 사용 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: df9b09e4c5519e0fff44902bd83b8e3d92a67ca8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286554"
---
# <a name="using-data-sources"></a>데이터 원본 사용
데이터 원본은 일반적으로 *ODBC 관리자라는*프로그램을 가진 최종 사용자 또는 기술자에 의해 만들어집니다. ODBC 관리자는 드라이버가 사용하도록 사용자에게 메시지를 표시한 다음 해당 드라이버를 호출합니다. 드라이버는 데이터 원본에 연결하는 데 필요한 정보를 요청하는 대화 상자를 표시합니다. 사용자가 정보를 입력하면 드라이버는 정보를 시스템에 저장합니다.  
  
 나중에 응용 프로그램은 Driver Manager를 호출하고 컴퓨터 데이터 원본의 이름 또는 파일 데이터 원본을 포함하는 파일의 경로를 전달합니다. 컴퓨터 데이터 원본 이름을 전달하면 드라이버 관리자는 시스템을 검색하여 데이터 원본에서 사용하는 드라이버를 찾습니다. 그런 다음 드라이버를 로드하고 데이터 원본 이름을 전달합니다. 드라이버는 데이터 원본 이름을 사용하여 데이터 원본에 연결하는 데 필요한 정보를 찾습니다. 마지막으로 데이터 원본에 연결하여 일반적으로 사용자에게 일반적으로 저장되지 않는 사용자 ID와 암호를 입력합니다.  
  
 파일 데이터 원본을 전달하면 드라이버 관리자가 파일을 열고 지정된 드라이버를 로드합니다. 파일에 연결 문자열도 포함되어 있으면 이 문자열을 드라이버에 전달합니다. 연결 문자열의 정보를 사용하여 드라이버는 데이터 원본에 연결합니다. 연결 문자열이 전달되지 않은 경우 드라이버는 일반적으로 사용자에게 필요한 정보를 묻는 메시지를 표시합니다.
