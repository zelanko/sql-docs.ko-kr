---
title: "ODBC 드라이버 아키텍처 | Microsoft Docs"
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
helpviewer_keywords: ODBC drivers [ODBC], architecture
ms.assetid: 21a62c7c-192e-4718-a16e-aa12b0de4419
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 69d4103e9f04da7775f38b436b009f8a3c06a962
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="odbc-driver-architecture"></a>ODBC 드라이버 아키텍처
드라이버 작성자 응용 프로그램 특정 DBMS SQL을 사용할 수 있는지 여부를 드라이버 아키텍처 수에 영향을 알고 있어야 합니다.  
  
 ![ODBC 드라이버 아키텍처 표시](../../../odbc/reference/develop-driver/media/odbcdriverovruarch.gif "ODBCDriverOvruArch")  
  
 [파일 기반 드라이버](../../../odbc/reference/file-based-drivers.md)  
  
 드라이버는 실제 데이터에 직접 액세스 드라이버가 드라이버와 데이터 원본으로 작동 합니다. 드라이버는 ODBC 호출과 SQL 문을 처리 해야 합니다. 파일 기반 드라이버의 개발자가 자신의 데이터베이스 엔진을 작성 해야 합니다.  
  
 [DBMS 기반 드라이버](../../../odbc/reference/dbms-based-drivers.md)  
  
 실제 데이터에 액세스 하는 별도 데이터베이스 엔진을 사용 하면 드라이버만 ODBC 호출을 처리 합니다. SQL 문을에 전달 하도록 데이터베이스 엔진을 처리 합니다.  
  
 [네트워크 아키텍처](../../../odbc/reference/network-example.md)  
  
 파일 및 DBMS ODBC 구성 단일 네트워크에 있을 수 있습니다.  
  
 [기타 드라이버 아키텍처](../../../odbc/reference/other-driver-architectures.md)  
  
 드라이버는 다양 한 데이터 원본 사용 해야 하는 경우 미들웨어로 사용할 수 있습니다. 형식이 다른 조인 엔진 아키텍처 드라이버 관리자도 표시 하는 드라이버를 만들 수 있습니다. 서버, 클라이언트의 계열 공유할 수에 드라이버를 설치할 수도 있습니다.  
  
 드라이버 아키텍처에 대 한 자세한 내용은 참조 [드라이버 관리자](../../../odbc/reference/the-driver-manager.md) 및 [드라이버 아키텍처](../../../odbc/reference/driver-architecture.md) 섹션에서 [ODBC 아키텍처](../../../odbc/reference/odbc-architecture.md)합니다.  
  
 드라이버 문제에 대 한 자세한 내용은 다음 표에 설명 된 위치에서 찾을 수 있습니다.  
  
|문제점|항목|위치|  
|-----------|-----------|--------------|  
|응용 프로그램 및 드라이버와의 호환성 문제|[응용 프로그램/드라이버 호환성](../../../odbc/reference/develop-app/application-and-driver-compatibility.md)|[프로그래밍 고려 사항](../../../odbc/reference/develop-app/programming-considerations.md), ODBC 프로그래머 참조|  
|쓰기 ODBC 드라이버|[ODBC 3.x 드라이버 작성](../../../odbc/reference/develop-app/writing-odbc-3-x-drivers.md)|[프로그래밍 고려 사항](../../../odbc/reference/develop-app/programming-considerations.md), ODBC 프로그래머 참조|  
|이전 버전과 호환성에 대 한 드라이버 지침|[이전 버전과 호환성에 대 한 드라이버 지침](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md)|[부록 g: 이전 버전과 호환성에 대 한 드라이버 지침](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md), ODBC 프로그래머 참조|  
|드라이버에 연결|[데이터 원본 또는 드라이버 선택](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)|[연결에 대 한 데이터 원본이 나 드라이버](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md), ODBC 프로그래머 참조|  
|드라이버를 식별합니다.|[드라이버 보기](../../../odbc/admin/viewing-drivers.md)|[드라이버 보기](../../../odbc/admin/viewing-drivers.md), 온라인 Microsoft ODBC 데이터 원본 관리자 도움말|  
|연결 풀링을 사용 하도록 설정|[ODBC 연결 풀링](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)|[연결에 대 한 데이터 원본이 나 드라이버](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md), ODBC 프로그래머 참조|  
|유니코드/ANSI 드라이버 및 연결 문제|[유니코드 드라이버](../../../odbc/reference/develop-app/unicode-drivers.md)|[프로그래밍 고려 사항](../../../odbc/reference/develop-app/programming-considerations.md), ODBC 프로그래머 참조|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
