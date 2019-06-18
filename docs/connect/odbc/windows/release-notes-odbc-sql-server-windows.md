---
title: Windows 기반 SQL Server에 대한 ODBC 릴리스 정보 | Microsoft Docs
ms.custom: ''
ms.date: 02/27/2019
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b8459ed8-625e-4d8b-891c-e7e78c9977cc
ms.reviewer: v-jizho2, v-chojas, genemi
author: v-makouz
ms.author: v-makouz
manager: kenvh
ms.openlocfilehash: f74d5a70325fdceb311bb3a45ba6824e64242ff0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63031211"
---
# <a name="release-notes-for-odbc-to-sql-server-on-windows"></a>Windows 기반 SQL Server에 대한 ODBC 릴리스 정보

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

이 릴리스 정보 문서에서는 Windows 기반 SQL Server에 대한 Microsoft ODBC 드라이버의 새로운 기능을 설명합니다.

<!--
PLEASE USE THE STANDARD 2-COLUMN TABLE FORMAT!

For all our Release Notes articles (What's New too?), we are standardizing on the 2-column format that you see here for version "## 17.3".

Going forward, all new additions to this article must use the 2-column format.

Also, use the shorter ## H2 title format, which eliminates all the redundant constants, and appends the date-added.
One beneift of shortness is the avoidance of the annoying wrapping of unnecessarily long H2 titles in the rightNav.
- OLD H2:  ## What's New in the [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17.3 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] on Windows
- NEW H2:  ## 17.3, February 2019

By the way, in GitHub, the file name is changing today 2019/03/30:
- FROM:  docs/connect/odbc/windows/release-notes.md
- TO  :  docs/connect/odbc/windows/release-notes-odbc-sql-server-windows.md

Thank you.
GeneMi (and CraigG).  2019/03/30.
-->

## <a name="173-february-2019"></a>17.3, 2019년 2월

| 추가된 기능 | 세부 정보 |
| :------------ | :------ |
| Azure Active Directory 관리 서비스 ID(시스템 및 사용자 할당) 인증 모드. | [ODBC 드라이버에서 Azure Active Directory 사용](../using-azure-active-directory.md)을 참조하세요. |
| Always Encrypted 열에 대해 입력 매개 변수를 스트리밍할 수 있음. | [Always Encrypted를 사용할 때 ODBC 드라이버의 제한 사항](../using-always-encrypted-with-the-odbc-driver.md#limitations-of-the-odbc-driver-when-using-always-encrypted)을 참조하세요. |
| XA 분산 트랜잭션. | [XA 트랜잭션 사용](../use-xa-with-dtc.md). |
| 버그 수정. | [버그 수정](../bug-fixes.md)을 참조하세요. |
| &nbsp; | &nbsp; |

## <a name="172-july-2018"></a>17.2, 2018년 7월

| 추가된 기능 | 세부 정보 |
| :------------ | :------ |
| Azure SQL Database 및 SQL Server에 대한 데이터 분류. | [데이터 분류](../data-classification.md)를 참조하세요. |
| UTF-8 서버 인코딩 지원. | &nbsp; |
| 버그 수정. | [버그 수정](../bug-fixes.md)을 참조하세요. |
| &nbsp; | &nbsp; |

## <a name="171-march-2018"></a>17.1, 2018년 3월

| 추가된 기능 | 세부 정보 |
| :------------ | :------ |
| `SQL_COPT_SS_CEKCACHETTL` 및 `SQL_COPT_SS_TRUSTEDCMKPATHS` 연결 특성 지원. | &bull; &nbsp; `SQL_COPT_SS_CEKCACHETTL`<br/>열 암호화 키의 로컬 캐시가 존재하는 경우 시간을 제어할 뿐만 아니라 플러시할 수도 있습니다.<br/><br/>&bull; &nbsp; `SQL_COPT_SS_TRUSTEDCMKPATHS`<br/>애플리케이션에서 AE 작업을 열 마스터 키의 지정된 목록만 사용하도록 제한할 수 있습니다.<br/><br/> 자세한 내용은 [SQL Server용 ODBC 드라이버와 함께 Always Encrypted 사용](../using-always-encrypted-with-the-odbc-driver.md)을 참조하세요. |
| Azure Active Directory 대화형 인증 지원 | &nbsp; |
| 버그 수정. | [버그 수정](../bug-fixes.md)을 참조하세요. |
| &nbsp; | &nbsp; |

## <a name="17-february-2018"></a>17, 2018년 2월

| 추가된 기능 | 세부 정보 |
| :------------ | :------ |
| BCP API에 대한 Always Encrypted 지원. | &nbsp; |
| 새 연결 문자열 특성 `UseFMTOnly`. | 임시 테이블이 필요한 특별한 경우 드라이버에서 구형 메타데이터를 사용하도록 합니다. |
| Azure SQL Managed Instance 지원. | 프라이빗 미리 보기 확장.<br/><br/>[Managed Instance를 사용하는 경우 차이점(ODBC 버전 17)](#diffs-managed-instance-17)에 대한 다음 목록을 참조하세요. |
| &nbsp; | &nbsp; |

| 종속성 변경 | 세부 정보 |
| :------------ | :------ |
| Microsoft 온라인 서비스 로그인 도우미 제거 | 종속성이 제거되었습니다. |
| &nbsp; | &nbsp; |

### <a name="diffs-managed-instance-17"></a> Managed Instance를 사용하는 경우 차이점(ODBC 버전 17)

이 버전의 ODBC는 Azure SQL Managed Instance 지원(프라이빗 미리 보기 확장)을 포함합니다. Managed Instance를 사용하는 경우 차이점에 대한 다음 설명 목록을 참조하세요.

> [!NOTE]
> Managed Instance를 사용하는 경우 여러 가지 차이점이 있습니다.
>
> - FILESTREAM이 지원되지 않습니다.
> - 로컬 파일 시스템 액세스는 지원되지 않지만 추적 파일과 같은 사항을 위해 필요합니다.
> - 로컬 경로에서 UDT 만들기는 지원되지 않습니다.
> - Windows 통합 인증은 지원되지 않습니다.
> - DTC는 지원되지 않습니다.
> - `sa`계정이 없습니다(기본 계정을 `cloudSA`라 함).
> - TDS 토큰 ERROR(0xAA)가 잘못된 서버 이름을 반환합니다.
> - 데이터베이스 이름에 특수 문자가 지원되지 않습니다.
> - ALTER DATABASE [dbname1] MODIFY NAME = [dbname2]가 지원되지 않습니다.
> - 오류 메시지는 언어 설정(Azure와 동일)에 관계 없이 항상 영어로 표시됩니다.

## <a name="131"></a>13.1

| 추가된 기능 | 세부 정보 |
| :------------ | :------ |
| [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]용 ODBC 드라이버 13.1에 [Always Encrypted](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) 및 [Azure Active Directory](../../../connect/odbc/using-azure-active-directory.md)에 대한 지원을 추가합니다. | 해당 추가된 지원은 Microsoft SQL Server 2016 또는 이후 버전에 연결할 때 사용할 수 있습니다. |
| Always Encrypted 및 Azure Active Directory에 대한 지원에 해당하는 연결 풀링 키워드 및 특성이 있습니다. | 해당 키워드 및 특성은 [SQL Server용 ODBC 드라이버의 드라이버 인식 연결 풀링](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)에서 설명합니다. |
| &nbsp; | &nbsp; |

## <a name="13"></a>13

| 추가된 기능 | 세부 정보 |
| :------------ | :------ |
| Microsoft SQL Server 2016 지원을 추가합니다. | ODBC 드라이버 버전 11의 기능을 유지합니다. |
| &nbsp; | &nbsp; |

## <a name="11"></a>11

| 추가된 기능 | 세부 정보 |
| :------------ | :------ |
| 새로운 기능을 포함합니다. | [Windows 기반 Microsoft ODBC Driver for SQL Server의 기능](features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md)을 참조하세요. |
| SQL Server 2012 원시 클라이언트에서 ODBC와 함께 제공되는 모든 기능을 포함합니다. | &nbsp; |
| &nbsp; | &nbsp; |
