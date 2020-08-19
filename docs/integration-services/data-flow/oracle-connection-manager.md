---
description: Oracle 연결 관리자
title: Oracle 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 428ca450371e452081d548a64e26dba2bd29b3b5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88430745"
---
# <a name="oracle-connection-manager"></a>Oracle 연결 관리자

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

Oracle 연결 관리자를 사용하여 패키지에서는 Oracle 데이터베이스의 데이터를 추출하고 Oracle 데이터베이스에 데이터를 로드할 수 있습니다.

Oracle 연결 관리자의 **ConnectionManagerType** 속성이 **ORACLE**로 설정됩니다.

## <a name="configuring-the-oracle-connection-manager"></a>Oracle 연결 관리자 구성

Oracle 연결 관리자 구성 변경은 런타임에 Integration Services에서 확인됩니다. **Oracle 연결 관리자 편집기** 대화 상자를 사용하여 Oracle 데이터 원본에 대한 연결을 추가할 수 있습니다.

![연결 관리자](media/oracle-connection-manager.png)

### <a name="options"></a>옵션

#### <a name="connection-manager-information"></a>연결 관리자 정보

Oracle 연결에 대한 정보를 입력합니다.

**이름**

Oracle 연결의 이름을 입력합니다. 기본 이름은 Oracle 연결 관리자입니다. 

**설명** 

연결에 대한 설명을 입력합니다. 이 입력은 선택 사항입니다.

**TNS 서비스 이름**

작업하는 Oracle 데이터베이스의 이름을 입력합니다. TNS 서비스 이름은 다음과 같을 수 있습니다.

- Oracle 클라이언트의 admin 폴더에 있는 tnsnames.ora 파일에 정의된 연결 설명자 이름입니다.

- EzConnect format: [//]host[:port][/service_name]

자세한 내용은 Oracle 설명서를 참조하십시오.

#### <a name="connection-manager-logging"></a>연결 관리자 로깅

다음 옵션 중 하나를 선택합니다.

- **Windows 인증 사용**: Windows 인증을 사용하려면 선택합니다.

- **Oracle 인증 사용**: Oracle 데이터베이스 인증을 사용하려면 선택합니다. 이 인증을 사용하는 경우 다음과 같이 Oracle 자격 증명을 입력합니다.  
    **사용자 이름**: Oracle 데이터베이스에 연결하는 데 사용되는 사용자 이름을 입력합니다.  
    **암호**: 사용자 이름 필드에 입력한 사용자의 Oracle 데이터베이스 암호를 입력합니다.

> [!NOTE]
>
>Oracle Server 18c에서는 Windows 인증이 지원되지 않습니다.

**연결 테스트**

**연결 테스트**를 클릭하여 제공된 정보가 올바른지 확인합니다. 입력한 정보로 Oracle 데이터베이스에 연결할 수 있으면 **연결 테스트 성공** 메시지가 표시됩니다.

### <a name="custom-properties"></a>사용자 지정 속성

Oracle 연결 관리자에는 다음과 같은 사용자 지정 연결 관리자 속성이 있습니다.

- **EnableDetailedTracing**: 사용되지 않습니다.

- **OracleHome**: 커넥터에서 사용할 32비트 Oracle Home 이름 또는 폴더를 지정합니다. (선택 사항)

- **OracleHome64**: 64비트 모드로 실행될 때 커넥터에서 사용할 64비트 Oracle Home 이름 또는 폴더를 지정합니다. (선택 사항)

사용자 지정 속성은 Oracle 연결 관리자 편집기에 나열되지 않습니다. **OracleHome** 및 **OracleHome64** 속성을 설정하려면

1. 연결 관리자 영역에서 작업 중인 Oracle 연결 관리자를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.

2. **속성** 창에서 Oracle 홈 디렉터리에 대한 전체 경로를 사용하여 **OracleHome** 또는 **OracleHome64** 속성을 설정합니다.

## <a name="next-steps"></a>다음 단계

- [Oracle 원본](oracle-source.md)을 구성합니다.
- [Oracle 대상](oracle-destination.md)을 구성합니다.
- 질문이 있는 경우 [TechCommunity](https://aka.ms/AA5u35j)을 방문하세요.
