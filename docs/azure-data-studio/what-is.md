---
title: Azure Data Studio 란? | Microsoft Docs
description: Azure Data Studio는 SQL Server, Azure SQL Database 및 Azure SQL Data Warehouse; 관리에 대 한 Windows, macOS 및 Linux에서 실행 되는 무료, 간단한 도구 실행 중인 위치 합니다.
ms.custom: tools|sos
ms.date: 09/24/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: overview
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 93e1eae9c920a06f24d19a3f2757a7afaa7ca968
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "48039145"
---
# <a name="what-is-includename-sosincludesname-sosmd"></a>이란 [!INCLUDE[name-sos](../includes/name-sos.md)]?

Azure 데이터 스튜디오는 플랫폼 간 도구를 온-프레미스 Microsoft 제품군을 사용 하 여 데이터 전문가 위한 데이터베이스 및 클라우드 데이터 플랫폼에서 Windows, MacOS 및 Linux입니다.

SQL Operations Studio 미리 보기 이름으로 이전에 릴리스된, Azure Data Studio는 Intellisense, 코드 조각, 소스 제어 통합 및 통합된 된 터미널을 사용 하 여 최신 편집기 환경을 제공 합니다. 엔지니어링 되어 염두, 데이터 플랫폼 사용자를 사용 하 여 사용 하 여 쿼리 결과 집합을 사용자 지정 가능한 대시보드 차트에 기본 제공 합니다.

**[다운로드 및 설치 [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md)**


## <a name="transact-sql-t-sql-code-editor-with-intellisense"></a>IntelliSense 사용 하 여 TRANSACT-SQL (T-SQL) 코드 편집기

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 최신, 키보드 포커스 T-SQL 코딩 환경을 제공 하는 다중 탭 창는 풍부한 T-SQL 편집기, IntelliSense, 키워드 완성, 코드 조각, 코드 탐색 및 소스 제어와 같은 기본 제공 기능을 사용 하 여 일상적인 작업을 쉽게 (Git)를 통합 합니다. 주문형으로 T-SQL 쿼리를 실행 하 고 보고 텍스트, JSON 또는 Excel로 결과 저장 합니다. 데이터 편집, 원하는 데이터베이스 연결 구성 및 데이터베이스 개체를 익숙한 개체 탐색 환경에서 찾아보기 T-SQL 편집기를 사용 하는 방법에 알아보려면 참조 [T-SQL 편집기를 사용 하 여 데이터베이스 개체를 만드는](tutorial-sql-editor.md)합니다.

## <a name="smart-t-sql-code-snippets"></a>스마트 T-SQL 코드 조각

T-SQL 코드 조각을 데이터베이스, 테이블, 뷰, 저장된 프로시저, 사용자, 로그인, 역할, 등을 만들고 기존 데이터베이스 개체를 업데이트 하려면 적절 한 T-SQL 구문을 생성 합니다. 개발 또는 테스트 목적으로 데이터베이스의 복사본을 신속히 생성 하 고 실행을 사용 하 여 스마트 코드 조각을 만들고 스크립트를 삽입 합니다.

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 또한 사용자 지정 T-SQL 코드 조각을 작성 하는 기능을 제공 합니다. 자세한 내용은 참조 하세요 [만들기 및 사용 하 여 코드 조각을](code-snippets.md)합니다.


## <a name="customizable-server-and-database-dashboards"></a>사용자 지정 가능한 서버 및 데이터베이스 대시보드

모니터링 하 고 데이터베이스의 성능 병목 상태를 신속 하 게 해결 하는 다양 한 사용자 지정 가능한 대시보드를 만듭니다. 정보 위젯 및 데이터베이스 (및 서버) 대시보드에 대 한 자세한 내용은 참조 하세요 [관리 서버 및 데이터베이스 정보 위젯](insight-widgets.md)합니다.

## <a name="connection-management-server-groups"></a>연결 관리 (서버 그룹)

서버 그룹에는 서버 및 데이터베이스를 사용 하 여 작업에 대 한 연결 정보를 구성 하는 방법을 제공 합니다. 자세한 내용은 참조 하세요 [서버 그룹](server-groups.md)합니다.

## <a name="integrated-terminal"></a>통합된 터미널

선호 하는 명령줄 도구를 사용 하 여 (예를 들어, Bash, PowerShell, sqlcmd, bcp 및 ssh) 내에서 통합 터미널 창에는 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 사용자 인터페이스입니다. 통합된 터미널에 대해 알아보려면 [통합 터미널 통합](terminal.md) 을 참조 하십시오.

## <a name="extensibility-and-extension-authoring"></a>확장성 및 확장 작성

향상 된 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 기본 설치의 기능을 확장 하 여 환경입니다. [!INCLUDE[name-sos](../includes/name-sos-short.md)] 확장 제작에 대 한 지원 뿐만 아니라 데이터 관리 작업에 대 한 확장성 지점을 제공합니다.

확장성에 대해 자세히 알아보려면 [!INCLUDE[name-sos](../includes/name-sos-short.md)]를 참조 하세요 [확장성](extensibility.md)합니다.
확장을 작성 하는 방법에 대 한 자세한 참조 [확장 제작](extension-authoring.md)합니다.




## <a name="next-steps"></a>다음 단계
- [다운로드 및 설치 [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md)
- [연결 및 SQL Server 쿼리](quickstart-sql-server.md)
- [Azure SQL Database 연결 및 쿼리](quickstart-sql-database.md)
