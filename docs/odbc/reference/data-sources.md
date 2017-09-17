---
title: "데이터 소스 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data sources [ODBC]
- data sources [ODBC], about data sources
ms.assetid: 4ae44fa2-0b9b-4e19-ab45-c1dc93b68406
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 179efeac4673884e615648d1ed118398132dc6f9
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="data-sources"></a>데이터 원본
A *데이터 소스* 데이터의 원본을 하기만 하면 됩니다. 라이브 데이터 피드의 또는 DBMS에 있는 특정 데이터베이스 파일을 수 있습니다. 데이터에는 프로그램과 동일한 컴퓨터에서 또는 네트워크의 임의 위치에서 다른 컴퓨터에 있을 수 있습니다. 예를 들어 데이터 원본 액세스 하 여 Novell® Netware; OS/2® 운영 체제에서 실행 되는 Oracle DBMS 됩니다. 게이트웨이;를 통해 액세스 하는 IBM DB2 DBMS 서버 디렉터리;에 있는 Xbase 파일의 컬렉션 또는 로컬 Microsoft® Access 데이터베이스 파일을 추가 합니다.  
  
 목적은 데이터 원본의 데이터에 액세스 하는 데 필요한 기술 정보를 모두 수집 하는 것-드라이버 이름, 네트워크 주소, 네트워크 소프트웨어 등에-단일 배치 하 고 사용자 로부터 숨길입니다. 사용자는 급여, 인벤토리 및 담당자를 포함 하는 목록에서 급여 목록에서 선택한 프로그램이 있는 급여 데이터 나 응용 프로그램에 도달한 방법을 알 없이 모두 급여 데이터에 연결 하 고 응용 프로그램 수 있어야 합니다.  
  
 용어 *데이터 소스* 와 유사한 단어 혼동 해서는 안 됩니다. 이 설명서에서는 *DBMS* 또는 *데이터베이스* 데이터베이스 프로그램 또는 엔진을 가리킵니다. 추가 구분할지 간의 *데스크톱 데이터베이스* 개인용 컴퓨터에서 실행 되도록 디자인 되 고 전체 SQL 및 트랜잭션 지원, 불완전 한 종종 및 *서버 데이터베이스* 클라이언트에서 실행 되도록 설계 / 서버 환경 및 특징은 독립 실행형 데이터베이스 엔진 및 다양 한 SQL 및 트랜잭션 지원 합니다. *데이터베이스* Xbase 파일의 파일 디렉터리 또는 데이터베이스에 SQL Server의 컬렉션에 같은 데이터의 특정 컬렉션을 의미 하기도 합니다. 용어는 일반적으로 동일 *카탈로그* 이 manual 또는 용어에 사용 되는 *한정자* 이전 버전의 ODBC 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [데이터 원본 유형](../../odbc/reference/types-of-data-sources.md)  
  
-   [데이터 원본 사용](../../odbc/reference/using-data-sources.md)  
  
-   [데이터 원본 예제](../../odbc/reference/data-source-example.md)
