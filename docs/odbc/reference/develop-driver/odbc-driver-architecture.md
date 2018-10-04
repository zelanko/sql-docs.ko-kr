---
title: ODBC 드라이버 아키텍처 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], architecture
ms.assetid: 21a62c7c-192e-4718-a16e-aa12b0de4419
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 260767c88fdf980466a21d4cc9658b259b91c854
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47788151"
---
# <a name="odbc-driver-architecture"></a>ODBC 드라이버 아키텍처
드라이버 작성자는 드라이버 아키텍처 영향을 줄 수 응용 프로그램이 특정 DBMS SQL을 사용할 수 있는지 여부를 알고 있어야 합니다.  
  
 ![ODBC 드라이버 아키텍처를 보여 줍니다](../../../odbc/reference/develop-driver/media/odbcdriverovruarch.gif "ODBCDriverOvruArch")  
  
 [파일 기반 드라이버](../../../odbc/reference/file-based-drivers.md)  
  
 드라이버에서 실제 데이터에 직접 액세스 하는 경우 드라이버는 드라이버 및 데이터 원본으로 작동 합니다. 드라이버는 ODBC 호출 및 SQL 문을 처리 해야 합니다. 파일 기반 드라이버의 개발자가 자신의 데이터베이스 엔진을 작성 해야 합니다.  
  
 [DBMS 기반 드라이버](../../../odbc/reference/dbms-based-drivers.md)  
  
 실제 데이터에 액세스 하는 별도 데이터베이스 엔진 사용할 드라이버만 ODBC 호출을 처리 합니다. 전달 SQL 문을 데이터베이스 엔진으로 처리 합니다.  
  
 [네트워크 아키텍처](../../../odbc/reference/network-example.md)  
  
 파일 및 DBMS ODBC 구성을 단일 네트워크에 있을 수 있습니다.  
  
 [기타 드라이버 아키텍처](../../../odbc/reference/other-driver-architectures.md)  
  
 드라이버는 다양 한 데이터 원본 작업에 필요한 미들웨어를 사용할 수 있습니다. 형식이 다른 조인 엔진 아키텍처 드라이버 관리자를 표시 하는 드라이버를 만들 수 있습니다. 일련의 클라이언트를 통해 공유할 수 있는 서버에서 드라이버를 설치할 수도 있습니다.  
  
 드라이버 아키텍처에 대 한 자세한 내용은 참조 하세요. [드라이버 관리자](../../../odbc/reference/the-driver-manager.md) 하 고 [드라이버 아키텍처](../../../odbc/reference/driver-architecture.md) 섹션에서 [ODBC 아키텍처](../../../odbc/reference/odbc-architecture.md)합니다.  
  
 드라이버 문제에 대 한 자세한 내용은 다음 표에 나와 있는 위치에 있습니다.  
  
|문제점|항목|위치|  
|-----------|-----------|--------------|  
|응용 프로그램 및 드라이버를 사용 하 여 호환성 문제|[응용 프로그램/드라이버 호환성](../../../odbc/reference/develop-app/application-and-driver-compatibility.md)|[프로그래밍 고려 사항](../../../odbc/reference/develop-app/programming-considerations.md), ODBC 프로그래머 참조|  
|ODBC 드라이버 작성|[ODBC 3.x 드라이버 작성](../../../odbc/reference/develop-app/writing-odbc-3-x-drivers.md)|[프로그래밍 고려 사항](../../../odbc/reference/develop-app/programming-considerations.md), ODBC 프로그래머 참조|  
|이전 버전과 호환성에 대 한 드라이버 지침|[이전 버전과 호환성에 대 한 드라이버 지침](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md)|[부록 g: 이전 버전과 호환성에 대 한 드라이버 지침](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md), ODBC 프로그래머 참조|  
|드라이버에 연결|[데이터 원본 또는 드라이버 선택](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)|[연결에 대 한 데이터 원본이 나 드라이버](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md), ODBC 프로그래머 참조|  
|드라이버를 식별합니다.|[드라이버 보기](../../../odbc/admin/viewing-drivers.md)|[드라이버 보기](../../../odbc/admin/viewing-drivers.md), 온라인 Microsoft ODBC 데이터 원본 관리자 도움말|  
|연결 풀링을 사용 하도록 설정|[ODBC 연결 풀링](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)|[연결에 대 한 데이터 원본이 나 드라이버](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md), ODBC 프로그래머 참조|  
|유니코드/ANSI 드라이버 및 연결 문제|[유니코드 드라이버](../../../odbc/reference/develop-app/unicode-drivers.md)|[프로그래밍 고려 사항](../../../odbc/reference/develop-app/programming-considerations.md), ODBC 프로그래머 참조|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
