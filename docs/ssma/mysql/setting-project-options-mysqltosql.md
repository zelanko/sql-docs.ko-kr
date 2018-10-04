---
title: 프로젝트 옵션 (MySQLToSQL) 설정 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Setting project options,configuration options
ms.assetid: 08820d88-e157-4d49-9401-38580dd7ec2d
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 56e7a30725a4fcad36ffa2df869ecc559056a29e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47819231"
---
# <a name="setting-project-options-mysqltosql"></a>프로젝트 옵션 설정(MySQLToSQL)
각 SSMA 프로젝트에 대 한 프로젝트 수준 옵션을 설정할 수 있습니다. 이러한 옵션에는 개체를 변환 하는 방법을, 데이터가 마이그레이션되는 방식 및 원본 데이터 형식을 대상 데이터 형식에 매핑하는 방법을 지정 합니다.  SQL Server 또는 SQL Azure 개체를 변환 하거나 SQL Server 또는 SQL Azure 데이터를 마이그레이션할 하기 전에 구성 옵션을 프로젝트에 적절 하 게 확인 합니다.  
  
SSMA를 사용 하면 모든 프로젝트에 대 한 기본 옵션을 구성할 수 있습니다. 이러한 옵션은 사용자가 만든 모든 새 프로젝트에 적용 됩니다. 그런 다음 각 프로젝트에 대 한 옵션을 사용자 지정할 수 있습니다.  
  
## <a name="configuration-options-and-modes"></a>구성 옵션 및 모드  
SSMA는 프로젝트 설정의 5 개 집합에 있습니다.  
  
-   프로젝트 정보  
  
-   일반 (변환, 마이그레이션 및 SQL Azure)  
  
-   Synchronization  
  
-   GUI  
  
-   형식 매핑  
  
프로젝트 설정 네 가지 방법으로 구성할 수 있습니다.  
  
-   Default  
  
-   Optimistic  
  
-   전체  
  
-   사용자 지정  
  
대부분의 사용자에 대 한 기본 모드를 사용 하는 것이 좋습니다. 최적 모드 현재 MySQL 구문의 자세히 유지 및 읽기가 쉽습니다. 그러나 현재 구문을 유지 정확 하지 않을 합니다. MySQL 구문을 해야 SQL Server 또는 SQL Azure 대 한 해당 구문을 변환할 수 있으면 전체 모드를 가장 완벽 변환을 수행 합니다. 그러나 결과 코드를 않을 읽기가 더 어려워집니다. 사용자 지정 모드로 옵션을 설정할 수 있습니다.  
  
설정 및 각 모드에는 설정 적용 방법에 대 한 자세한 내용은 다음 항목을 참조 합니다.  
  
-   [프로젝트 설정 &#40;변환&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
  
-   [프로젝트 설정 &#40;마이그레이션&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-migration-mysqltosql.md)  
  
-   [프로젝트 설정 (GUI) (SSMA 공통)](http://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693)  
  
-   [프로젝트 설정 &#40;형식 매핑&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md)  
  
-   [프로젝트 설정 &#40;동기화&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-synchronization-mysqltosql.md)  
  
-   [프로젝트 설정 &#40;Azure SQL DB&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-azure-sql-db-mysqltosql.md)  
  
## <a name="setting-project-options"></a>프로젝트 옵션 설정  
SSMA에 모든 프로젝트에 대 한 기본 설정을 구성할 수 있습니다. 이러한 설정은 SSMA 구성 파일에 저장 되며 사용자가 만든 모든 새 프로젝트에 적용 됩니다.  
  
**기본 프로젝트 옵션을 설정 하려면**  
  
1.  에 **도구** 메뉴에서 클릭 **기본 프로젝트 설정**합니다.  
  
2.  에 **기본 프로젝트 설정** 대화 상자에서 다음 절차 중 하나를 사용 합니다.  
  
    1.  설정을 볼 /에서 변경 하는 데 필요한는 마이그레이션 프로젝트 형식을 선택 **마이그레이션 대상 버전** 드롭다운을 클릭 합니다 **일반** 선택 고왼쪽된창맨아래에**변환 또는 SQL Azure 마이그레이션** 옵션입니다.  
  
    2.  미리 정의 된 모드를 선택 하려면 **기본**를 **Optimistic**, 또는 **전체** 에서 **모드** 드롭다운 목록 상자입니다.  
  
    3.  사용자 지정 설정을 지정 하려면 선택 하거나 새 설정이 나 값을 입력 합니다.  
  
3.  클릭 **확인** 설정을 저장 합니다.  
  
현재 프로젝트에 대 한 설정을 사용자 지정할 수도 있습니다. 현재 프로젝트 파일에 설정은 저장 합니다.  
  
**현재 프로젝트에 대 한 설정을 사용자 지정 하려면**  
  
1.  에 **도구** 메뉴에서 클릭 **ProjectSettings**합니다.  
  
2.  에 **ProjectSettings** 대화 상자에서 다음 절차 중 하나를 사용 합니다.  
  
    1.  미리 정의 된 모드를 선택 하려면 **기본**를 **Optimistic**, 또는 **전체** 에서 **모드** 드롭다운 목록 상자입니다.  
  
    2.  사용자 지정 모드를 지정 하려면 **사용자 지정** 에서 합니다 **모드** 드롭다운 목록 상자입니다. 선택한 후 적절 한 프로젝트 설정 합니다.  
  
3.  클릭 **확인** 설정을 저장 합니다.  
  
## <a name="next-step"></a>다음 단계  
다음 단계는 마이그레이션 프로젝트 요구 사항에 따라 달라 집니다.  
  
-   원본 및 대상 데이터 형식 매핑 사용자 지정을 참조 하세요 [매핑 MySQL 및 SQL Server 데이터 형식 &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   그렇지 않은 경우 SQL Server 또는 SQL Azure 개체 정의에 MySQL 데이터베이스 개체 정의 변환할 수 있습니다. 자세한 내용은 [MySQL 데이터베이스 변환 &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>관련 항목  
[MySQL 및 SQL Server 데이터 형식 매핑 &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
