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
ms.openlocfilehash: 5d123bdf1ea3357a4846a223c41950c952c1af2d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67915530"
---
# <a name="odbc-driver-architecture"></a>ODBC 드라이버 아키텍처
드라이버 작성자는 드라이버 아키텍처가 응용 프로그램에서 DBMS 관련 SQL을 사용할 수 있는지 여부에 영향을 줄 수 있음을 알고 있어야 합니다.  
  
 ![ODBC 드라이버 아키텍처 표시](../../../odbc/reference/develop-driver/media/odbcdriverovruarch.gif "ODBCDriverOvruArch")  
  
 [파일 기반 드라이버](../../../odbc/reference/file-based-drivers.md)  
  
 드라이버가 물리적 데이터에 직접 액세스 하는 경우 드라이버는 드라이버 및 데이터 원본 역할을 합니다. 드라이버는 ODBC 호출과 SQL 문을 모두 처리 해야 합니다. 파일 기반 드라이버의 개발자는 자신의 데이터베이스 엔진을 작성 해야 합니다.  
  
 [DBMS 기반 드라이버](../../../odbc/reference/dbms-based-drivers.md)  
  
 물리적 데이터에 액세스 하기 위해 별도의 데이터베이스 엔진을 사용 하는 경우 드라이버는 ODBC 호출만 처리 합니다. 처리를 위해 SQL 문을 데이터베이스 엔진에 전달 합니다.  
  
 [네트워크 아키텍처](../../../odbc/reference/network-example.md)  
  
 파일 및 DBMS ODBC 구성은 단일 네트워크에 있을 수 있습니다.  
  
 [기타 드라이버 아키텍처](../../../odbc/reference/other-driver-architectures.md)  
  
 다양 한 데이터 원본에서 작동 하는 데 필요한 드라이버는 미들웨어로 사용할 수 있습니다. 유형이 다른 조인 엔진 아키텍처를 사용 하면 드라이버가 드라이버 관리자로 표시 될 수 있습니다. 드라이버는 일련의 클라이언트에서 공유할 수 있는 서버에 설치할 수도 있습니다.  
  
 드라이버 아키텍처에 대 한 자세한 내용은 [ODBC 아키텍처](../../../odbc/reference/odbc-architecture.md)섹션의 [드라이버 관리자](../../../odbc/reference/the-driver-manager.md) 및 [드라이버 아키텍처](../../../odbc/reference/driver-architecture.md) 를 참조 하세요.  
  
 드라이버 문제에 대 한 자세한 내용은 다음 표에 설명 된 위치에서 찾을 수 있습니다.  
  
|문제|항목|위치|  
|-----------|-----------|--------------|  
|응용 프로그램 및 드라이버와의 호환성 문제|[응용 프로그램/드라이버 호환성](../../../odbc/reference/develop-app/application-and-driver-compatibility.md)|ODBC 프로그래머 참조의 [프로그래밍 고려 사항](../../../odbc/reference/develop-app/programming-considerations.md)|  
|ODBC 드라이버 작성|[ODBC 3.x 드라이버 작성](../../../odbc/reference/develop-app/writing-odbc-3-x-drivers.md)|ODBC 프로그래머 참조의 [프로그래밍 고려 사항](../../../odbc/reference/develop-app/programming-considerations.md)|  
|이전 버전과의 호환성을 위한 드라이버 지침|[이전 버전과의 호환성을 위한 드라이버 지침](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md)|[부록 G: ODBC 프로그래머 참조의 이전 버전과의 호환성을 위한 드라이버 지침](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md)|  
|드라이버에 연결|[데이터 원본 또는 드라이버 선택](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)|ODBC 프로그래머 참조에서 [데이터 원본 또는 드라이버에 연결](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)|  
|드라이버 식별|[드라이버 보기](../../../odbc/admin/viewing-drivers.md)|Microsoft ODBC 데이터 원본 관리자 온라인 도움말에서 [드라이버 보기](../../../odbc/admin/viewing-drivers.md)|  
|연결 풀링 사용|[ODBC 연결 풀링](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)|ODBC 프로그래머 참조에서 [데이터 원본 또는 드라이버에 연결](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)|  
|유니코드/o d e/ANSI 드라이버 및 연결 문제|[유니코드 드라이버](../../../odbc/reference/develop-app/unicode-drivers.md)|ODBC 프로그래머 참조의 [프로그래밍 고려 사항](../../../odbc/reference/develop-app/programming-considerations.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
