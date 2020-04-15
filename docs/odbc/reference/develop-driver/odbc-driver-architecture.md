---
title: ODBC 드라이버 아키텍처 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 712de6a7a3f80ce1cd3ca854a88765dbfa531356
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294561"
---
# <a name="odbc-driver-architecture"></a>ODBC 드라이버 아키텍처
드라이버 작성기는 드라이버 아키텍처가 응용 프로그램이 DBMS 관련 SQL을 사용할 수 있는지 여부에 영향을 줄 수 있다는 점에 유의해야 합니다.  
  
 ![ODBC 드라이버 아키텍처 표시](../../../odbc/reference/develop-driver/media/odbcdriverovruarch.gif "ODBC드라이버오브루아치")  
  
 [파일 기반 드라이버](../../../odbc/reference/file-based-drivers.md)  
  
 드라이버가 물리적 데이터에 직접 액세스하면 드라이버는 드라이버와 데이터 원본 모두의 역할을 합니다. 드라이버는 ODBC 호출과 SQL 문을 모두 처리해야 합니다. 파일 기반 드라이버의 개발자는 자체 데이터베이스 엔진을 작성해야 합니다.  
  
 [DBMS 기반 드라이버](../../../odbc/reference/dbms-based-drivers.md)  
  
 별도의 데이터베이스 엔진을 사용하여 물리적 데이터에 액세스하는 경우 드라이버는 ODBC 호출만 처리합니다. 처리를 위해 SQL 문을 데이터베이스 엔진에 전달합니다.  
  
 [네트워크 아키텍처](../../../odbc/reference/network-example.md)  
  
 파일 및 DBMS ODBC 구성은 단일 네트워크에 존재할 수 있습니다.  
  
 [기타 드라이버 아키텍처](../../../odbc/reference/other-driver-architectures.md)  
  
 드라이버가 다양한 데이터 원본으로 작업해야 하는 경우 미들웨어로 사용할 수 있습니다. 이기종 조인 엔진 아키텍처는 드라이버를 드라이버 관리자로 표시할 수 있습니다. 드라이버는 일련의 클라이언트에서 공유할 수 있는 서버에설치할 수도 있습니다.  
  
 드라이버 아키텍처에 대한 자세한 내용은 [ODBC 아키텍처](../../../odbc/reference/odbc-architecture.md)섹션의 [드라이버 관리자](../../../odbc/reference/the-driver-manager.md) 및 [드라이버 아키텍처를](../../../odbc/reference/driver-architecture.md) 참조하십시오.  
  
 드라이버 문제에 대한 자세한 내용은 다음 표에 설명된 위치에서 확인할 수 있습니다.  
  
|문제|항목|위치|  
|-----------|-----------|--------------|  
|응용 프로그램 및 드라이버와의 호환성 문제|[응용 프로그램/드라이버 호환성](../../../odbc/reference/develop-app/application-and-driver-compatibility.md)|[프로그래밍 고려 사항,](../../../odbc/reference/develop-app/programming-considerations.md)ODBC 프로그래머 참조|  
|ODBC 드라이버 쓰기|[ODBC 3.x 드라이버 작성](../../../odbc/reference/develop-app/writing-odbc-3-x-drivers.md)|[프로그래밍 고려 사항,](../../../odbc/reference/develop-app/programming-considerations.md)ODBC 프로그래머 참조|  
|이전 버전과의 호환성을 위한 드라이버 지침|[이전 버전과의 호환성을 위한 드라이버 지침](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md)|[부록 G: ODBC](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md)프로그래머의 참조에서 이전 버전과의 호환성을 위한 드라이버 지침|  
|드라이버에 연결|[데이터 원본 또는 드라이버 선택](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)|ODBC 프로그래머 의 참조에서 [데이터 원본 또는 드라이버에 연결](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)|  
|드라이버 식별|[드라이버 보기](../../../odbc/admin/viewing-drivers.md)|[드라이버 보기](../../../odbc/admin/viewing-drivers.md), Microsoft ODBC 데이터 원본 관리자 온라인 도움말|  
|연결 풀링 사용|[ODBC 연결 풀링](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)|ODBC 프로그래머 의 참조에서 [데이터 원본 또는 드라이버에 연결](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)|  
|유니코드/ANSI 드라이버 및 연결 문제|[유니코드 드라이버](../../../odbc/reference/develop-app/unicode-drivers.md)|[프로그래밍 고려 사항,](../../../odbc/reference/develop-app/programming-considerations.md)ODBC 프로그래머 참조|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
