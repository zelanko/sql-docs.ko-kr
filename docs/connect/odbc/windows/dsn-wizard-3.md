---
description: 데이터 원본 마법사 화면 3(ODBC Driver for SQL Server)
title: 데이터 원본 마법사 화면 3(ODBC Driver for SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 09/27/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 48b65f57ac4a47a372ff82db4bc92f5ee631ea36
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88462198"
---
# <a name="data-source-wizard-screen-3"></a>데이터 원본 마법사 화면 3

기본 데이터베이스, 드라이버에 사용할 다양한 ANSI 옵션 및 미러 서버의 이름을 지정합니다.

## <a name="options"></a>옵션

### <a name="change-the-default-database-to"></a>기본 데이터베이스를 다음으로 변경

이 데이터 원본을 사용하여 설정된 모든 연결에 대한 기본 데이터베이스의 이름을 지정합니다. 이 확인란을 선택하지 않으면 서버의 로그인 ID에 대해 정의된 기본 데이터베이스가 연결에 사용됩니다. 이 확인란을 선택하면 상자에 이름이 지정된 데이터베이스가 로그인 ID에 대해 정의된 기본 데이터베이스를 덮어씁니다. **데이터베이스 파일 이름 첨부** 상자에 주 파일의 이름이 있는 경우 주 파일에 기술된 데이터베이스가 **기본 데이터베이스를 다음으로 변경** 상자에 지정된 데이터베이스 이름을 사용하여 데이터베이스로 연결됩니다.

ODBC 데이터 원본의 기본 데이터베이스를 지정하는 것보다 로그인 ID에 대한 기본 데이터베이스를 사용하는 것이 더 효율적입니다.

### <a name="mirror-server"></a>미러 서버

미러되는 데이터베이스의 장애 조치(failover) 파트너 이름을 지정합니다. 데이터베이스 이름이 **기본 데이터베이스를 다음으로 변경** 상자에 표시되지 않거나 표시된 이름이 기본 데이터베이스인 경우 **미러 서버**는 회색으로 나타납니다.

필요에 따라 미러 서버에 대한 SPN(서버 보안 주체 이름)을 지정할 수 있습니다. 미러 서버에 대한 SPN은 클라이언트와 서버 간의 상호 인증에 사용됩니다.

### <a name="attach-database-filename"></a>데이터베이스 파일 이름 첨부

연결할 수 있는 데이터베이스에 대한 주 파일의 이름을 지정합니다. 이 데이터베이스는 데이터 원본에 대한 기본 데이터베이스로 연결되어 사용됩니다. 주 파일에 대한 전체 경로와 파일 이름을 지정하십시오. **기본 데이터베이스를 다음으로 변경** 상자에 지정된 데이터베이스 이름은 연결된 데이터베이스의 이름으로 사용됩니다.

### <a name="use-ansi-quoted-identifiers"></a>따옴표가 붙은 ANSI 식별자 사용

ODBC Driver for SQL Server가 연결될 때 QUOTED_IDENTIFIERS가 설정되도록 지정합니다. 이 확인란을 선택하면 SQL Server에서 따옴표에 대한 ANSI 규칙을 적용합니다. 큰따옴표는 열 및 테이블 이름과 같은 식별자에만 사용할 수 있습니다. 문자열은 다음과 같이 작은따옴표로 감싸야 합니다.

```
SELECT "LastName"
FROM "Person.Contact"
WHERE "LastName" = 'O''Brien'
```

이 확인란을 선택하지 않으면 Microsoft Excel과 함께 제공되는 Microsoft 쿼리 유틸리티와 같이 따옴표가 붙은 식별자를 사용하는 애플리케이션에서는 따옴표가 붙은 식별자가 있는 SQL 문을 생성할 때 오류가 발생합니다.

### <a name="use-ansi-nulls-paddings-and-warnings"></a>ANSI 널, 채움 문자 및 경고 사용

ODBC Driver for SQL Server가 연결될 때 ANSI_NULLS, ANSI_WARNINGS 및 ANSI_PADDINGS 옵션이 설정되도록 지정합니다.

ANSI_NULLS가 설정되면 서버는 NULL 열 비교에 대한 ANSI 규칙을 적용합니다. 모든 NULL 비교에 ANSI 구문 "IS NULL" 또는 "IS NOT NULL"을 사용해야 합니다. Transact-SQL 구문 "= NULL"은 지원되지 않습니다.

ANSI_WARNINGS가 설정되면 SQL Server는 ANSI 규칙은 위반하지만 Transact-SQL 규칙은 위반하지 않는 조건에 대해 경고 메시지를 표시합니다. 이러한 오류의 예로는 INSERT 또는 UPDATE 문 실행 시 데이터가 잘리는 경우나 집계 함수 중간에 Null 값이 발견되는 경우가 있습니다. 

ANSI_PADDING이 설정되면 **varchar** 값의 후행 공백과 **varbinary** 값의 후행 0이 자동으로 잘리지 않습니다.

### <a name="application-intent"></a>애플리케이션 의도

서버에 연결할 때 애플리케이션 작업 유형을 선언합니다. 가능한 값은 **ReadOnly** 및 **ReadWrite**입니다.

### <a name="multi-subnet-failover"></a>다중 서브넷 장애 조치(failover)

애플리케이션이 다른 서브넷의 고가용성 재해 복구(AlwaysOn 가용성 그룹) 가용성 그룹(AG)에 연결되어 있는 경우 **다중 서브넷 장애 조치(failover)** 를 사용하도록 설정합니다. 현재 활성 상태인 서버를 더 빠르게 검색하고 연결할 수 있도록 ODBC Driver for SQL Server를 구성합니다.

### <a name="transparent-network-ip-resolution"></a>투명 네트워크 IP 확인.

장애 조치(failover) 중에 더 빠르게 다시 연결할 수 있도록 **다중 서브넷 장애 조치(failover)** 동작을 변경합니다. 자세한 내용은 [투명한 네트워크 IP 확인 사용](../../../connect/odbc/using-transparent-network-ip-resolution.md)을 참조하세요.

### <a name="column-encryption"></a>열 암호화.

SQL Server 2016 이상에서 제공되는 [Always Encrypted](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) 기능으로 열에 대한 데이터 전송의 자동 암호화 및 암호 해독을 사용하도록 설정합니다.

### <a name="use-fmtonly-metadata-discovery"></a>FMTONLY 메타데이터 검색을 사용합니다.

SQL Server 2012 이상에 연결하는 경우 레거시 SET FMTONLY 메타데이터 검색 방법을 사용합니다. 임시 테이블이 포함된 쿼리와 같이 [sp_describe_first_result_set](../../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)에서 지원되지 않는 쿼리를 사용하는 경우에만 사용하도록 설정합니다. 

### <a name="next"></a>다음

마법사의 다음 화면으로 진행합니다.

### <a name="back"></a>뒤로

마법사의 이전 화면으로 돌아갑니다.

## <a name="next-steps"></a>다음 단계

[데이터 원본 마법사 화면 2](../../../connect/odbc/windows/dsn-wizard-2.md)

[데이터 원본 마법사 화면 4](../../../connect/odbc/windows/dsn-wizard-4.md)
