---
description: MSSQLSERVER_3859
title: MSSQLSERVER_3859
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3859 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 4a3857e9e98bfbe7fcc86ee07272698f0fcac763
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418775"
---
# <a name="mssqlserver_3859"></a>MSSQLSERVER_3859
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>세부 정보

|attribute|값|
|---|---|
|제품 이름|SQL Server|
|이벤트 ID|3859|
|이벤트 원본|MSSQLSERVER|
|구성 요소|SQLEngine|
|심볼 이름|DBCC_CHECKCAT_DIRECT_UPDATE|
|메시지 텍스트|경고: 시스템 카탈로그가 데이터베이스 ID \%d에서 직접 업데이트되었습니다. 가장 최근 업데이트 날짜는 %S_DATE입니다.|
||

## <a name="explanation"></a>설명

이 오류는 사용자가 시스템 테이블 변경을 시작했음을 나타냅니다. 시스템 테이블을 수동으로 업데이트할 수는 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 엔진을 통한 시스템 테이블 업데이트만 가능합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용자가 시작한 시스템 테이블 변경을 감지할 경우 다음 두 가지 시나리오에서 오류 3859가 발생합니다.

- 시나리오 1

    수동으로 업데이트된 시스템 테이블을 포함하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 시작할 때 이벤트 뷰어의 애플리케이션 로그 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 다음과 같은 이벤트가 로그됩니다.

    > 로그 이름: 애플리케이션  
    원본: MSSQLSERVER 이벤트 ID: 3859  
    태스크 범주: 서버  
    수준: 정보  
    설명: 경고: 시스템 카탈로그가 데이터베이스 ID \%d에서 직접 업데이트되었습니다. 최근 업데이트 날짜는 **date_time** 입니다.  

- 시나리오 2  

    시스템 테이블을 수동으로 업데이트한 후 `DBCC_CHECKDB` 명령을 실행하면 다음과 같은 경고 메시지가 반환됩니다.

    > ‘ **database_name** ’의 DBCC 결과입니다.  
    메시지 8992, 수준 16, 상태 1, 줄 1  
    카탈로그 검사 메시지 3859, 상태 1: 경고: 시스템 카탈로그가 데이터베이스 ID \%d에서 직접 업데이트되었습니다. 최근 업데이트 날짜는 **date_time** 입니다.  
    CHECKDB가 ‘ **db_name** ’ 데이터베이스에서 할당 오류 0개와 일관성 오류 0개를 찾았습니다.  
    DBCC 실행이 완료되었습니다. DBCC에서 오류 메시지를 출력하면 시스템 관리자에게 문의하십시오.

## <a name="user-action"></a>사용자 조치

이 문제를 해결하려면 다음 방법 중 하나를 사용합니다.

- 방법 1

    데이터베이스의 새 백업이 있는 경우 백업에서 데이터베이스를 복원합니다.  
    > [!NOTE]
    > 이 방법은 백업의 메타데이터에 불일치가 없는 경우에만 사용할 수 있습니다.  

- 방법 2  

    백업에서 데이터베이스를 복원할 수 없는 경우 데이터와 개체를 새 데이터베이스로 내보냅니다. 그런 다음, 수동으로 업데이트된 데이터베이스의 내용을 새 데이터베이스로 전송합니다. 참고: DBCC CHECKDB 명령에 REPAIR 옵션을 사용하여 시스템 카탈로그의 불일치를 복구할 수는 없습니다. 따라서 이 명령은 메타데이터 손상을 복구할 수 없기 때문에 권장 복구 수준을 제공하지 않습니다.

    > [!NOTE]
    > 시스템 카탈로그 뷰를 통해 시스템 테이블의 데이터를 볼 수 있습니다.

## <a name="more-information"></a>자세한 정보

자세한 내용은 다음을 참조하세요. [시스템 기본 테이블](/sql/relational-databases/system-tables/system-base-tables)
